# ur_a_wizard

Setting up the emulator
```bash
wget https://user.eng.umd.edu/\~yavuz/teaching/courses/enee350/vesp-source-code/vesp1.1X/main.cpp
g++ -o vesp1_1 main.cpp
```

I manually translated the opcodes in the `spell.vsp` file into mnemonics. 
This architecure has 16bit opcodes. The weird thing about them is that it identifies the instruction using only the first nibble (most significant), and the rest three are either ignored or alter the behaviour in some way.
```
2000 0000   LDA A        0000
2001 0000   LDA B        0000
2010 0000   LDA [010]    0000
2000 0000   LDA A        0000
2001 0001   LDA B        0001
2010 0000   LDA [010]    0000
0DA3        ADD
1000        CMP
07BC        ADD
2001 0001   LDA B        0001
05F0        ADD
0D31        ADD
1000        CMP
098B        ADD
2001 0001   LDA B        0001
0ACC        ADD
0601        ADD
1000        CMP
0C3F        ADD
2001 0001   LDA B        0001
087C        ADD
0C24        ADD
1000        CMP
0056        ADD
2001 0001   LDA B        0001
2010 000A   LDA [010]    000A
2000 0001   LDA A        0001
3001 0010   MOV [010] A
7000        HLT
```

The `LDA` instruction (`2xxx`) stores the immediate value in the `[xxx]` address.
The `ADD` instruction (`0xxx`) stores the result A + B into A.

In the translated program, observe the opcode for each ADD instruction. Taking all the `ADD` opcodes,
```python
add = [ '0DA3', '07BC',  '05F0', '0D31', '098B', '0ACC', '0601', '0C3F', '087C', '0C24', '0056' ]
flag = "".join([ op.strip('0') for op in add ]).lower()
print("flag{" + flag + "}")
```
