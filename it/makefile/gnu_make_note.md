#Preface
Reading Note of "Gnu make" document

The document original url:	
	https://www.gnu.org/software/make/manual/html_node/index.html#SEC_Contents
	

# About the original document
	- HTML format. 
	- Next link doesn't points to next chapter, not sub-chapter 
	- Sub chapter shown as link on button of their parent chapter. 
	
#Introduction
##rule
	`
	target ... : prerequisites ...
		recipe
		...
		...
	`
	- 1...+ Target
	- 0...+ prerequisites
	- 0...+ recipe
	- Tab is in front of each recipe
	
#Simple Makefile
	
	- spilit long line : \
	- Default Goal (DG): first target in first rule 
	- .DEFAULT_GOAL variable changes the DG to specified one.
	- Independant rule: A rule that is not DG's dependants. It is invoked by `make rulename`. Usually rulename is a phony target, such as `make clean`.
	
	- Implicit rule (IL): 
		- c to o file `cc -c`. To use this IL:  omit the .c prerequisites and recipe.

		Explicit rule (EL):
		`main.o : main.c defs.h
			cc -c main.c`
		Same in IL: 
		`main.o : defs.h`

# Writing Makefile
## What M file contains
	- There are 5 different entities
		- EL 
		- IL 
		- variable definitions
		- directives
		- comments #

## Remake Makefiles
	M remakes the final makefile(FMf) before it starts to next step.
	- import other makefiles from `MAKEFILES` variable and `include` directive.
	- process the rule that target is makefile, to get latest version

## Environment variable MAKEFILES 
	- MAKEFILES contains a string list of makefiles(MMs). 
	- M imports all MMs, put them in front of FMf.
	- M doesn't take any rules as DG from MMs 

## Include directive
`include foo *.mk $(bar)...`
	- M searches couple places for included file, including directories defined by -I.
	- M scans file twice. 
	- Included makefiles share the global variables
	- To ignore the missing file error, use `-include ...`
	
#Writing rules
	- First rule of the first target is the DG
	- Order of other rules is not significant
	- Pattern rule has no effect on the DG.

## rule syntax
	`targets : prerequisites
			recipe
			...`
	or 
	`targets : prerequisites ; recipe`				# First recipe after the prerequisites
			`recipe
			...`
	
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

	### Type of prerequisites
	- Normal prerequisites : When they changes, target needs be rebuild
	- Order only prerequisites: They don't obsolete the target when changes.
	- `foo: normal_pre | order_only_pre
			...`
	- Example:
		`objs = foo.o bar.o
		
		foo/%.o : %.c		# Wildcard rule, no DG 
			cc -c $< -o $@
			
		all : $(objs)		# DG. phony target. force to rebuid all. 
		
		# because desti 
			
	
	
	
	
 
	