#Preface
Reading Note of "Gnu make" document

The document original url:	
	https://www.gnu.org/software/make/manual/html_node/index.html#SEC_Contents
	
#Overview
	Makefile describes tasks where based on when and how, especially updating files from some conditions such as depending files changed etc. 

##About the original document
	- HTML 
	- Next link points to same level, not sub level. e.g. If you are in chapter 1, then Next points to chapter 2, not Chapter 1.2 .
	- Sub chapter level shown as link on button of current chapter.
	
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
	
`
edit : main.o kbd.o command.o display.o \
        insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o \
		insert.o search.o files.o utils.o

main.o : main.c defs.h
        cc -c main.c
kbd.o : kbd.c defs.h command.h
        cc -c kbd.c
command.o : command.c defs.h command.h
        cc -c command.c
display.o : display.c defs.h buffer.h
        cc -c display.c
insert.o : insert.c defs.h buffer.h
        cc -c insert.c
search.o : search.c defs.h buffer.h
        cc -c search.c
files.o : files.c defs.h buffer.h command.h
        cc -c files.c
utils.o : utils.c defs.h
        cc -c utils.c
clean :
        rm edit main.o kbd.o command.o display.o \
           insert.o search.o files.o utils.o
`

	- \ spilit long line
	- Default Goal : The goal that make invokes without specifying the target.
		- The first rule that has real target is usually took as default rule, the target of this rule is default target. 
		- All rules whose targets are prerequisites of default target will be invoked on default goal. 
		- .DEFAULT_GOAL variable changes the default goal to specified one.
	- Special rule: If a target is not prerequisite of default target, its rule can only be invoked by `make target` for example, `make clean`
		
	- Implicit rule: 
		- c to o file `cc -c`  omit the implicit recipe and prerequisite:
`
main.o : main.c defs.h
	cc -c main.c
`
can be simplified to
`
main.o : defs.h
`
# Writing Makefile

`"The information that tells make how to recompile a system comes from reading a data base called the makefile."`	-- Chapter 3

Is it because my poor English skill that I feel it really awkward to understand why simple things described as this. Shall it be 
  
  `The Makefile tells make what to do and how to do it.` ?  

# What make file contains
	Pretty mess when describe what Makefile contains. Here are content that is reorganized
	- Makefile can contains 5 different entities
		- explicitly rules
			A explicit rule contains:
				target, prerequisites and recipe. 
		- implicit rules
			A rule has implicit recipe and prerequisites. 
		- variable definitions
		- directives
			including other makefile, condition and multi-line variables
		- comments #
		
# include directive
`include foo *.mk $(bar)...`
	- tells make to include other files
	- if files can not be found, it searches -I directories plus a set of predefined directories for c source.
	- make scan file twice, the first run finish all that can be done, if some included file missing, it use partial results of first scan (such as -I) to search the missing file, it that fails, make emits errors.
`-include filenames...`
	Same as `include`, but ignore the missing file error.

	## MAKEFILES environment variable
	This variable is a list of string, each is a makefile that is included into makefile on front. Specially: Default goal is never taken from these files. 
    	
    ## Remake Makefiles
	Makefile can be remade from other files, such as RCS, SCCS files. 
	- The makefile itself is a target of a rule.

#Writing rules
	- Order of rule is not significant
	- First rule of the first target is the default goal
	- pattern rule has no effect on the default goal.
## rule syntax
	` 
	targets : prerequisites
			recipe
			...
	`
	or 
	` 
	targets : prerequisites ; recipe
			recipe
			...
	`
	### targets, prerequisites
	- usually one rule one target
	- Space seperated.
	- Space in name can be escaped
	- Wildcard targets
	- a(m), member m of archive file as entities
	
	### recipe
	- start with a tab in next line to prerequisites
	- first recipe can appear same line of prerequisite, after ';'
	- $ sign is for variable, to escape it, use $$

## Type of prerequisites
	
	
	
	
	
	
 
	