# CODTECH-TASK-2
Cross-Site Scripting (XSS) is a security vulnerability typically found in web applications where an attacker can inject malicious scripts into web pages viewed by other users. This vulnerability arises when a website allows the injection of untrusted content (like JavaScript, HTML, or other executable code) into web pages that are later executed by other users' browsers.
**How XSS Works**
An attacker injects a script (usually JavaScript) into a web page that is displayed to other users.
When the script is executed in the victim's browser, it can:
Steal sensitive information (like cookies, session tokens, or login credentials).
Redirect the user to malicious websites.
Manipulate the content of the web page, making it look like a legitimate part of the site.
Perform actions on behalf of the user, such as submitting forms, without their consent.
**information**
Identifying the XSS Vulnerability
The search box on the website was tested for input sanitization. Entering a basic XSS payload resulted in the payload being executed on the page, confirming the vulnerability
