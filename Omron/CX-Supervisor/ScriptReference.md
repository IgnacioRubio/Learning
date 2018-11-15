# CX-SUPERVISOR - SCRIPT REFERENCE

## SCRIPT LANGUAGE

### CONTROL STATEMENTS

#### Simple conditional statements
- **Syntax**
```java
IF condition THEN
 statementblock1
ENDIF
``` 
or
```java
IF condition THEN
 statementblock1
ELSE
 statementblock2
ENDIF
```
*Argument:* condition --> the condition es made up of points and constants, using relational. logical or arithemetical notation as a test. The condition can evalute Boolean state 'TRUE' and 'FALSE', Interger or Real numbers, or a text string.
*Argument:* statementblock1 --> one or more statements which are perfomed if the condition is met.
*Argument:* statementblock2 --> one or more statements which are perfomed if the condition is met.
- **Examples**
```java
IF fuel < 0 THEN
 fuel = 0
ENDIF
```

### SUBROUTINES

#### return
- **Syntax**
```java
RETURN
```
- **Example**
```java
IF limit > 1000 THEN
 RETURN
ELSE
 value = limit
REM final part of script
POLYGON_1.COLOUR = red
ELLIPSE_5.WIDTH = value
```

## FUNCTIONS AND METHODS

### PAGE COMMANDS

#### Display page
- **Syntax**
```java
display ("pagename")
```
or
```java
display ("pagename", X, Y)
```
*Argument:* pagename (string) --> this is the name of the page for display, based on its filename without the file extension
- **Examples**
```java
display ("CAR")

textpoint = "CAR"
display (textpoint)

// 'CAR.PAG' is displayed in a custom position, 100 pixels across from the left of the main windows and 200 pixels down from the top 
display ("CAR", 100, 200)
```


#### Close page
- **Syntax**
```java
close ("pagename")
```
*Argument:* pagename (string)--> this is the name of the page for display, based on its filename without the file extension
> **Note:** The 'close' operation will cause the page to be unloaded, including all objects, ActiveX controls and scripts.  They can't be accessed.
 
> **Note:** Where the script containing the 'close' instruction is on the page to be closed, this should be the last instruction in the script s it will cause the script to be unloaded.

- **Examples**
```java
close ("CAR")

textpoint = "CAR"
close (textpoint"
```


### TEXT COMMANDS

#### Message
- **Syntax**
```java
Message("message")
```
*Argument:* message (string) --> contains the text string that is displayed in the message box.
 - **Examples**
```java
Message("this is a message")
```
 
# BIBLIOGRAPHY

[CX-Supervisor Script Reference Omron official manual](https://assets.omron.eu/downloads/manual/en/w09e_cx-supervisor_reference_manual_en.pdf)
