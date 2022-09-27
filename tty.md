# Commands for manage TTY

## Resume
During an attack phase, when obtaining a reverse shell given a victim IP during a pentesting, there comes a time when we have to connect
to the victim machine in order to rummage through internal files or even escalate their privileges. It is at that moment when we have to make a
tty treatment

## ¿What is the TTY?
tty is a Unix (also similar to GNU/Linux) command that prints (writes to standard output) the terminal's filename from standard input.
Remember that this is executed through a BASH (bourn again shell).

## ¿Why is it necesary?
When connecting to a victim machine (remotely) there are certain complications and restrictions when operating bash commands.
For example, if we press [CTRL + C], this tells bash to cut off all communication already established, which causes us to lose all the work we have done.
So, treating the TTY will help us avoid these problems and therefore improve the performance of our bash.

## ¿How do we make it?
To make a correct treatment of a TTY, it is first necessary to be connected (and to have achieved a reverse shell). Usually this step is accomplished by
a launch of a *netcat* server specifying a listening port in our bash.

The next step is to follow these command lines and you should be good to go.

### 1) Check that we have the connection established. Running the *whoami* command should return the hostname.
```bash
whoami
```
### 2) Launch an interactive bash (a pseudo console).

```bash
script /dev/null -c bash
```

### 3) Send the process that is running to the background.

```bash
[CTRL + Z]
```

### 4) Resume the process previously left in the background (3)

```bash
stty raw -echo; fg
```

### 5) Restart the current configuration of the terminal (after this step we should be able to operate the external terminal more comfortably).

```bash
reset xterm
```

### 6) We export an Xterm terminal

```bash
export TERM=xterm
```

### 7) We export a bash

```bash
export SHELL=bash
```

### 8) Change the resolution of our interactive bash. Note: To check the number of current rows and columns run -> stty size.
```bash
stty rows 51 columns 189
```

### 9) Restart the current terminal configuration again.
```bash
reset xterm
```

