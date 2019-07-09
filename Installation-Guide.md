Dunner can be installed using various options on each platform:

* [Download precompiled binary](https://github.com/leopardslab/dunner/wiki/Installation-Guide/_edit#1-install-on-all-platforms) - all platforms
* Package Managers
  - [Linux](https://github.com/leopardslab/dunner/wiki/Installation-Guide/_edit#2-install-on-linux)
  - [Max OS X](https://github.com/leopardslab/dunner/wiki/Installation-Guide/_edit#2-install-on-mac-os-x)
* [Install from source code](https://github.com/leopardslab/dunner/wiki/Installation-Guide#3-install-from-source-code)

# 1. Install on all Platforms

### 1. Download binary

Download the suitable tar file from [Github Releases page](https://github.com/leopardslab/Dunner/releases/) based on your OS and architecture type. 
Extract the file as below:
```
tar -xvzf <path_to_downloaded_tar_file>
```
This extracts the `dunner` binary which can be added to `$PATH` environment variable.

# 2. Install on Linux

Dunner can be installed on any flavour of Linux using the below methods:

### 1. Debian/Apt

For the first time use, add Dunner's GPG Key and also add Dunner to the `apt` repository list using below commands.
```
apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-keys 379CE192D401AB61
echo "deb https://dl.bintray.com/leopardslab/dunner-deb stable main" | tee -a /etc/apt/sources.list
```

Finally, install Dunner as:
```
sudo apt-get update
sudo apt-get install dunner
```

Note: In some Linux images, you might need to run `apt update && apt install ca-certificates gnupg2` to add gpg key.

### 2. Snapcraft

```
snap install dunner
```

### 3. Download .deb/.rpm
Download the .deb or .rpm from [Github Releases page](https://github.com/leopardslab/Dunner/releases/) and install with `dpkg -i` and `rpm -i` respectively.

### 4. Install using YUM/DNF

For the first time, add Dunner to yum repository list by running below commands:
```
wget https://bintray.com/leopardslab/dunner-rpm/rpm -O bintray-leopardslab-dunner-rpm.repo 
sudo mv bintray-leopardslab-dunner-rpm.repo /etc/yum.repos.d/
```

Then install dunner as:

```
sudo dnf update
sudo dnf install dunner
```

# 2. Install on Mac OS X
[Dunner](https://github.com/leopardslab/Dunner) can be installed via [Homebrew](https://brew.sh/). On Mac OS X, you can install by running below command:

```
brew tap leopardslab/dunner
```
or
```
brew install leopardslab/homebrew-dunner/dunner
```

To reinstall, run `brew reinstall dunner`.

# 3. Install on Arch Linux
[[Refer this](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages)]
Clone the AUR package repository,
```bash
git clone https://aur.archlinux.org/dunner.git
cd dunner/
```
Use `makepkg` to build the `PKGBUILD` file and install Dunner
```bash
makepkg -si
```

# 4. Install from source code

**Note**: You need 'Dep' to download the dependencies. See how to install Dep [here](https://golang.github.io/dep/docs/installation.html).

1. Run `dep ensure` to download all the dependencies of Dunner.

2. Run `go install` to install Dunner on your machine.

Now you can use `dunner` like `dunner do <taskname>`

***

**Note:** We will be adding more methods like RPM & Deb packages in the future
