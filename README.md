# Distrobox on Crostini

## Step 1: Set up UIDs and GIDs for rootless podman

Open terminal (penguin) and run
```
sudo apt install uidmap podman-y
```
Now close terminal and execute **ctrl + alt + t**

After this run the following commands:
```
vsh termina
```
```
lxc exec penguin -- /bin/sh -c "printf '%s\n' '1000:100000:65536' | tee /etc/subuid /etc/subgid"
```
After this close the window and open terminal again.

## Step 2: Install Distrobox

Everything here can be condensed into one command:
```
mkdir ~/.local
mkdir ~/.local/bin
PATH=$PATH:~/.local/bin
git clone https://github.com/89luca89/distrobox.git
cd distrobox
./install
```
After this, you can now use Distrobox on your chromebook!
