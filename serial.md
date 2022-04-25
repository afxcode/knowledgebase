## Create serial pipe
* create serial file 
```bash
$ touch $HOME/dev/ttyV0
```
* point serial pipe to ceated file 
```bash
$ socat pty,link=$HOME/dev/ttyV0,waitslave tcp:10.3.2.40:1701
```
## Monitor serial (read)
* you can use minicom for monitoring 
```bash 
$ minicom -D $HOME/dev/ttyV0
```
## Send command
* you can use arrow to send command 
```bash 
$ echo "read wt0101 wt0103" > $HOME/dev/ttyV0
```
