# SYSMAC STUDIO - INSTRUCTION REFERENCE


## INSTRUCTION DESCRIPTIONS

### ST STATEMENT INSTRUCTIONS

#### IF
- **Operators**:
  + *Equals* (a=b)
  + *Not equals* (a<>b)
  + *Comparision* (a<b, a<=b, a>b, a>=b)
  + *Logical AND* (a AND b, a & b)
  + *Logical OR* (a OR b)
  + *Exclusive OR* (a XOR b)
  + *NOT* (NOT a)

```java
IF condition expression 1 THEN
  IF condition expresion 11 THEN
    statement 11;
  ELSIF condition expression 12 THEN
    statement 12;
  ELSE
    statement 13;
  END_IF;
ELSIF condition expression 2 THEN
  statement 2;
ELSE
  statement 3;
END_IF;
```
  
  
# BIBLIOGRAPHY

[NJ/NX Instructions Reference Omron official manual](https://industrial.omron.us/en/media/NJ_NX_Instructions_ReferenceMan_en_201704_W502-E1-20_tcm849-112705.pdf)
