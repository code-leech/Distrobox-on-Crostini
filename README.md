# Welcome to a simple tutorial which is (hopefully) useful to you!
This is a tutorial for Chromebook users to install Distrobox and Podman to try different Distros.

## Install Podman

Firstly, set up linux in **Developer Options** and select **Setup up linux**. 
Then, open *Penguin* in the terminal options.
Now run these commands:
```
sudo apt update -y
sudo apt install uidmap
```
**Now close the terminal.**
Open **CROSH** by pressing *ctrl + alt + t*

Once opened, run these commands one by one. 
```
vsh termina
```
```
lxc exec penguin -- /bin/sh -c "printf '%s\n' '1000:100000:65536' | tee /etc/subuid /etc/subgid"
```
```
lxc restart penguin
```
```
exit
```
After this, run these commands also.
```
vmc container termina penguin --privileged true
```
```
sudo apt install podman
podman system migrate
```
Now, check if the assigned GIDs and UIDs are correct.
```
cat /etc/subuid /etc/subgid
```

The outputs should read

*1000:100000:65536*

*1000:100000:65536*

## Install Distrobox

Copy the whole box and run it all:
```
mkdir ~/.local/bin
PATH=$PATH:~/.local/bin
git clone https://github.com/89luca89/distrobox.git
cd distrobox
./install
```
Now close **CROSH**

## Final step...

Just restart *penguin* by right clicking terminal in taskbar and selecting **Shut down linux** then opening terminal again and selecting *penguin*

There we go, Distrobox + Podman has been installed on your computer. Enjoy!
