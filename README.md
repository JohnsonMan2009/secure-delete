## Secure File/Folder Delete Tool

This is a cross-platform (Windows/Linux) command-line tool for **securely deleting files and folders**. It is designed to make data recovery extremely difficult by overwriting, renaming, and finally removing the target files and directories.

### Features

- **Multi-pass Overwrite:** Each file is overwritten multiple times (default: 3 passes) with zeros, ones, and random data.
- **Random Renaming:** The file is renamed to a random name after each overwrite pass to prevent recovery by filename.
- **Truncation:** After overwriting, the file is truncated to a random length to further obfuscate residual data.
- **Read-only Attribute Removal:** The tool removes read-only attributes before deletion to maximize success.
- **Recursive Folder Deletion:** Securely deletes all files and subfolders within a directory.
- **Privilege Check:** Requires administrator (Windows) or root (Linux) privileges to run, ensuring it can access and delete protected files.

### How It Works

1. **Privilege Check:** The script checks if it is running with administrator/root privileges. If not, it exits with a message.
2. **File Deletion Logic:**
    - For each file:
        - Remove read-only attributes.
        - Overwrite the file multiple times:
            - First pass: all zeros.
            - Second pass: all ones.
            - Third and subsequent passes: random data.
        - After each pass, rename the file to a random name.
        - After overwriting, truncate the file to a random length.
        - Rename one final time, then delete.
    - For folders:
        - Recursively apply the above logic to all files and subfolders.
        - Attempt to remove each directory after its contents are deleted.
3. **Error Reporting:** Any files or folders that could not be securely deleted are reported at the end.

### Usage

1. **Run as Administrator/Root:**
    - **Windows:** Right-click your terminal or the generated `.exe` and select "Run as administrator".
    - **Linux:** Run with `sudo python3 delete.py`.

2. **Interactive Menu:**
    - Type `1` to securely delete a file or folder.
    - Enter the full path to the file or folder you wish to delete.
    - Type `quit` to exit the program.

### Example

```
This is a Secure File Delete Application!
Welcome!
Options:
  1. Securely delete a file or folder
  quit. Exit the program

Please input the number (or 'quit' to exit): 1
You want to securely delete a file or folder. Now give me the path. For example: D:\game.exe or D:\myfolder
The path: D:\sensitive_file.txt
File securely deleted: D:\sensitive_file.txt
```

### Security Notice

- This tool is designed for high-security environments. For SSDs, absolute data destruction cannot be guaranteed due to hardware-level wear leveling.
- Always double-check the path you enter—**deleted data cannot be recovered!**
