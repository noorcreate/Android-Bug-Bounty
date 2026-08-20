# Termux Setup

My Bash Start-up script, this script runs the moment you open a new terminal session in Termux.

```
cat ~/.bashrc
``` 

to check it, and to edit it.

```
nano ~/.bashrc
```

Nano is a pretty bad text editor, you can use micro, or if you're a madman you could use vim or neovim. You could search for other Termux-friendly text editors.

Here's my bashrc

```
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$PATH
alias cu="curl -i -L "
alias local='python -m http.server 8000 & am start -a android.intent.action.VIEW -d http://localhost:8000'
alias py="python3"
alias serv='python -m http.server 8000'
cd /storage/emulated/0/A.Termux/
export GIT_DISCOVERY_ACROSS_FILESYSTEM=1
alias gp='git add . && git commit -m "update" && git push'
alias pu="git pull --rebase"
```

The first two exports make sure your Go tools are working correctly.

The "cu" is for sending a basic curl command with headers and redirect follow to any url.

```
cu https://example.com
```

The "local" alias immediately starts a server (serves the directory the command was run in) at localhost 8000 and immediately opens it in your default browser.

The "serv" alias also does the same thing, but doesn't open in your browser.

The "py" alias is also for shortening python3 python.py into py python.py (You know it's annoying to type in mobile)

The cd command immediately takes you to a directory of your choice as soon as you start Termux, this is because accessing Termux home directory "~\" from file managers is sometimes a bit tricky, this is why I keep most of my stuff in a normal folder easily accessible from file managers.

The other commands are basically for GitHub, though I barely use GitHub from the CLI. 

## If it wasn't pretty obvious, I'm bad at coding.

# Packages 

## pkg install
```bash
pkg install -y git curl wget nmap apktool aapt2 openjdk-21 android-tools \
  python python-pip nodejs golang clang make nano jq dnsutils \
  proxychains-ng tor openssh ffmpeg exiftool pdftk proot-distro
```

## Go tools (security)
```bash
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install github.com/projectdiscovery/httpx/cmd/httpx@latest
go install github.com/projectdiscovery/katana/cmd/katana@latest
go install github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
go install github.com/lc/gau/v2/cmd/gau@latest
go install github.com/tomnomnom/waybackurls@latest
go install github.com/tomnomnom/gf@latest
go install github.com/ffuf/ffuf/v2@latest
```

## pip install
```bash
pip install mitmproxy flask requests beautifulsoup4 uro \
  jsbeautifier
```

## Notable tools
- `apktool` + `aapt2` + `openjdk-21` — APK decompile/recompile
- `android-tools` — adb for device interaction
- `mitmproxy` — traffic interception with custom addon
- `android-unpinner` — cert pinning bypass
- `proxychains-ng` + `tor` — anonymization if needed
- `exiftool` — metadata extraction from files
- `ffuf` — web fuzzing
- `uro` — URL deduplication


Note: Some of these, especially mitmproxy will NOT properly install in the first try. I recommend you to install them one by one. And if facing any errors in any of these packages, consult the errors with Claude, because they definitely installed fine for me after bashing my head for a while.


# Useful Commands

Termux System Management Commands

---

System Management

Clean All Caches

```bash
pkg clean && pip cache purge && go clean -cache -modcache -testcache
```

Clears package manager cache, pip cache, and Go module cache all at once. Use when storage is running low.

Check Storage Usage

```bash
du -sh ~/* ~/.??* | sort -h | head -20
```

Shows the 20 largest files/directories in your Termux home directory, including hidden ones. Useful for identifying what's taking up space.

Find Large Files

```bash
find ~ -type f -size +50M 2>/dev/null -exec ls -lh {} \; | sort -k5 -h
```

Locates all files larger than 50MB in your Termux directory and sorts them by size. Helps identify space-hogging files.

Kill Process Using Port

```bash
fuser -k -n tcp 8080
```

Terminates any process listening on a specific TCP port. Replace 8080 with the port you want to free up.

---

Process Management

List All Processes

```bash
ps aux | grep -v grep
```

Shows all running processes without showing the grep command itself in the output.

```bash
kill -9 <PID>
```
Kill any process from Process ID, (get PID from ps aux)

Top Memory Consumers

```bash
ps aux --sort=-%mem | head -20
```

Displays the top 20 processes using the most memory. Great for identifying memory-hogging apps.

Top CPU Consumers

```bash
ps aux --sort=-%cpu | head -20
```

Shows the top 20 processes consuming the most CPU resources. Useful for performance troubleshooting.

Kill by Process Name

```bash
pkill -f process_name
```

Kills all processes matching the given name pattern. Use with caution as it will terminate matching processes immediately.

---

Network Tools

Get Public IP

```bash
curl -s ifconfig.me
```

Fetches your external/public IP address from ifconfig.me service.

Test Connectivity

```bash
ping -c 4 8.8.8.8
```

Sends 4 ICMP echo requests to Google's DNS server. Use to check if you have internet connectivity.

---