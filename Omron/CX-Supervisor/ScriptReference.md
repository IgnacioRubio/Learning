# CX-SUPERVISOR - SCRIPT REFERENCE


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
1. *Argument*: pagename --> this is the name of the page for display, based on its filename without the file extension
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
1. *Argument*: pagename --> this is the name of the page for display, based on its filename without the file extension
> **Note:** The 'close' operation will cause the page to be unloaded, including all objects, ActiveX controls and scripts.  They can't be accessed.
 
> **Note:** Where the script containing the 'close' instruction is on the page to be closed, this should be the last instruction in the script s it will cause the script to be unloaded.

- **Examples**
```java
close ("CAR")

textpoint = "CAR"
close (textpoint"
```
 
# BIBLIOGRAPHY

[CX-Supervisor Script Reference Omron official manual](https://assets.omron.eu/downloads/manual/en/w09e_cx-supervisor_reference_manual_en.pdf)
