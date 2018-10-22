# Lab Setup

The goal of this lab is to successfully prepare your environment for the remainder of the labs. We will be using a variety of technologies including 

### Requirements
- VirtualBox
- Santoku Linux Virtual Machine
- Xcode installed on your local machine

### Task 1: Clone This Repository
On your local machine in an easy-to-find location (such as the Desktop) run the following command:
```
git clone https://github.com/ManicodeSecurity/iOS-Attack-Defense
```

### Task 2: Download and Install DVIA 
[Damn Vulnerable iOS Application](http://damnvulnerableiosapp.com/) is an intentionally insecure iOS application built to help students and researchers learn about iOS security in a legal environment. It was built by [@prateekg147](http://twitter.com/prateekg147) as free and open source software. We will use DVIA extensively throughout the course. 

Everything needed to install DVIA is located in the `DVIA-v2` directory of this lab. 

First we need to install some dependencies. In the `/DVIA-v2/DVIA-v2` directory you will see a `Podfile`. In this directory, run the following command:

```
pod update
pod install
```

If you do not have `cocoapods` installed please use the following command:
```
sudo gem install cocoapods
```

We will compile the DVIA source code using Xcode. In the `DVIA-v2` directory you will see a file called `DVIA-v2.xcworkspace`. Open this file in Xcode to start exploring the application and run the emulator.

Xcode may prompt you to install additional components, please follow the prompts to install these before continuing. 

### Task 3: Build and Explore the Application 

In the upper navigation bar of Xcode, click the button with the triangle to compile the application. This will open the app up in the Simulator. Click around and take a look at some of the challenges that come with DVIA.

If you are running Xcode 10 the build will likely fail. If you ran a build already and it failed first we need to clear your project with `cmd+shift+k`.

Next we tell Xcode to use the `Legacy Build System` as follows:

```
In Xcode, go to File->Project/Workspace settings

Change the Build System to "Legacy Build System" in both "Shared Workspace Settings as well as "Per-User Workspace Settings".

While you are still in the Workspace Settings dialog, you will need to delete Derived Data. This can be done by clicking the little grey arrow under Derived data section of the page then selecting your project folder called "DerivedData" and moving it to the trash.
```

### Task 4: Santoku Linux Setup
[Santoku Linux](https://santoku-linux.com/) is an open-source virtual machine that comes pre-installed with a number of useful tools needed for mobile security testing, malware analysis, and mobile forensics. 

If you have not already downloaded the .ISO file, please do so now. 

Please follow the directions outlined in the official [Santoku Linux Documentation](https://santoku-linux.com/howto/installing-santoku/installing-santoku-in-a-virtual-machine/) to complete the setup in VirtualBox.

*! Important !* Please ensure VirtualBox Guest additions is installed per the instructions.

### Task 5: Install Docker in the VM
We will need to use [Docker](https://www.docker.com/) to run some tools in our VM. Below is how we install it in this Ubuntu VM:


```
# The following should be run in the Santoku VM - NOT on your local machine
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

sudo apt-get install docker-ce
```

Ensure Docker is installed and running:
```
sudo docker images
```

### Task 6: Clone This Repo in the VM

To avoid setting up shared folders in VirtualBox, we will just simply clone the repo in the Santoku VM. Open a terminal in the VM and run the following commands:

```
cd ~/Desktop

git clone https://github.com/ManicodeSecurity/iOS-Attack-Defense
```


