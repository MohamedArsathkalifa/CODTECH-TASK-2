# CODTECH-TASK-2
Cross-Site Scripting (XSS) is a security vulnerability typically found in web applications where an attacker can inject malicious scripts into web pages viewed by other users. This vulnerability arises when a website allows the injection of untrusted content (like JavaScript, HTML, or other executable code) into web pages that are later executed by other users' browsers.



***How XSS Works***
An attacker injects a script (usually JavaScript) into a web page that is displayed to other users.
When the script is executed in the victim's browser, it can:
Steal sensitive information (like cookies, session tokens, or login credentials).
Redirect the user to malicious websites.
Manipulate the content of the web page, making it look like a legitimate part of the site.
Perform actions on behalf of the user, such as submitting forms, without their consent.



***information***
1.Identifying the XSS Vulnerability
The search box on the website was tested for input sanitization. Entering a basic XSS payload resulted in the payload being executed on the page, confirming the vulnerability


The website indicated that the input was not sanitized by displaying a pop-up window with the alert message once this payload was entered into the search input field.

***payload***

<sCrIpt>alert("XsS")</scRiPt>

![Screenshot 2024-12-07 063434](https://github.com/user-attachments/assets/16507c8d-6d98-4182-aeec-6c6fee4af6fe)

2.Exploiting the XSS Vulnerability web page
Example of Stored XSS

I found a column in the database where the payload could be saved for testing reasons and run when other users accessed it.


![Screenshot 2024-12-07 064618](https://github.com/user-attachments/assets/a52ed705-d580-41a8-b02b-adfd49b4cd29)


***MORE INFORMATION ABOUT XSS***



Steps Taken to Identify the XSS Vulnerability:



Testing for Input Sanitization:

Initial Test: You entered a basic XSS payload, such as <script>alert('XSS')</script>, into the search box.
Observation: When you submitted the input, the script was executed on the page (e.g., an alert box appeared), indicating that the input was not properly sanitized or escaped.




Execution of Payload:

The fact that the payload executed in the browser indicates that the application is not properly validating or escaping user input before rendering it on the page. This failure allows the malicious JavaScript to be injected and executed in the context of the page viewed by other users.


What This Means:
Input Not Sanitized: The web application doesn't sanitize user input correctly, meaning it doesn’t properly escape special characters like <, >, or " that are used in HTML/JavaScript. This lack of sanitization allows malicious scripts to run.


Reflection: The script likely gets reflected back into the page content without modification, making the payload execute. This could be a sign of a Reflected XSS vulnerability, where the malicious script is executed as part of the page response after being input.
