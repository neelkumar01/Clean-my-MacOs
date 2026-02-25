<div align="center">
  <h1 align="center">
    MacOS System Cleanup Guide
    <p></p>
    <img height="100" alt="ticket" src="https://github.com/user-attachments/assets/078226ad-d5c1-429e-b57c-43e147e09083" />
  </h1>
  <p>Efficient, safe, and professional way to clean caches, logs, and temporary files on macOS ⭐️</p>
</div>

> ⚠️ Disclaimer <br>
This script is powerful and uses sudo in multiple places. Review each command carefully before executing <br>
Some paths may be system-specific. Always test commands individually before running them in bulk.

### 📌 What This Script Does
- Clears user and system caches
- Removes old logs
- Deletes Time Machine local snapshots
- Cleans Homebrew cache
- Clears Xcode derived data
- Cleans browser and VS Code cache
- Flushes DNS & system cache
- Rebuilds Spotlight index
- Removes old system logs

### ⚠️ Important Safety Guidelines
Before running:
1. ✅ Backup important data (Time Machine recommended)
2. ✅ Read every command
3. ❌ Never run blindly from the internet
4. 🧪 Test commands individually first
5. 🔐 Only use sudo when necessary

### 🧼 Cleanup Commands

### 1. Clear User Cache
```bash
rm -rf ~/Library/Caches/*
```

**What it does?** <br>
Deletes application cache stored in your user directory.

**Safe?** <br>
Yes. Apps regenerate cache automatically.

---

### 2. Clear System Cache
```bash
sudo rm -rf /Library/Caches/*
```

**What it does?** <br>
Removes system-wide cached files.

**Safe?** <br>
Generally safe, but requires admin privileges.

---

### 3. Delete Old Logs (Older than 7 Days)
```bash
sudo find /Library/Logs -type f -mtime +7 -delete
sudo find /private/var/log -type f -mtime +7 -delete
```

**What it does?** <br>
Deletes logs older than 7 days.

**Why helpful?** <br>
Prevents log files from consuming disk space.

---

### 4. Flush DNS Cache
```bash
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
```

**What it does?** <br>
Clears DNS cache. Useful if websites are not resolving correctly.

---

### 5. Clear Memory Cache (RAM)
```bash
sudo purge
```

**What it does?** <br>
Frees inactive RAM.

**Note:** <br>
Modern macOS manages memory well. This is usually unnecessary.

---

### 6. Rebuild Spotlight Index
```bash
sudo mdutil -E /
```

**What it does?** <br>
Erases and rebuilds Spotlight search index.

**Use only if:** <br>
Spotlight search is not working properly.

---

### 7. Delete Time Machine Local Snapshots
```bash
tmutil listlocalsnapshots /
sudo tmutil deletelocalsnapshots <snapshot-date>
```

**Or automated:**
```bash
for d in $(tmutil listlocalsnapshots / | grep -oE '[0-9]{4}-[0-9]{2}-[0-9]{2}-[0-9]{6}'); do sudo tmutil deletelocalsnapshots $d; done
```

**What it does?** <br>
Deletes local backup snapshots that consume disk space.

---

### 8. Homebrew Cleanup
```bash
brew cleanup -s
rm -rf $(brew --cache)
```

**What it does?** <br>
Removes outdated formulae and cached downloads.

---

### 9. Xcode Cleanup
```bash
rm -rf ~/Library/Developer/Xcode/DerivedData/*
```

**What it does?** <br>
Removes build artifacts from Xcode.

**Safe?** <br>
Yes. Rebuilt automatically on next build.

---

### 10. VS Code Cache Cleanup
```bash
rm -rf ~/Library/Application\ Support/Code/CachedData/*
rm -rf ~/Library/Application\ Support/Code/User/WorkspaceStorage/*
rm -rf ~/Library/Application\ Support/Code/logs/*
```

**What it does?** <br>
Removes temporary and cached workspace data.

---

### 11. Google Chrome Cleanup
```bash
rm -rf ~/Library/Application\ Support/Google/Chrome/*/Cache/*
rm -rf ~/Library/Application\ Support/Google/Chrome/*/Code\ Cache/*
rm -rf ~/Library/Application\ Support/Google/Chrome/*/Service\ Worker/CacheStorage/*
```

**What it does?** <br>
Clears browser cache for all profiles.

**Warning:** <br>
Will log you out of some websites.

---

### 12. Remove Old Logs (3 Days)
```bash
sudo find /var/log -type f -mtime +3 -delete
```

**What it does?** <br>
Deletes logs older than 3 days.

---

### 13. Reset Font Cache
```bash
atsutil databases -remove
```

**What it does?** <br>
Useful if fonts behave incorrectly.

---

### 14. Reset QuickLook Cache
```bash
qlmanage -r cache
```

**What it does?** <br>
Fixes preview glitches in Finder.

---

### ⚠️ Commands That Are SYSTEM-SPECIFIC

These may vary depending on your setup:

```bash
rm -rf ~/Library/Application\ Support/Google/GoogleSoftwareUpdate/*
rm -rf ~/Library/Application\ Support/Code/*
```

**Note:** <br>
If you don’t use the following applications, you can remove their cleanup sections safely:

- VS Code  
- Chrome  
- Xcode  
- Homebrew

### 🔐 Final Warning

Some commands like:

```bash
sudo rm -rf /private/var/log/*
sudo rm -rf /Library/Logs/*
```

**Warning:** <br>
These can remove diagnostic data needed for troubleshooting.

Use responsibly.
