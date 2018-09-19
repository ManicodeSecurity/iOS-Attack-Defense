
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

We will compile the DVIA source code using Xcode. In the `DVIA-v2` directory you will see a file called `DVIA-v2.xcworkspace`. Open this file in Xcode to start exploring the application and run the emulator.

### Task 3: Build and Explore the Application 

In the upper navigation bar of Xcode, click the button with the triangle to compile the application. This will open the app up in the Simulator. Click around and take a look at some of the challenges that come with DVIA.


### Task 4: Santoku Linux Setup
[Santoku Linux](https://santoku-linux.com/) is an open-source virtual machine that comes pre-installed with a number of useful tools needed for mobile security testing, malware analysis, and mobile forensics. 

If you have not already downloaded the .ISO file, please do so now. 

Please follow the directions outlined in the official [Santoku Linux Documentation](https://santoku-linux.com/howto/installing-santoku/installing-santoku-in-a-virtual-machine/) to complete the setup in VirtualBox.

*! Important !* Please ensure VirtualBox Guest additions is installed per the instructions.

### Task 5: Install Docker in the VM
We will need to use [Docker](https://www.docker.com/) to run some tools in our VM. Below is how we install it in this Ubuntu VM:


```
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


