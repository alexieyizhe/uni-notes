__CS 241 | __ April 04, 2019

# Loaders

The **operating system** is responsible for loading all the programs that we write and executing them. The OS itself is also a program, and that requires it to be loaded into memory as well.

```pseudocode
// A rudimentary OS v1
repeat:
	p <- next program to run
	copy P into memory at 0x0
	jalr $0
	beq $0, $0, repeat
```

When we load programs, we may have collisions still since the OS requires to be loaded as well. 

So, we amend the logic for the OS to find an arbitrary location $\alpha$ in memory for the program and copy it there to run it:

```pseudocode
// OS v2
repeat: 
	p <- next program to run
  $3 <- loader(p)
  jalr $3
  beq $0, $0, repeat
  
// implementation of loader(p)
// assuming there are k words in the program, with
// each word being w_1 ... w_k
// alpha is the location in memory of the program
loader:
	alpha <- starting location in memory of the program
	n <- k + stack_space
	for i from 1 to k:
		MEM[alpha + 4 * i] = w_i
  $30 <- alpha + 4 * n         // starts the stack at the right place
  
	return alpha	
```

However, the issue now is that labels for IDs may be incorrect. They assume the program starts at `0x0`, so we need to update them with the proper $\alpha$ offset. But only the IDs - values that are constants (like numbers, etc) must not be modified.

```pseudocode
repeat:
	p <- next program to run
  $3 <- load_and_relocate(p)
  jalr $3
  beq $0, $0, repeat
```

This is still a problem, since when we translated the assembly into machine code, we are no longer able to tell if a value like `0x00000018` is a constant or an ID.

Recall that MERL files are object code - assembly code with some additional information stored in headers, etc.

MERL files are created by the assembler.

We can output our own object code instead of plain assembly code in order to update the labels to correct values. The code will look something like:

```php
beq $0 , $0 , 2
. word endfile // length of file
. word endcode // length of code + header

// Insert translated MIPS assembly code here (ex. below)
. word 0x4 // Constant (no relocation)
. word 0x8 // Constant (no relocation)
. word A // ID label (needs relocation)
B: 
  jr $31
A:
	beq $0, $0, B // (no relocation)
// END translated MIPS assembly code
    
// START OF RELOCATION TABLE
endcode: ; MERL symbol table
. word 0x1 ; Format code 1 means relocate !
. word 0x14 ; Location of A .
endfile:
```

This object code requires 2 passes to be outputted:

1. Track the size of the file, start counting addresses at `0x0c` instead of `0x0` and record the location of all `.word ID` instructions
2. Output the header, then the MIPS machine code, and then the relocation table

And the updated `loader(p)` algorithm is:

```pseudocode
read_line() // skip beq line 
endMod <-- read_line() // End of MERL file
codeLen <- read_line() - 12 // No header in codeLen
alpha <- findFreeRAM(codeLen) // Find space in RAM that can fit program

// Place program code in RAM
for (int i = 0; i < codeLen; i += 4)
  MEM [alpha + i] <- read_line()
  
i <- codeLen + 12 // start of reloc. table
  
// Relocate label addresses
while (i < endMod)
  should_format <- read_line()
  if (should_format == 1) // should relocate
    rel_addr <- read_line() // address relative to start of program
    
    // alpha + rel_addr - 12 since we don’t load header (3 lines).
    MEM [alpha + rel_addr - 12] += alpha - 12 // update offset: go forward by alpha and back by header len
    
  else
    ERROR
    
  i += 8 // jump to next entry
```

This algorithm can still produce code that only works at address 0 if you use hardcoded addresses like:

```
lis $2
.word 12 // user meant for this to be the address of line 4
jr $2 // jumps to line 4 (address 12)
jr $31
```

So, you should _never_ use hardcoded addresses instead of labels to refer to locations in the program.

Another problem: if we have different files that are meant to be merged together to form a program, we won't be able to update words that reference labels in different files.

This is what **linkers** allow us to do: combine multiple files while updating references to be valid, forming a complete program.

# Linkers

If we have two files, `a.asm` and `b.asm`:

```php
// a.asm
lis $3
.word label

// b.asm
label: sw $4, -4($30)
```

We can't load the program with the correct label replacements separately. We need to modify the assembler to replace `label` in `a.asm` with a placeholder sentinel value that indicates we cannot run this program until we get the value of the ID. 

We also need to differentiate labels that reference other files from simple typos, so we can still throw an error if a label doesn't exist in a file when it's unintended.

### External Symbol References (ESR)

The `.import SOME_ID` directive will tell the assembler that any occurrence of the label `SOME_ID` is _not_ a typo, and should occur in some other file. It does _not_ translate to a word in MIPS.

The assembler will error only if both:

1. The label `SOME_ID` is not in the current file.
2. There is no `.import SOME_ID` in the file.

This will result in an entry called an **external symbol reference (ESR)** in the relocation table. An ESR entry consists of:

1. The format code `0x11` (like a regular label)
2. The location address where the symbol is used (like a regular label)
3. Name of the symbol, split into:
   - A line indicating the length $n$ of the name
   - $n​$ lines, each with one ASCII character of the name

### External Symbol Definition (ESD)

If, along with `a.asm` and `b.asm`, we have a `c.asm` that _also_ contains the label `SOME_ID`. There's no indication as to which `SOME_ID` is being refered to in `a.asm`: the one in `b.asm`, or the one in `c.asm`?

We need the `.export SOME_ID` directive to indicate to the assembler that the label `SOME_ID` is meant to be used in other files when linking. This also does not translate to a word in MIPS.

This will result in an entry called an **external symbol definition (ESR)** in the relocation table. An ESD entry consists of:

1. The format code `0x05` (like a regular label)
2. The location address that the symbol represents
3. Name of the symbol, split into:
   - A line indicating the length $n$ of the name
   - $n$ lines, each with one ASCII character of the name



### The Linker Algorithm

At this point, the MERL file will contain our translated MIPS code, addresses that need relocationg, and addresses & names of each ESR and ESD. The linker has everything it needs to do its job.

```pseudocode
// This links two MERL files: m_1 and m_2 
alpha <- m_1.codeLen - 12

relocate m_2 by alpha // move m_2 below m_1

add alpha to each entry of m_2's symbol table

if (intersection of exports of m_1, m_2) is non-empty then
	ERROR // cannot export same name twice
end if

for (addr_1, label) in m_1's imports do
	if there exists a (addr_2, label) in m_2's exports then
		m_1.code[addr_1] = addr_2
		remove (addr_1, label) from m_1's imports
		add addr_1 to m_1's relocates

for (addr_2, label) in m_2's imports do
	if there exists a (addr_1, label) in m_1's exports then
		m_2.code[addr_2] = addr_1
		remove (addr_2, label) from m_2's imports
		add addr_2 to m_2's relocates

imports = union of m_1 and m_2's imports
exports = union of m_1 and m_2's exports
relocates = union of m_1 and m_2's relocates

// START OF MERL FILE 
output 0x10000002 // merl cookie (beq $0, $0, 2)
output total codeLen + total (import, export, relocates) + 12 // total len of file (code + header + reloc table)
output total codeLen + 12 // total len of code + header
output m_1.code
output m_2.code
output imports, exports, relocates
```



