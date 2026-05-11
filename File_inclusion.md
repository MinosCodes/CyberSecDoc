# File Inclusion

Short summary of file inclusion vulnerabilities and how they are used in practice.

## Definition

File inclusion is a vulnerability that occurs when an application loads files based on user-controlled input without proper validation. It can lead to reading sensitive files or, in some cases, executing malicious code.

## Why It Matters

File inclusion issues can expose configuration files, source code, credentials, or system files. In more severe cases, they can be chained into remote code execution if an attacker can influence the included file.

## Notes

- Path traversal / directory traversal.
- Dot-dot-slash attacks: `../`
- Climb up directories until the root directory is reached.
- Common OS files used while testing:
- `/etc/passwd`: The most common file for testing LFI on Linux, as it is typically world-readable and reveals all users on the system.
- `/etc/shadow`: Contains hashed user passwords (requires root privileges).
- `/etc/issue`: Contains system identification information.
- `/etc/profile`: Contains system-wide environment variables.
- `/proc/version`: Reveals kernel version and system information.
- `/proc/self/environ`: Used to execute code by injecting it into environment variables.
- `/root/.bash_history`: Contains command history for the root user.
- `/var/log/apache2/access.log` or `/var/log/nginx/access.log`: Used for log poisoning to achieve remote code execution (RCE).
- file_get_contents is the function that causes this vulnerabilities in PHP .

