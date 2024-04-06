## Controlling Terminal
Within a session, one terminal device is designated as the controlling terminal.
This terminal is responsible for handling input and output for certain processes and
is the point of interaction between the user and the session
tty - prints the controlling terminal

## Controlling Terminal is responsible for
- session handling
- process and job control
- foreground/background processes
- signal handling
- terminal settings

### Session Handling
In Unix-like operating systems, a session is a collection of processes grouped together
under a common context. Typically, a session starts when a user logs in and ends when the user logs out.

### Foreground & Background Processes
Processes running in the foreground are those that have access to the controlling terminal for input and output.
Processes in the background do not have access to the terminal by default.


### Terminal Settings
The controlling terminal is responsible for managing terminal settings, such as line discipline, echo behavior, and terminal modes.
`stty`

### TTY Driver
The TTY driver is also provided by the kernel, it implements session management which will help user to have many processes running at the same time and only interacting with foreground process which his/her input will be redirected to it and only the foreground process will be allowed to send output to the TTY device.



### Line Discipline
the line discipline (LDISC) which is provided by the kernel to allow editing
commands features like backspace, erase word, and clear line, it also handles
special characters such as the interrupt character (CTRL + C).

Advanced applications like vim and ssh disables these features by putting the
line discipline into raw mode, so they can handle all these stuff themselves

The kernel provides many line disciplines but only one is enabled by default and
connected to a serial device. The default one, which provides line editing, is called N_TTY (drivers/char/n_tty.c)

The line discipline does not handle keys like Up, Left, Down, Right, that’s why when you
press them you will see something like ^[A the ^[ is called the escape sequence. the
terminal emulator encodes keystrokes that has no character representation

### Line Discipline Modes
- raw mode
- cooked mode(canonical mode)

Most interactive applications (editors, mail user agents, shells, all programs relying on curses or readline) run in raw mode, and handle all the line editing commands themselves. The line discipline also contains options for character echoing and automatic conversion between carriage returns and linefeeds. Think of it as a primitive kernel-level sed(1), if you like.

### Carriage Return and Line Feed
- carriage return(\r) moves the cursor to the beginning of the current line
- linefeed(\n) moves the cursor down the next line without jumping to the beginning of that line
- So when we hit enter cursor is moved down the next line while jumping to the  beginning of the line. So the combination of CR and LF applies.

### Seat
A seat consists of all hardware devices (display, keyboard, mouse ..) assigned to a specific workplace.
In Linux you can list seats using loginctl list-seats, and loginctl seat-status seat0 to list devices assigned to seat seat0

### Echoing

### Modes

Pseudo Terminals(pty)
Master
Slave

Terminal emulator is launched from a graphical environment that is itself launched from a virtual terminal
[virtual terminal]->[graphical env]->[terminal emulator]

How to they interact in the terminal emulators
How to they interact in ssh
what is sane state.

### Shells
In Unix system administration, a user's shell is the program that is invoked when they log in.

### Commands
```
python3 -c 'import pty; pty.spawn("/bin/bash");'
tty
stty
ps
chvt [tty number] to switch between ttys in the terminal. (chvt stands for change virtual terminal)

echo "Hello World" > /dev/pts/2
```

We should be able to understand
> the difference between terminal, tty, shell, console and how they work together
> What is ioctl and how it is related to terminals?
> What are shells and how they spawn processes?
> How pseudo-terminals work?
> How terminal emulators work?
> What are the roles of pseudo-terminals for implementing ssh.


## References
### Articles and Documents
```
https://yakout.io/blog/terminal-under-the-hood/
https://www.linusakesson.net/programming/tty/index.php
https://www.baeldung.com/linux/pty-vs-tty
https://linuxhint.com/what-does-tty-stand-for/
https://itsfoss.com/what-is-tty-in-linux/
```

### Questions and Discussions
```
https://unix.stackexchange.com/questions/4126/what-is-the-exact-difference-between-a-terminal-a-shell-a-tty-and-a-con
https://askubuntu.com/questions/14284/why-is-a-virtual-terminal-virtual-and-what-why-where-is-the-real-terminal
```




