**CS 246 |** Sept 18, 2018


# Shell Scripting
A shell script is a series of shell commands (`bash` or otherwise) contained in a file that can be run all at once.
 - write `#!/bin/bash` at the top to denote a bash script (the shell will look in all the `PATH`s it knows to find a bash executable to run the script)

### Syntax
__Arguments:__
 - Access specific arguments passed in on the cmd line through `$1`, `$2`, etc.
 - `$#` denotes number of arguments
 - `$*` gives all arguments

__If Statements:__
```bash
if [ $1 -neq "pass" ]; then
  echo "you fail"
elif [ $1 -eq "probation" ]; then
  echo "oh it gets worse"
else
  echo "ok another chance"
fi
```
 - Note that the spaces in the statement ` [ ... ] ` are mandatory as the brackets are aliases for the `test` command, so they are commands themselves.

__Loops:__
```bash
for i in {START_VAL..END_VAL..STEP_VAL}; do
    echo "$i is inclusive"
done

for var in ~/Documents/*.txt; do
  echo $var
done

for output in $(COMMAND); do
  echo $output
done
```

__Functions:__
```bash
some_fn () {
  echo "this function is called a subroutine in bash"
  exit 0
}

some_fn # call the function
```

__Misc:__
| Syntax | Usage |
| ------ | ----- |
| `exit` | quits program |
| `-a`   | && for statements  |
| `-o`   | \|\| for statements  |
| `-e FILE` |  T if file exists |
| `-z STRING` | T if string len is 0  |
| `=`    | == for strings |
| `-eq`  |  ==  for ints  |
| `-ne`  |  !=  for ints  |
| `-lt`  |  <   for ints  |
| `-le`  |  <=  for ints  |
| `-gt`  |  >=  for ints  |
| `-ge`  |  >=  for ints  |
