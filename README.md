### MacOS System Cleanup Guide 🧹

> Efficient, safe, and professional way to clean caches, logs, and temporary files on macOS ⭐️

### 📝 Important Notes

- Always **backup important files** before running cleanup commands ⚠
- Commands using `sudo` require **admin privileges**.  
- These commands are **safe for daily maintenance**, but deleting files outside caches/logs is **not recommended**.  
- Running cleanup may **temporarily affect app performance** until caches rebuild.  


### 📦 1. Clear User Cache

```bash
rm -rf ~/Library/Caches/*
```
Description:
Deletes all caches in your user Library. Apps will rebuild them automatically.

Effect:
- Frees disk space
- Resets temporary app data


### 📜 2. Clear System Cache
```bash
sudo rm -rf /Library/Caches/*
```

Description:
Removes system-wide caches maintained by macOS and apps.

Effect:

- Frees disk space
- Requires admin privileges

### 🗂 3. Clear Temporary Folders
```bash
sudo rm -rf /private/var/folders/*
```

Description:
Removes temporary files used by macOS and apps.

Effect:

- Frees disk space
- macOS will automatically recreate required folders

### 📑 4. Remove Old System Logs
```bash
sudo find /Library/Logs -type f -mtime +7 -delete
sudo find /private/var/log -type f -mtime +7 -delete
```

Description:
Deletes log files older than 7 days.

Effect:

- Reduces disk usage
- Keeps recent logs for troubleshooting

### 🌐 5. Flush DNS Cache
```bash
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

Description:
Resets DNS cache.

Effect:

- Fixes network or connectivity issues

- Useful after changing DNS settings

### 🧸 6. Free Up Inactive Memory
```bash
sudo purge
```

Description:
Clears inactive memory to free RAM.

Effect:

- Helps improve performance

- Recommended when experiencing slowdowns

### 🔮 7. Reindex Spotlight
```bash
sudo mdutil -E /
```

Description:
Forces macOS Spotlight to reindex the entire drive.

Effect:

- Fixes search issues

- Rebuilds indexing for faster file search

### ✅ Pro Tips for Safe Cleanup

- Run commands one at a time to monitor effects.

- Avoid deleting system-critical files.

- Restart your Mac after cleanup for maximum efficiency.

- Combine this with regular disk maintenance and app updates for optimal performance.

### 🖥 Optional: Combine All Commands into One Script
```bash
#!/bin/bash
echo "🧹 Starting macOS cleanup..."
rm -rf ~/Library/Caches/*
sudo rm -rf /Library/Caches/*
sudo find /Library/Logs -type f -mtime +7 -delete
sudo find /private/var/log -type f -mtime +7 -delete
sudo rm -rf /private/var/folders/*
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
sudo purge
sudo mdutil -E /
echo "✅ Cleanup complete!"
```

Instructions:

- Save as mac_cleanup.sh

- Make it executable:
```bash
chmod +x mac_cleanup.sh
```

Run the script:
```bash
./mac_cleanup.sh
```
