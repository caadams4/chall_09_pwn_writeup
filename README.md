# chall_09_pwn_writeup
send a null

'checksec ./chall_09' yeilds full green. So no stack smashing, no executable stack etc. 

What ever will we do?

Lets open the binary in radare2 and reverse. 

![image](https://user-images.githubusercontent.com/79220528/160525873-528eaab5-3c1b-4aa7-bb3b-3624a9783818.png)

So, fgets reads in 0x32 bytes to var_50, cant overwrite other variables... that's limiting. 

Sets var_54 to the strlen of the input string. 

Iterates through the string and compares the XORed input to an object[iteration]. 

The loop continues until the iteration is greater than the strlen. Which is **NEVER!**

The only way this loop will break is if the strlen of input is less that 0 ... wut

So... lets just send a null byte (0x00) and see what happens.

![image](https://user-images.githubusercontent.com/79220528/160526691-7e23c8f3-d8dc-4e27-b1fe-c8f8d12973d0.png)

**POW**
