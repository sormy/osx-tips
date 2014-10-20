
# Tun/tap kernel driver for Mac OS X.

Yosemite compatible instruction.

Need homebrew installed.

Install tuntap:
<pre>
brew install tuntap
</pre>

Disregard post installation instructions from homwbrew and use instead:
```
sudo cp -pR /usr/local/Cellar/tuntap/20111101/Library/Extensions/tap.kext /Library/Extensions
sudo cp -pR /usr/local/Cellar/tuntap/20111101/Library/Extensions/tun.kext /Library/Extensions
sudo chown -R root:wheel /Library/Extensions/tap.kext
sudo chown -R root:wheel /Library/Extensions/tun.kext
sudo touch /Library/Extensions
sudo nano /Library/LaunchDaemons/tun.plist # use content below
sudo nano /Library/LaunchDaemons/tap.plist # use content below
launchctl load -w /Library/LaunchDaemons/tun.plist
launchctl load -w /Library/LaunchDaemons/tap.plist
sudo nvram boot-args="kext-dev-mode=1" # allow to load unsigned extensions in yosemite, reboot required
```

`/Library/LaunchDaemons/tun.plist`:
```
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
        <key>KeepAlive</key>
        <false/>
        <key>Label</key>
        <string>tun</string>
        <key>ProgramArguments</key>
        <array>
                <string>/sbin/kextload</string>
                <string>/Library/Extensions/tun.kext</string>
        </array>
        <key>RunAtLoad</key>
        <true/>
        <key>StandardErrorPath</key>
        <string>/dev/null</string>
        <key>StandardOutPath</key>
        <string>/dev/null</string>
        <key>UserName</key>
        <string>root</string>
</dict>
</plist>
```

`/Library/LaunchDaemons/tap.plist`:
```
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
        <key>KeepAlive</key>
        <false/>
        <key>Label</key>
        <string>tap</string>
        <key>ProgramArguments</key>
        <array>
                <string>/sbin/kextload</string>
                <string>/Library/Extensions/tap.kext</string>
        </array>
        <key>RunAtLoad</key>
        <true/>
        <key>StandardErrorPath</key>
        <string>/dev/null</string>
        <key>StandardOutPath</key>
        <string>/dev/null</string>
        <key>UserName</key>
        <string>root</string>
</dict>
</plist>
```
