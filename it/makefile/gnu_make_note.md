
# Preface
Reading Note of "Gnu make" document

[HTML One Page mode manual](https://www.gnu.org/software/make/manual/make.html#SEC_Contents)

[PDF format](https://www.gnu.org/software/make/manual/make.pdf)	

# About the original document
- There are multiple format of GNU Make Manul. One page mode HTML has better navigation. 
	
# Introduction
## rule
```makefile	
target ... : prerequisites ...
	recipe
	...
	...
```
+ Count of items

Item name | count
:----------|------: 
Target | 1+
prerequisites |0 or 1+ 
recipe | 0 or 1+

+ Tab is in front of each recipe
	
# Simple Makefile
	
- spilit long line : \
- Default Goal (DG): first target in first rule 
- .DEFAULT_GOAL variable changes the DG to specified one.
- Independant rule: A rule that is not DG's dependants. It is invoked by `make rulename`. Usually rulename is a phony target, such as `make clean`.
	
- Implicit rule (IR): 
	- c to o file `cc -c`. To use this IL:  omit the .c prerequisites and recipe.

Explicit rule (ER):
```makefile
main.o : main.c defs.h
	cc -c main.c
```
Same in IR: 
```makefile
main.o : defs.h
```

# Writing Makefile
## What MK file contains
- There are 5 different entities
	- ER
	- IR 
 - variable definitions
 - directives
 - comments #

## Remake Makefiles
M remakes the final makefile(FMf) before it starts to next step.
- import other makefiles from `MAKEFILES` variable and `include` directive.
- process the rule that target is makefile, to get latest version

## Environment variable MAKEFILES 
- M contains a string list of makefiles(MMs). 
- M imports all MMs, put them in front of FMf.
- M doesn't take any rules as DG from MMs 

## Include directive
```makefile
include foo *.mk $(bar)...
```
- M searches couple places for included file, including directories defined by -I.
- M scans file twice. 
- Included makefiles share the global variables
- To ignore the missing file error, use `-include ...`
	
# Writing rules
- First rule of the first target is the DG
- Order of other rules is not significant
- Pattern rule has no effect on the DG.

## rule syntax
```makefile
targets : prerequisites
	recipe
	...
```
or 
```makefile 
targets : prerequisites ; recipe				# First recipe after the prerequisites
	recipe
	...
```
	
### targets, prerequisites
- Usually one rule per target.
- Entities are seperated by space.
- Escape: `name\ with\ space: ...`
- Wildcard 
- a(m), member m of archive file as entity
	
### recipe
- Indented with tab charater
- First recipe can be same line as prerequisite. 
- use $$ to escape the $. 

## Type of prerequisites
- Normal prerequisites : When they changes, target needs be rebuild
- Order only prerequisites: They don't obsolete the target when changes.
```makefile
foo: normal_pre | order_only_pre
	...
```                              
- Example:
```makefile
objs = foo.o bar.o

foo/%.o : %.c		# Wildcard rule, no DG 
	cc -c $< -o $@
		
all : $(objs)		# DG. phony target. force to rebuid all. 
```		
## Wildcard

Wildcard	|represents		| Example
----------------|-----------------------|-----------------
\*		| Any charaters		|  *.c
?		| Any charater		|  a?.c	
[a,b]		| a or b		|  m[a,e]n matches man or men
~/ 		| home              	|
~jhon/ 		| jhon's home		|
\x		| escape            	|

- *Pitfal* : If none of files matches wildcard, then wildcard itself (verbatim) become filename. This made direct use wildcar almost improper. Use $(wildcard, pattern...) to avoid pitfal.
- Wildcard expansion is not happened except it is in rule, or in wildcard function.
	- rule 			: immediatly, make expands target and prerequisites, shell process recipe.
	- $(wildcard,..): immediatly, make.
	- variable		: not expanded
- Forward slash		: To avoid escape slash confliction, use forward slash only on Windows path.


## Searching

 
			
	
	
	
	
 
	
