# Pre-compiled CCMiner for Termux:
This is a WIP repo for pre-compiled ccminer binaries with latest Termux(v0.118.0) and latest Clang(v17.0.6).

# **`Disclaimer: I accept no warranties or liabilities on this repo. Do it at your own risk!!!`**

# **`This is for any ARMv8 device`**

# **`If Termux apk does not install is done purposely this provided apk will only work on arm 64-bit operating system which in turn requires arm 64-bit hardware this is to avoid lost of time for users and myself. (Mining on 32-bit devices is not profitable)`**

# Installation:
1. Download & install latest arm64-v8a [Termux](https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_arm64-v8a.apk):
```
https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_arm64-v8a.apk
```
2. Get Termux ready:
- Type `y` then enter key in any prompts!
```
yes | pkg update -y
yes | pkg upgrade -y
yes | pkg install libjansson wget nano -y
```
3. Download ccminer, config, start:
```
mkdir ccminer && cd ccminer
wget https://raw.githubusercontent.com/Sabas31/pre-compiled/generic/ccminer
wget https://raw.githubusercontent.com/Sabas31/pre-compiled/generic/config.json
wget https://raw.githubusercontent.com/Sabas31/pre-compiled/generic/start.sh
chmod +x ccminer start.sh
cp ./ccminer ../../usr/bin/start.sh
```
# Usage:

1. Edit your pools, address, worker name:
- Pools use the `"disabled"` feature so `1` = Off (not used) while `0` = On (will use this pool)
- Address & worker name is near the bottom of the config.json in format `address here.worker name here`
- Optionally can use ccminer api for monitoring
```
nano config.json
```
2. Start ccminer with:
```
~/ccminer/start.sh
```
3. Close ccminer with:
```
CTRL + c
```
Create boot directory & setting termux properties
```
mkdir ~/.termux/boot
```

```
nano ~/.termux/termux.properties
```

Create script auto start termux and running verus mining.
```
nano ~/.termux/boot/start-verus
```

```
am startservice --user 0 -n com.termux/com.termux.app.RunCommandService \
-a com.termux.RUN_COMMAND \
--es com.termux.RUN_COMMAND_PATH '/data/data/com.termux/files/home/ccminer/start.sh' \
--esa com.termux.RUN_COMMAND_ARGUMENTS '-n,5' \
--es com.termux.RUN_COMMAND_WORKDIR '/data/data/com.termux/files/home' \
--ez com.termux.RUN_COMMAND_BACKGROUND 'false' \
--es com.termux.RUN_COMMAND_SESSION_ACTION '1'
```

```
#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
```
```
chmod +x ~/.termux/boot/start-verus
```


```
echo "/data/data/com.termux/files/home/ccminer/start.sh" >> ~/.bashrc
echo "termux-wake-lock" >> ~/.bashrc
```
