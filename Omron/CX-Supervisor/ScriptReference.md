# CX-SUPERVISOR - SCRIPT REFERENCE


## FUNCTIONS AND METHODS

### PAGE COMMANDS

#### Display page
- **Sintax**
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
  
  
# BIBLIOGRAPHY

[CX-Supervisor Script Reference Omron official manual](https://assets.omron.eu/downloads/manual/en/w09e_cx-supervisor_reference_manual_en.pdf)
