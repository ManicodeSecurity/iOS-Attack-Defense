# Insecure Data Storage

## Storing Sensitive Data in NSUserDefaults

A common method of saving data in iOS applications is utilizing `NSUserDefaults`. This data persists even if the application itself is closed. Data stored in `NSUserDefaults` is not encrypted and can easily be retrieved in the application bundle. 

### Step 1: Open the DVIA Lab
Using the iOS Simulator, navigate to the DVIA app. Open the menu and go to `Local Data Storage` and select `UserDefaults`.

Enter some dummy data in the text field.

### Step 2: Retrieve the Info in the NSUserDefaults Plist File
We can now retrieve the data that we stored in `NSUserDefaults` by using `grep` to find the appropriate plist file:

```
cd ~/Library/Developer/CoreSimulator/Devices
find . | grep DVIAswiftv2.plist

# We now cat the plist file. Yours will look different!
cat ./D0461942-D7D7-4EC8-8C94-5E6D4CDF6C28/data/Containers/Data/Application/BF64C8E3-915B-4414-85DB-4ADB2D5C7037/Library/Preferences/com.highaltitudehacks.DVIAswiftv2.plist
```

## Storing Sensitive Data in Plist Files
Another common way of storing data is directly in plist files. Plist files are an acceptable place to store information that is not confidential. Plist files are unencrypted and can be easily be fetched even from a non-jailbroken device. 

### Step 1: Open the DVIA Lab
Using the iOS Simulator, navigate to the DVIA app. Open the menu and go to `Local Data Storage` and select `Plist`.

Now, enter some dummy "sensitive data" in the fields. 

### Step 2: Retrieve the Info in the Plist File
We can now retrieve the .plist file on our local machine. Open up a new terminal window on your laptop and run the following commands:
```
# Go to the directory with our local devices
cd ~/Library/Developer/CoreSimulator/Devices

# We need to find the correct device that contains the plist file
find . | grep userInfo.plist

# Now we can cat the plist file (below is an example, please replace with your correct path from the above command)
cat ./D0461942-D7D7-4EC8-8C94-5E6D4CDF6C28/data/Containers/Data/Application/BF64C8E3-915B-4414-85DB-4ADB2D5C7037/Documents/userInfo.plist
```

## Snapshot Data Storage

One of the features in iOS to make it seem like apps load more seamlessly is the Snapshot feature. iOS will take a screenshot of the application in its current state when it is placed in the background. That screenshot is displayed when the app is brought to the foreground as the app loads. This makes the experience seem instant. Snapshots should never contain sensitive information as they are accessible in the application's bundle. 

Open up the DVIA app in the simulator and under the `Sidechannel Data Leakage` menu, select `App Screenshot`.

Enter a fake answer in the "security question" box and background the application by hitting the home button in the simulator.

Open up your terminal and view the Snapshot that was taken by running the following commands:
```
# Your path will have different IDs, find the directory from the path to userInfo.plist. You want the parent directory of "/Documents/".
cd ~/Library/Developer/CoreSimulator/Devices/D0461942-D7D7-4EC8-8C94-5E6D4CDF6C28/data/Containers/Data/Application/BF64C8E3-915B-4414-85DB-4ADB2D5C7037/Library/Caches/Snapshots/com.highaltitudehacks.DVIAswiftv2

# The Snapshot is stored as a ktx image file
open 7C163A44-F2D7-4B55-BC09-C5CB45EE34AD@3x.ktx
```

## SQLite Files

In the directory `/sqlite` of this lab you will find the SQLite database that was used in a previous version of the United MileagePlus iOS application. This file was retrieved from an iTunes backup. Feel free to explore it using the `sqlite3` command line utility. 
