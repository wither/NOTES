
# Vuln Chat

`printFlag()` function at `0x0804856b` that uses `/bin/cat` to print the contents of `./flag.txt`.

```c
void printFlag(void)

{
  system("/bin/cat ./flag.txt");
  puts("Use it wisely");
  return;
}
```



```c
undefined4 main(void)

{
  undefined1 password [20];
  undefined1 name [20];
  undefined4 format;
  undefined1 local_5;
  
  setvbuf(stdout,(char *)0,2,20);
  puts("----------- Welcome to vuln-chat -------------");
  printf("Enter your username: ");
  format = 0x73303325;
  local_5 = 0;
  __isoc99_scanf(&format,name);
  printf("Welcome %s!\n",name);
  puts("Connecting to \'djinn\'");
  sleep(1);
  puts("--- \'djinn\' has joined your chat ---");
  puts("djinn: I have the information. But how do I know I can trust you?");
  printf("%s: ",name);
  __isoc99_scanf(&format,password);
  puts("djinn: Sorry. That\'s not good enough");
  fflush(stdout);
  return 0;
```



```
                             undefined main()
             undefined         <UNASSIGNED>   <RETURN>
             undefined1        Stack[-0x5]:1  local_5                                 XREF[1]:     080485c5(W)  
             undefined4        Stack[-0x9]:4  format                                  XREF[3]:     080485be(W), 
                                                                                                   080485cd(*), 
                                                                                                   08048630(*)  
             undefined1[20]    Stack[-0x1d]   name                                    XREF[3]:     080485c9(*), 
                                                                                                   080485d9(*), 
                                                                                                   0804861b(*)  
             undefined1[20]    Stack[-0x31]   password                                XREF[1]:     0804862c(*)  
                             main                                            XREF[4]:     Entry Point(*), 
                                                                                          _start:08048487(*), 08048830, 
                                                                                          080488ac(*)  
        0804858a 55              PUSH       EBP
```



```shell
python3

Python 3.12.3 (main, Feb  4 2025, 14:48:35) [GCC 13.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 0x31 - 0x1d
20
```