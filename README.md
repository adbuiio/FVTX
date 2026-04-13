# Python Tools

A collection of Python tools for PC and mobile.

## Usage:


### Requirements
- Make sure your phone and computer are on the **same WiFi network**.
- Both devices need **Python 3.7+** installed.

### Mode 1: Phone as Server (Recommended)
Best for: Phone sends files to PC, or PC browses files on phone.

**1. On your phone, run:**
```bash
python FVTX-M-1.2-MAIN.py
```

**2. Choose `1` (Server mode):**
```
1. Server mode (PC connects to me)
2. Client mode (I connect to PC)
Choose [1/2]: 1
```

**3. The phone will display its IP address, for example:**
```
[*] Connect from PC: 192.168.1.100:8765
```

**4. On your computer, open a terminal and connect using `netcat` (or telnet):**
```bash
nc 192.168.1.100 8765
```

**5. Once connected, you can use these commands:**

| Command | Description | Example |
|---------|-------------|---------|
| `LIST:<path>` | List directory contents | `LIST:/sdcard/Download` |
| `PREVIEW:<file>` | Preview first 5000 bytes of a file | `PREVIEW:/sdcard/note.txt` |
| `DOWNLOAD:<file>` | Download a file (netcat will save raw data) | `DOWNLOAD:/sdcard/photo.jpg` |
| `UPLOAD:<path>` | Upload a file to phone | `UPLOAD:/sdcard/newfile.txt` |
| `EXIT` | Disconnect | `EXIT` |

>  **Tip for netcat users**: After `DOWNLOAD`, the raw file data will print to your terminal. Use output redirection: `nc 192.168.1.100 8765 > received_file.jpg`

---

### Mode 2: PC as Server
Best for: Phone downloads files from PC, or PC sends files to phone.

**1. On your computer, run the script:**
```bash
python FVTX-M-1.2-MAIN.py
```

**2. Choose `1` (Server mode). Note the IP address displayed.**

**3. On your phone, run the script and choose `2` (Client mode):**
```
1. Server mode (PC connects to me)
2. Client mode (I connect to PC)
Choose [1/2]: 2
```

**4. Enter your computer's IP and port:**
```
Computer IP: 192.168.1.50
Port (default 8765): 
```

**5. Once connected, use these commands in the phone terminal:**

| Command | Description | Example |
|---------|-------------|---------|
| `ls <path>` | List directory | `ls C:\Users\YourName\Desktop` |
| `preview <file>` | Preview file | `preview C:\file.txt` |
| `download <remote> <local>` | Download from PC to phone | `download C:\photo.jpg /sdcard/photo.jpg` |
| `upload <local> <remote>` | Upload from phone to PC | `upload /sdcard/test.txt C:\received.txt` |
| `exit` | Disconnect | `exit` |

---

### Troubleshooting

| Problem | Solution |
|---------|----------|
| `Connection refused` | Make sure the server is running first, and check the IP and port |
| `Connection timeout` | Verify both devices are on the same WiFi and no firewall is blocking port 8765 |
| `ERROR: Path not found` | Use absolute paths (e.g., `/sdcard/` on Android, `C:\Users\...` on Windows) |
| `Preview shows garbled text` | The file might be binary (image, video). Preview works best for text files |

---

### Running on Android (Termux)

1. Install Termux from F-Droid (not Google Play, it's outdated)
2. Install Python: `pkg install python`
3. Transfer the script to your phone or clone the repo:
   ```bash
   git clone https://github.com/adbuiio/FVTX.git
   cd FVTX
   ```
4. Run the script: `python FVTX-M-1.2-MAIN.py`

>  **Note for Android users**: Access to `/sdcard/` may require storage permission. In Termux, run `termux-setup-storage` first.

## Requirements

- Python 3.7+

## License

This project is licensed under the **MIT License**. See [LICENSE.md](LICENSE.md) for details.

Original code copyright (c) 2024 adbuiio.

If you use this code in your project, please include the following notice in your software, documentation, or "About" page:

> This software is based on adbuiio's MIT open source code.

## Author

- adbuiio
- GitHub: https://github.com/adbuiio

## Changelog

- 2026/4/12: Initial release
