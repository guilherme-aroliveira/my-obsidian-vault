COBOL is a procedural language, but it can be used to accomplish similar tasks that can be found in other more recent object oriented programming languages. 

COBOL is mainly used on the mainframe computer, but it's possible to simulate an environment on a personal computer.

GnuCOBOL --> formerly open COBOL, free COBOL compiler

Programs in COBOL are run using JCL.

JCL --> Job Control Language
- it's name for the scripting language that's used on IBM mainframes' operating systems to instruct the systems on how to run a batch job or how to start an online subsystem.
- the purpose of JCL it to say which program to run using which files or devices for input and output, and also indicate whether or not there area additional conditions that might require to skip a step.

>[!info]
>In a mainframe environment, programs can be executed in batch an online modes. Example: processing high-volume banking transactions through a VSAM file and applying it to the corresponding account. An example of online system can be a back office screen to enter customer information.

to test COBOL on a linux machine:
- `sudo apt-get install gnucobol`

COBOL syntax:

columns 1 to 6: 
- line 4 to 6:
	- contain comments, it has an `*` --> indicates a comment.
- optional columns, but they contain either sequence numbers or line numbers.
columns 8 to 11:
- line 8:
	- identification division must contain the program ID, but it can include fields such as the author.
	- program ID --> specifies the program name and can consist of 1 to 30 characters.
- considered the A margin.
- used from starting the program, such as identification division (mandatory division of every COBOL program).
- location to write division headers, section headers, paragraph names, and files descriptions.
column 7:
- used to indicate that is a continuation to the next line or a comment.
- might have an hyphen --> continuation of a non-numerical literal.

>[!note]
>It's important to start certain keywords and statement in specific column numbers, which reflect the historic use of punch cards.

statement end with a `.` instead of a `;` --> Example: `PROGRAM-ID. "HELLOWORLD".`

PROCEDURE DIVISION --> main part of the program 

`END PROGRAM` --> is optional, it's omitted the program ends when the are no more lines of code

`cobc -x <program_name>.cbl` --> to compile the program
`./<program_name>` --> to run the program

To create a variable in COBOL start with a level number. Ex: 01 --> highest level of element.

`WORKING_STORAGE SECTION` --> section do declare variables
ACCEPT --> to read a value from the terminal back into the variable
verb


`01 NAME`

PIC clause --> para alfanumericos
Every variable has to have a PIC clause, which is going to define: the type of data, how many characters, or how many numbers can be in that piece of data.

Example - Alphanumeric

`WORKING_STORAGE SECTION.`
`01 NAME PIC A(20)` --> 20 indicates the number of characters (from 0 zero 20).
`01 BMI PIC 999V99` --> 9 is used when the value of the variable is numeric, and V99 is used to include any decimal portion (implied decimal)