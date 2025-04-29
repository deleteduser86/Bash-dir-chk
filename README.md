# Bash Directory Existence Check Cheatsheet

This repository provides a comprehensive guide and examples for checking directory existence in Bash scripts. It also includes best practices for error handling and reusable methods to make your Bash scripting more robust.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Cheatsheet: Directory Existence Checks](#cheatsheet-directory-existence-checks)
3. [Error Handling Best Practices](#error-handling-best-practices)
4. [Reusable Function Template](#reusable-function-template)
5. [Examples](#examples)
6. [Contributing](#contributing)
7. [License](#license)

---

## Introduction

Bash is a powerful scripting language often used for automating tasks in Linux environments. One common task is checking whether a directory exists. This repository aims to provide clear, optimized, and reusable methods for performing directory existence checks in Bash, ensuring error handling is robust and adaptable.

---

## Cheatsheet: Directory Existence Checks

### 1. **Using `if` with `-d`**
```bash
DIR="/path/to/directory"

if [ -d "$DIR" ]; then
  echo "Directory exists."
else
  echo "Directory does not exist."
fi
```

### 2. **Using `[[` with `-d`**
```bash
DIR="/path/to/directory"

if [[ -d "$DIR" ]]; then
  echo "Directory exists."
else
  echo "Directory does not exist."
fi
```

### 3. **Using `test` Command**
```bash
DIR="/path/to/directory"

if test -d "$DIR"; then
  echo "Directory exists."
else
  echo "Directory does not exist."
fi
```

### 4. **Using `ls` Command**
```bash
DIR="/path/to/directory"

ls "$DIR" >/dev/null 2>&1
if [ $? -eq 0 ]; then
  echo "Directory exists."
else
  echo "Directory does not exist."
fi
```

### 5. **Using `find` Command**
```bash
DIR="/path/to/directory"

if find "$DIR" -type d >/dev/null 2>&1; then
  echo "Directory exists."
else
  echo "Directory does not exist."
fi
```

### 6. **Using `stat` Command**
```bash
DIR="/path/to/directory"

if stat "$DIR" >/dev/null 2>&1; then
  echo "Directory exists."
else
  echo "Directory does not exist."
fi
```

### 7. **Using Logical Operators**
```bash
DIR="/path/to/directory"

test -d "$DIR" && echo "Directory exists." || echo "Directory does not exist."
```

---

## Error Handling Best Practices

1. **Always Quote Variables**
   - Use `"$DIR"` to handle spaces or special characters in paths.
   
2. **Redirect Errors**
   - Use `2>/dev/null` to suppress error messages when accessing non-existent directories.
   
3. **Validate Input**
   - Check for empty or malformed input before testing.

4. **Handle Permissions**
   - Ensure the script has the necessary permissions to access the directory.

5. **Set Exit Codes**
   - Use `exit 1` for errors to indicate failure.

---

## Reusable Function Template

Encapsulate directory checks in a reusable function:

```bash
check_directory() {
  local DIR="$1"
  
  if [[ -d "$DIR" ]]; then
    echo "Directory '$DIR' exists."
    return 0
  else
    echo "Directory '$DIR' does not exist."
    return 1
  fi
}
```

Usage:
```bash
DIR="/path/to/directory"
check_directory "$DIR"
```

---

## Examples

### Example 1: Basic Check
```bash
DIR="/home/user/docs"
if [ -d "$DIR" ]; then
  echo "Documents directory exists."
else
  echo "Documents directory does not exist."
fi
```

### Example 2: Check with Error Suppression
```bash
DIR="/invalid/path"
if stat "$DIR" >/dev/null 2>&1; then
  echo "Directory exists."
else
  echo "Directory does not exist."
fi
```

### Example 3: Using Reusable Function
```bash
DIR="/tmp"
check_directory "$DIR" || echo "Failed to locate directory."
```

---

## Contributing

We welcome contributions! Follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-name`).
3. Commit your changes (`git commit -m "Description of changes"`).
4. Push to the branch (`git push origin feature-name`).
5. Open a pull request.

Ensure your code follows the best practices outlined in this documentation.

---

## License

This project is licensed under the [MIT License](LICENSE).

---
