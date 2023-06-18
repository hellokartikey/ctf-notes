# ur_a_wizard

Setting up the emulator
```bash
wget https://user.eng.umd.edu/\~yavuz/teaching/courses/enee350/vesp-source-code/vesp1.1X/main.cpp
g++ -o vesp1_1 main.cpp
```

I manually translated the opcodes in the `writeright.vsp` file into mnemonics. 
This architecure has 16bit opcodes. The weired thing about them is that it identifies the instruction using only the first nibble (most significant), and the rest three are either ignored or alter the behaviour in some way.
```
LDA A 0000
LDA B 0000
LDA B 0004
LDA A 00CB
ADD
MOV [0209] A // cf
LDA B 0007
LDA A 006C
ADD
MOV [0180] A // 73
LDA A 0034
LDA B 0006
ADD
MOV [012B] A // 3a
LDA B 0005
LDA A 00BF
ADD
MOV [023B] A // c4
LDA B 0007
LDA A 00EC
ADD
MOV [0120] A // f3
LDA B 0003
LDA A 00F1
ADD
MOV [0229] A // f4
LDA B 0005
LDA A 007c
ADD
MOV [1D13] A // 81
LDA B 0005
LDA A 008B
ADD
MOV [020F] A // 90
LDA B 0008
LDA A 0018
ADD
MOV [01D0] A // 20
LDA B 0003
LDA A 0047
ADD
MOV [01D7] A // 4a
LDA B 0006
LDA A 008A
ADD
MOV [01B8] A // 90
LDA B 0009
LDA A 002D
ADD
MOV [017D] A // 36
LDA B 0006
LDA A 0001
ADD
MOV [01A9] A // 07
LDA B 0001
LDA A 009A
ADD
MOV [018B] A // a1
LDA B 0001
LDA A 00B3
ADD
MOV [0200] A // b4
LDA B 0009
LDA A 0067
ADD
MOV [0240] A // 70
HLT
```

Concatenating all the values that are being stored in memory yields the flag.
```python
store = [ 'cf', '73',  '3a', 'c4', 'f3', 'f4', '81', '90', '36', '07', 'a1', 'b4', '70' ]
flag = "".join(store).lower()
print("flag{" + flag + "}")
```
