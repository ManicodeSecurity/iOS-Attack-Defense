# Recon
The goal of this lab is to discover everything that we can just from what is publicly and easily available to us as researchers (the .ipa file). 

### Task 1: Inspect Info.plist
We will first take a look at the `Info.plist` file to look for sensitive information and gather more intel about the app.

The `Info.plist` file is often in binary format. Run the following command to convert it:
```
plutil -convert xml1 Info.plist
```

Now we can search for data in the file using a simple `cat` command. The following will tell us if the app has the `NSAllowsArbitraryLoads` config set to `true`. Remember, this means that the app is configured to allow content to be loaded over non-encrypted connections.

```
cat Info.plist | grep NSAllowsArbitraryLoads -A1
```

### Discussion Question
What else can we look for in the `Info.plist` file to understand more about the application?

### Task 2: Run Strings
Strings will help us discover hardcoded credentials, URLs, keys, and more. It is a simple tool that is used as the first step in recon of an app. Below are some simple examples. Feel free to experiment further.

```
strings <IPA_FILE> | egrep -i 'http|https'
strings <IPA_FILE> | egrep 'key'
strings <IPA_FILE> | egrep 'password'

```

### Task 3: Run otool

`otool` allows us to view the load commands in the Mach-O executable file included in our application's bundle. `otool` is built into OSX. 

IPA files that are from the official iOS App Store are encrypted by default. We can use `otool` to verify if our Mach-O executable is encrypted or not using the following command:

```
otool -l <IPA_NAME> | grep -i crypt
```
The output should have a field called `cryptid`. If it equals 1 the binary is encrypted, if it is 0, it is not.

Another handy use of otool is to identify all of the linked libraries associated with the binary. These libraries are a good place to start when mapping out the application attack surface and functionality. The following command will display the linked libraries in our binary:

```
otool -L <IPA_NAME>
```

For those who are literate in assembly code, we can also use `otool` to disassemble the app into assembly language (this will also make your terminal look like you are doing some 1337 hax):

```
otool -tV <IPA_NAME>
```
