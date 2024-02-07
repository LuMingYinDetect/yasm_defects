Affected Version:
yasm 1.3.0 9defefae9fbcb6958cddbfa778c1ea8605da8b8b

Vulnerability Description:
The defect occurs at line 177 in the file /yasm/modules/preprocs/nasm/nasmlib.c.This defect is a null pointer dereference issue, where a null pointer is passed into the strlen function. As glibc does not check whether the pointer passed to the strlen function is null, passing a null pointer to the strlen function can lead to a program crash.

yasm download address:
https://github.com/yasm/yasm.git

Detailed Description of the Defect:

1.The program passed &(tline->text) as the second argument to the nasm_src_get function on line 4163 of the file /yasm/modules/preprocs/nasm/nasm-pp.c, as shown in the following illustration:

![image](https://github.com/LuMingYinDetect/yasm_defects/blob/main/yasm_1.png)

2.In the nasm_src_get function, the parameter corresponding to &(tline->text) is named xname. On line 162, when file_name is empty, *xname is assigned the value NULL, and then returned on line 164, as illustrated below:

![image](https://github.com/LuMingYinDetect/yasm_defects/blob/main/yasm_2.png)

3.After the function returns from nasm_src_get, the program subsequently passes &(tline->text) to the nasm_quote function, as shown in the following illustration:

![image](https://github.com/LuMingYinDetect/yasm_defects/blob/main/yasm_3.png)

4.
In the nasm_quote function, the parameter corresponding to &(tline->text) is named str. On line 177, the program passes *str to the strlen function, thereby causing a null pointer dereference issue, as illustrated below:

![image](https://github.com/LuMingYinDetect/yasm_defects/blob/main/yasm_4.png)
