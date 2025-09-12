# ADD

FORMAT: `add rd, rs1, rs2`   <br><br>
(rd = destination register, rs1 = source register 1, rs2 = source register 2)
<br>

<b>NOTE:</b>f,g,h,i,j --> x19,x20,x21,x22,x23<br><br>
<b>Question:</b> 

1. f=g+h+i+j
```asm
add f,g,h
add f,f,i
add f,f,j
```
2. f = (g+h) - (i+j)
```asm
add t0,g,h
add t1,i,j
sub f,t0,t1
```
3. f = g
```asm
add f,g,x0
```  
# ADDI
FORMAT: `addi rd, rs1, imm`   <br><br>
(rd = destination register, rs1 = source register 1, imm = immediate value)
<br>
<b>Question:</b>

1. f= g+7
```asm
addi f,g,7
```
2. f = g
```asm
addi f,g,0
``` 
3. f = 100  (initializing a variable)
```asm  
addi f,x0,100
```

# CONDITIONAL BRANCHES
FORMAT: `beq rs1, rs2, label`   <br><br
(label = target label to branch to if condition is met.
label itself is not an instruction, it acts as a address marker for the instruction)
<br><br>

## TYPES:
- beq: Branch if Equal
- bne: Branch if Not Equal
- blt: Branch if Less Than
- bge: Branch if Greater than or Equal
- bltu: Branch if Less Than (Unsigned)
- bgeu: Branch if Greater than or Equal (Unsigned)

<b>Question:</b>

1.
 ```c
if (i==j){
    f=g+h;    
} 
```
```asm
bne i,j,END
add f,g,h
END:
```
2.
 ```c
if (i==j){
    f=g+h;    
}else{
    f=g-h;
}
```
```asm
bne i,j,ELSE
add f,g,h
END
ELSE:
sub f,g,h
END:
```

```asm
bne i,j,ELSE
add f,g,h
beq x0,x0,END
ELSE:
sub f,g,h
END:
```

# LOOPING STATEMENTS
FORMAT: 

<img src="Resources/Screenshot 2025-09-12 093511.png">

<b>Question:</b>

1.
```c
sum=0;
i=0;
while(i<100){
    sum+=i;
    i++;
}
```
```asm
Loop:
    bge i,100,END
    add sum,sum,i
    addi i,i,1
beq x0,x0,Loop
END:
```
2.
```c
sum=0;
for(i=0;i<100;i++){
    sum+=i;
}
```
```asm
    addi sum,x0,0
    addi i,x0,0
beq x0,x0,Test
Loop:
    add sum,sum,i
    addi i,i,1
Test:
    blt i,100,Loop
```