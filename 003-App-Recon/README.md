# iOS App Recon
The goal of this lab is to discover everything that we can just from what is publicly and easily available to us as researchers (the .ipa file). For this lab we will use the unzipped .ipa file from `002-Exploring-IPA`. 

In a terminal on your local machine, `cd` into the directory `/002-Exploring-IPA/Payload/DVIA-v2.app`

### Task 1: Inspect Info.plist
We will first take a look at the `Info.plist` file to look for sensitive information and gather more intel about the app.

The `Info.plist` file is often in binary format. Run the following command to convert it:

```
plutil -convert xml1 Info.plist
```

Now we can search for data in the file using a simple `cat` command. The following will tell us if the app has the `NSAllowsArbitraryLoads` config set to `true`. Remember, this means that the app is configured to allow content to be loaded over non-encrypted connections.

```
cat Info.plist
cat Info.plist | grep -A1 NSAllowsArbitraryLoads
```

### Discussion Question
What else can we look for in the `Info.plist` file to understand more about the application?

### Task 2: Run Strings
Strings will help us discover hardcoded credentials, URLs, keys, and more. It is a simple tool that is used as the first step in recon of an app. Below are some simple examples. Feel free to experiment further.

We run `strings` on the Mach-O executable called `DVIA-v2` located in the `/002-Exploring-IPA/Payload/DVIA-v2.app` directory:

```
strings DVIA-v2 | egrep -i 'http|https'
strings DVIA-v2 | egrep 'key'
strings DVIA-v2 | egrep 'password'

```

### Task 3: Run otool

`otool` allows us to view the load commands in the Mach-O executable file included in our application's bundle. `otool` is built into OSX. 

IPA files that are from the official iOS App Store are encrypted by default. We can use `otool` to verify if our Mach-O executable is encrypted or not using the following command. This will be run in the same directory as Task 2:

```
otool -l DVIA-v2 | grep -i crypt
```
The output should have a field called `cryptid`. If it equals 1 the binary is encrypted, if it is 0, it is not.

Another handy use of otool is to identify all of the linked libraries associated with the binary. These libraries are a good place to start when mapping out the application attack surface and functionality. The following command will display the linked libraries in our binary:

```
otool -L DVIA-v2
```

For those who are literate in assembly code, we can also use `otool` to disassemble the app into assembly language (this will also make your terminal look like you are doing some 1337 hax):

```
otool -tV DVIA-v2
```
