# mitmproxy and Proxy setup

https://github.com/theappbusiness/android-proxy-toggle

Download and set this app up, this allows you to easily turn on/off proxy for mitmproxy.



# Mitmproxy Setup

```
pip install mitmproxy
```

## Common Issues

Failed building wheel for cryptography

```
pkg install rust binutils
pip install --upgrade cryptography
pip install mitmproxy
```

Couldn't find module OpenSSL

```
pkg install openssl
pip install mitmproxy
```

If other issues, copy-paste the error to someone more useful than me (AI)

---

# Why mitmproxy?

mitmproxy has three different modes.
1. mitmproxy - Basic CLI https inspection.
2. mitmweb - (Ugly) Web-based UI for https inspection in localhost
3. mitmdump (love of my life) - Scriptable proxy engine, se can build anything on top of it. 


# Basic Setup

Extract mitm.zip in a directory, then go into that directory.

Set your proxy to 127.0.0.1:8080

Run "mitmdump -s addon.py"

Visit 127.0.0.1:8082/index.html (The script serves GUI on port 8082)

And it should be capturing your traffic, allowing you to edit them, intercept them, save responses and requests, etc.

### This is very bare bones, I'm sure my script is only the tip of what mitmdump can do, if you're actually a proficient programmer unlike me, feel free to run through their docs and create something even better of your own.


