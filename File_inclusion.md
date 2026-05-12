# File Inclusion

Short summary of file inclusion vulnerabilities and how they are used in practice.

## Definition

File inclusion is a vulnerability that occurs when an application loads files based on user-controlled input without proper validation. It can lead to reading sensitive files or, in some cases, executing malicious code.

## Why It Matters

File inclusion issues can expose configuration files, source code, credentials, or system files. In more severe cases, they can be chained into remote code execution if an attacker can influence the included file.

## Entry Point

The entry point is where an application accepts user input and uses it directly (or with insufficient validation) to determine which file to include or load. Common entry points include:

- **URL Parameters**: `page=about.php`, `file=config.ini`
- **Form Fields**: File upload paths, file selection inputs
- **Cookies**: File path stored in session or cookie data
- **Headers**: Custom headers containing file paths
- **Database Values**: User-controlled data fetched from database used in include statements

The vulnerability occurs when the application passes this user input directly to file inclusion functions without proper validation or sanitization.

## Attack Methods

### Path Traversal
- **Directory Traversal**: Navigate up directory levels using relative paths
- **Dot-dot-slash attacks**: Use `../` sequences to climb directories
- Goal: Reach root directory and access sensitive files

## Common Target Files

### Linux System Files
- `/etc/passwd`: User account information (world-readable)
- `/etc/shadow`: Hashed user passwords (root privileges required)
- `/etc/issue`: System identification information
- `/etc/profile`: System-wide environment variables
- `/proc/version`: Kernel version and system information
- `/proc/self/environ`: Environment variables (RCE vector)
- `/root/.bash_history`: Root user command history
- `/var/log/apache2/access.log` or `/var/log/nginx/access.log`: Log files (RCE via log poisoning)

## Vulnerable Functions

### PHP
- `file_get_contents()`: Common function exploited for file inclusion

## Bypass Techniques

- **Keyword Filtering Bypass**: If `../` is filtered, use `....//` to bypass restrictions
- **Directory Restriction Bypass**: If inclusion is limited to a defined directory, include the target path in your payload

## Prevention Methods

- **Keep systems updated**: Maintain the latest versions of all operating systems and services
- **Disable error reporting**: Turn off PHP errors and detailed error messages to avoid leaking source code information
- **Web Application Firewall (WAF)**: Configure a WAF to detect and prevent file inclusion attacks
- **Disable risky functions**: Disable `allow_url_fopen` to prevent Remote File Inclusion (RFI)
- **Input validation**: Never trust user input—always validate, sanitize, and use allowlists for file paths
- **Use secure include functions**: Implement proper path validation before including files
