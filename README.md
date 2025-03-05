## iOS Activation Bypass Instructions for A7 Devices ##
### Confirmed Working Devices ###

- iOS 12.5.7
  - iPad Air 1st Gen
  
### Jailbreak the iDevice ###
- Jailbreak with Checkra1n 0.10.2 
  - https://checkra.in/releases/0.10.2-beta#all-downloads
- Alternatively use Bootra1n 10.2
  - https://github.com/foxlet/bootra1n
- This can be a VERY finicky process with freezing at the 'Right Before Trigger (this is the real bug setup)'.  
  - Unplug the iDevice after ~15-20 seconds of the screen showing 'Right Before Trigger...' then plug the iDevice back in after 1-2 seconds.  You should see a 'Booting Up' message immediately after plugging the device back in.  If you don't you'll likely have to start all over with checkra!n.  If you keep failing you can try and restore the iOS firmware in iTunes and start over again.

### Bypass iCloud Activation ###

- Start iProxy
  ```
  .\iproxy.exe 22 44
  ```
  - 22 is the local masquerade port
  - 44 is the port SSH is running on on the iDevice (SSH on the iDevice is 44 per Checkra1n docs)

- Open a second shell
- Type: **ssh root@127.0.0.1**
  - Password: **alpine**

- On the iDevice, continue to the 'Chose a Wi-Fi Netowrk' screen but **DO NOT** connect

- In the SSH Powershell console enter the following commands in order:
    ```
    mount -o rw,union,update /
    launchctl unload /System/Library/LaunchDaemons/com.apple.mobileactivationd.plist
    rm /usr/libexec/mobileactivationd
    uicache --all
    ```
- On your pc do: xxd -p mobileactivationd mbact.hex
- Open mbact.hex, copy every single line to clipboard
- In the ipad SSH Console go to /usr/libexec/ and do vi mbact.hex
- Paste everything and do :wq
- After that, enter the command xxd -r -p mbact.hex mobileactivationd
  
- Once complete enter the following commands in order:
    ```
    chmod 755 /usr/libexec/mobileactivationd
    launchctl load /System/Library/LaunchDaemons/com.apple.mobileactivationd.plist
    ```
    
- Finally chose 'Connect to iTunes' on the bottom of the 'Chose a Wi-Fi Network' page to complete bypass
 
 
  
<sub> These directions were pulled from many sources and compiled by me, the steps and patched mobileactivationd file for the iCloud bypass were extracted from [iOS-Hacktivation](https://github.com/Hacktivation/iOS-Hacktivation-Toolkit/tree/master/bypass_scripts/mobileactivationd_12_4_7).  Many thanks to the talented individuals that create these tools! </sub>
