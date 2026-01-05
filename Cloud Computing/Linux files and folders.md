
## 1. What are Files and Folders in Linux?

- **File** → Stores data (text, image, program, config, etc.)
    
- **Folder (Directory)** → Holds files and other folders
    
- In Linux, **everything is treated as a file** (even devices)
    

---
## 2. Linux Directory Structure (Filesystem Tree)

Linux uses a **single root directory**: `/`

```
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── opt
├── proc
├── root
├── sbin
├── tmp
├── usr
└── var
```

### Important Directories

|Directory|Purpose|
|---|---|
|`/`|Root of the filesystem|
|`/home`|User home directories (e.g. `/home/kevin`)|
|`/root`|Home directory for root user|
|`/bin`|Essential command binaries (`ls`, `cp`, `mv`)|
|`/sbin`|System binaries (admin commands)|
|`/etc`|Configuration files|
|`/var`|Variable data (logs, mail, cache)|
|`/tmp`|Temporary files|
|`/usr`|User programs and libraries|
|`/dev`|Device files|
|`/media`|Mounted external devices (USB, CD)|

---

## 3. Paths in Linux

### Absolute Path

- Starts from root `/`
    

```
/home/kevin/Documents/file.txt
```

### Relative Path

- Starts from current directory
    

```
Documents/file.txt
```

### Special Path Symbols

|Symbol|Meaning|
|---|---|
|`.`|Current directory|
|`..`|Parent directory|
|`~`|Home directory|
|`/`|Root|

---

## 4. Basic File & Folder Commands

### 📂 Directory Commands

|Command|Description|
|---|---|
|`pwd`|Show current directory|
|`ls`|List files|
|`ls -l`|Detailed list|
|`ls -a`|Show hidden files|
|`cd folder`|Change directory|
|`cd ..`|Go up one level|
|`mkdir folder`|Create directory|
|`rmdir folder`|Delete empty directory|

---

### 📄 File Commands

|Command|Description|
|---|---|
|`touch file.txt`|Create empty file|
|`cat file.txt`|View file content|
|`less file.txt`|View file page by page|
|`cp file1 file2`|Copy file|
|`mv file1 file2`|Rename or move file|
|`rm file.txt`|Delete file|
|`rm -r folder`|Delete folder and contents|

⚠️ **Be careful with `rm -r` – it deletes permanently**

---

## 5. Hidden Files

- Hidden files start with a **dot (.)**
    

```
.bashrc
.gitignore
```

- View hidden files:
    

```
ls -a
```

---

## 6. File Permissions

Linux uses **read, write, execute** permissions.

```
-rwxr-xr--
```

|Symbol|Meaning|
|---|---|
|`r`|Read|
|`w`|Write|
|`x`|Execute|
|`-`|No permission|

### Permission Groups

1. Owner
    
2. Group
    
3. Others
    

### Change Permissions

```
chmod 755 file.sh
chmod +x script.sh
```

---

## 7. File Ownership

|Command|Description|
|---|---|
|`ls -l`|Show owner and group|
|`chown user file`|Change owner|
|`chgrp group file`|Change group|

---

## 8. Searching Files

```
find /home -name file.txt
```

```
locate file.txt
```

---

## 9. File Types in Linux

|Type|Symbol|
|---|---|
|Regular file|`-`|
|Directory|`d`|
|Link|`l`|
|Device|`b`, `c`|

---

## 10. Practical Example

```
mkdir projects
cd projects
touch app.js
ls
```

---

## 11. Summary

- Linux uses a **tree structure**
    
- Root directory is `/`
    
- Files and folders are managed using terminal commands
    
- Permissions control access
    
- Everything in Linux is treated as a file
    

---

If you want, I can:

- Make **short exam notes**
    
- Convert this into **PDF / Word**
    
- Add **practice exercises**
    
- Explain **permissions in depth**
    

Just tell me 👍