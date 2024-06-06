# Distrobox on Crostini

## Step 1: Set up UIDs and GIDs for rootless podman

Open terminal (penguin) and run
```
sudo apt install uidmap podman -y
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

## Alternatively, here are the docker instructions:

Open terminal (penguin) and run
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
After this, run 
```
sudo groupadd docker && sudo usermod -aG docker $USER
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Finally, right click terminal in your taskbar and select power off.
After this, proceed to [Step 2](https://github.com/upperint/Distrobox_on_Crostini?tab=readme-ov-file#step-2-install-distrobox)

## Setting up Docker's registries in Podman

Use your favourite editor and open /etc/containers/registries.conf

Now change `## unqualified-search-registries = ["example.com]`

to `unqualified-search-registries = ["docker.io"]`

After this, you can now pull Docker images with Podman.

## Foreign architecture support (Podman only)

Open crosh again (**ctrl + alt + t**)

Now run
```
vmc container termina penguin --privileged true
```
```
sudo apt install qemu-user-static binfmt-support
```
and close crosh.

Finally, right click terminal in your taskbar and select power off.
