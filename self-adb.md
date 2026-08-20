# Connect your own phone to ADB

## Requires wireless debugging functionality, may not be available on some older phones.

1. Enable Wireless Debugging

```
Settings > Developer Options > Wireless Debugging > Toggle ON
```

2. Pair with Pairing Code

```
Tap "Pair device with pairing code"
Note the IP:PORT and pairing code shown
```

3. Pair in Termux

```bash
adb pair 192.168.x.x:PORT
```

Example:

```bash
adb pair 192.168.1.100:37181
```

Enter the pairing code when prompted.

4. Connect

```bash
adb connect 192.168.x.x:PORT
```

Note: This is the connection port (usually 5555 or similar), NOT the pairing port.

Example:

```bash
adb connect 192.168.1.100:5555
```

5. Verify

```bash
adb devices
```

## Pairing is one-time

The next time, just turn on wireless debugging and do adb connect ip:port, it should work.

## Common Problem

When you leave Settings app to enter Pairing port in Termux, it sometimes kills the pairing prompt. I work around this by opening Settings AND Termux both in split-screen then doing it. If you know any other solutions, you could recommend them.

###ADB will definitely not be as powerful as it would have been from an actual computer.