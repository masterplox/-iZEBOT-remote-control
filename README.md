# -iZEBOT-remote-control
CMPS3111 Programming Project 2 
The Solution 
 
A. Write a BNF grammar for the meta-language for iZEBOT remote control that strictly adheres to the specification provided above. 
 
B. The BNF grammar may be written using BNF or EBNF. 
 
C. Write a computer program that: 
 
a. Upon starting it displays the BNF grammar for the meta-language for iZEBOT remote control b. Accepts an input string. c. If the user enters CANCEL when prompted for an input string, the program terminates. d. Conduct lexical/ syntax analysis on the input string to verify that is a sentence of the meta-language by attempting a LEFTMOST derivation based on the meta-language grammar on the input string. The derivation attempt is outputted to the screen.  i. If the derivation is not successful it generates an appropriate error and then the program prompts for another string (loops) ii. If the derivation is successful it indicates this, and then proceeds to: 1. prompts the user to press a key or click to continue; 2. draws the PARSE TREE for derivation of the input string, displays the tree; 3. prompts the user to press a key or click to continue; 4. generate the PBASIC (intermediate) program for the sentence accepted by inserting relevant header, footer and subroutine instructions from the PBASIC code provided or constructing the required body instructions; 
5. then displays onscreen the program generated; 6. and saves the program generated to a text file with named IZEBOT.BSP; 7. prompts the user to press a key or click to continue; 8. Loops back to A. 
 
e. The machine code for the BSP file will then be uploaded to the iZEBOT via the BASIC Stamp Editor. f. The correctness of the uploaded program will be verified by running the iZEBOT. 
 
D. As discussed in class, the generated PBASIC program will comprise a HEADER, a BODY, a FOOTER 1 SUBROUTINE, and a FOOTER 2 code blocks. The HEADER and FOOTER blocks are static while the BODY and SUBROUTINE blocks are dynamic, both dependent on the button selected for programming and the movements assigned to the buttons selected. 
 
See slide 13 from the class discussion for an example of a program generated for a valid sentence. 
 
The following is the necessary code and format for the respective blocks: 
 
HEADER BLOCK code 
 
 '{$STAMP BS2p}  '{$PBASIC 2.5}  KEY     VAR     Byte  Main:     DO           SERIN 3,2063,250,Timeout,[KEY] 
 
BODY BLOCK - Button assignment code (1 or more lines depending on how many keys are programmed) 
 
IF KEY = “x" OR KEY = “y" THEN GOSUB routine 
 
Where  x   is A, B, C, or D;   y   is a, b, c, or d;   routine   is Forward, Backward, T_Left, T_Right, S_Left, S_Right, or Motor_OFF 
 
FOOTER 1 Code 
 
   LOOP  Timeout:  GOSUB Motor_OFF      GOTO Main 
 
 '+++++ Movement Procedure ++++++++++++++++++++++++++++++ 
 
SUBROUTINE BLOCK code 
 
 Forward:   HIGH  13 : LOW 12 : HIGH 15 : LOW 14 : RETURN  Backward:  HIGH  12 : LOW 13 : HIGH 14 : LOW 15 : RETURN  T_Left:    HIGH  13 : LOW 12 : LOW  15 : LOW 14 : RETURN  T_Right:   LOW   13 : LOW 12 : HIGH 15 : LOW 14 : RETURN  S_Left:    HIGH  13 : LOW 12 : HIGH 14 : LOW 15 : RETURN  S_Right:   HIGH  12 : LOW 13 : HIGH 15 : LOW 14 : RETURN 
 
FOOTER 2 code 
 
 Motor_OFF: LOW   13 : LOW 12 : LOW  15 : LOW 14 : RETURN  '+++++++++++++++++++++++++++++++++++++++++++++++++++++++ 
 
Syntactic structure of generated PBASIC program 
 
Header Code Body Code   (content depends on the button and the movements selected)  Footer Code 1 Subroutine Code  (include only relevant subroutines for the movements selected) Footer Code 2 
 
The Program [42 points] 
 
A. The program should comprise: 
 
a. A MAIN that displays the BNF grammar for the meta-language and then prompts for an input string. If the input string is “CANCEL” the program terminates, else MAIN should call: 
 
i. A subprogram that executes a LEFTMOST derivation of the input string showing each sentential form and the final generated sentence. If the derivation cannot complete successfully (i.e. the string is not recognized by the grammar), the subprogram should generate an appropriate error message. The subprogram then prompts the user to press a key or click to continue. 
 
ii. A subprogram that is called if the derivation is successful which draws the PARSE TREE for derivation of the input string, displays the tree, and then prompts the user to press a key or click to continue.  
 
iii. A subprogram that is called after subprogram (ii) if the derivation is successful which: 
 
1. generates the PBASIC program code by applying the relevant semantics for the input string,  2. displays onscreen the generated code,  3. and saves the generated code in a text file named IZEBOT.BSP 4. and then prompts the user to press a key or click to continue. 
 
