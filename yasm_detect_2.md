Affected Version:
yasm 1.3.0 9defefae9fbcb6958cddbfa778c1ea8605da8b8b

Vulnerability Description:
The vulnerability is a memory leak bug located at line 71 of the file /yasm/tools/genmacro/genmacro.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

yasm download address:
https://github.com/yasm/yasm.git

Detailed Description of the Defect:

1.In the file /yasm/tools/genmacro/genmacro.c, a pointer to a string named str is defined at line 39. This pointer is dynamically allocated a memory block of size 1024 using the malloc function at line 59. When the program's condition at line 67 evaluates to true, the program returns at line 71 without freeing the memory area pointed to by the variable str, resulting in a memory leak defect, as illustrated below:

![image](https://github.com/LuMingYinDetect/yasm_defects/blob/main/yasm_5.png)
