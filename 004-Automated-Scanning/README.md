# Automated Scanning
While running tools such as `strings` and `otool` are very useful in our quest to understand the inner-workings of an app from an attackers perspective, we have some excellent automated solutions available to us that can be plugged directly to our pipeline and SDLC. One of those tools is [MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF).

Mobile Security Framework is an automated, all-in-one mobile application (Android/iOS/Windows) pen-testing framework capable of performing static analysis, dynamic analysis, malware analysis and web API testing. 

Head over to the Santoku VM that is running and open up the terminal. MobSF has the ability to run in Docker which is what we will use for this lab. Run the following two commands in the Santoku Linux VM:

```
sudo docker pull opensecurity/mobile-security-framework-mobsf
sudo docker run -it -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

Now open up Firefox or Chromium in the VM and go to the following URL:
```
http://localhost:8000
```

This will open the MobSF web UI. From here, we can start analyzing our IPA files. MobSF handles things like running `strings` and performing dynamic analysis for us. Tools like these are being run against your iOS applications constantly looking for issues.

Choose one of the .ipa files located in the lab repo that was cloned earlier on the VM to run a scan on it and read the results. 

Find anything interesting?

## Discussion Question
How would you plug a tool like this into your current CI/CD pipeline?