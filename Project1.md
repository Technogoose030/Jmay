---
layout: default
---

## Project 1: Vulnerability Assessment Using Burp Suite on a Home Lab with Active Directory

Executed a detailed vulnerability assessment on a home lab environment configured with Active Directory to simulate a corporate network. The project utilized Burp Suite to identify and analyze web application vulnerabilities and their implications for the integrated Active Directory setup.

# 1.Home Lab Setup:

# <ins>Infrastructure Configuration:<ins>

There are free trials or access at these links 

Burpsuite community edition(cant web app scan with the free version unfortunately)

https://portswigger.net/burp/releases/professional-community-2024-6-6?requestededition=community&requestedplatform=

Windows Server 2022 

https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022  

Windows 10 Enterprise

https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise

## <ins>Virtualization:<ins>
Deployed a virtualized environment using software like VMware Workstation.

Set up multiple virtual machines (VMs) to simulate various network roles, including domain controllers, application servers, and client workstations.

## <ins>Active Directory (AD):<ins>

Installed and configured Windows Server with Active Directory Domain Services (AD DS) on a dedicated VM.

Created a domain (e.g., marvel.local) and configured organizational units (OUs), user accounts, and group policies to replicate a typical corporate setup.

## <ins>Web Application:<ins>

Deployed a vulnerable web application (e.g., DVWA – Damn Vulnerable Web Application) on a separate VM to serve as the target for testing.

Configured the web application to interact with Active Directory for authentication and authorization, simulating a real-world scenario.

# <ins> 2. Burp Suite Configuration:<ins>

## <ins>Installation and Setup:<ins>

Installed Burp Suite on a local machine.

Configured Burp Suite to intercept traffic by setting up a local proxy server using foxyproxy, typically running on port 8080.

## <ins>Browser Configuration:<ins>

Configured web browsers Firefox to use Burp Suite’s proxy for all HTTP/S traffic.

Set up SSL certificates in Burp Suite to decrypt and inspect HTTPS traffic without browser security warnings.

# <ins>3. Scanning and Testing:<ins>

## <ins>Spidering:<ins>

Used Burp Suite’s Spider tool to automatically crawl the web application and map its structure, including all pages, parameters, and functionalities.

Configured spidering settings to follow all links, submit forms, and handle session tokens

## <ins>Automated Scanning:<ins>

Tenable Nessus Web App Scanner to detect common web application vulnerabilities such as SQL injection, Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF), and insecure direct object references.

Analyzed scan results for severity levels and potential impacts on security.

## <ins>Manual Testing:<ins>

Conducted manual tests using Burp Suite’s Intruder and Repeater tools to exploit vulnerabilities identified during automated scanning.

Performed targeted attacks, such as injecting malicious payloads into form fields and URL parameters to confirm and exploit vulnerabilities.

# <ins>4. Active Directory Integration Testing:<ins>

## <ins>Session Management:<ins>

## Session Fixation:

Captured session cookies using Burp Suite.Attempted to access the application with captured cookies to test if unauthorized access was possible.

## Session Expiry:

Tested session timeout and logout functionality.Confirmed sessions expired after inactivity and were invalidated upon logout.

## Session Regeneration:

Checked if the application regenerated session IDs after login and sensitive actions.

## Findings:

Session Fixation: Application allowed session ID fixation.

Session Hijacking: Session cookies lacked Secure attributes.

Session Expiry: Ineffective session timeout enforcement.

## Remediation:

Fixed Session ID: Implemented session ID regeneration post-login.

Secure Cookies: Added Secure, HttpOnly, and SameSite attributes to cookies.

Improved Expiry: Configured proper session timeout and validated implementation.


## <ins>Privilege Escalation:<ins>

Checked for privilege escalation opportunities by exploiting vulnerabilities in the web application that might allow unauthorized access to AD resources or functions.

Attempted to bypass access controls and view or modify sensitive data in AD based on application flaws.

## <ins>Injection Attacks:<ins>

## <ins>LDAP Injection:<ins>

Tested for LDAP injection vulnerabilities by injecting payloads into search parameters and login forms.

Evaluated the impact on Active Directory, such as unauthorized access or directory enumeration.

# <ins>5.Reporting and Remediation:<ins>

## <ins>Detailed Reporting:<ins>

## <ins>Vulnerability Identification:<ins>

The vulnerability assessment successfully identified and remediated a critical XSS vulnerability and some session id problems like fixation, hijacking and session expiry within the home lab environment.

Their was alot of vulnerabilities not listed that would still have to be looked at assessed and remediated  

## <ins>Remediation Recommendations:<ins>

Implemented server-side input validation to filter out potentially malicious input. Modified the web application code to ensure that all user inputs are validated against a whitelist of acceptable characters.

Applied output encoding to ensure that user input is rendered as plain text in the web application. Updated the search results display logic to escape special characters, preventing them from being interpreted as HTML or JavaScript.

## <ins>Follow-Up Actions:<ins>

## <ins>Verification:<ins>

Conducted follow-up testing to ensure that all identified vulnerabilities were remediated effectively.
Re-ran Burp Suite’s Scanner tool to ensure that the XSS vulnerability was successfully mitigated.

Conducted manual testing using Burp Suite’s Intruder and Repeater tools to confirm that the input validation and output encoding were correctly implemented and that no XSS vulnerabilities remained.


>
>>
>>>
>>>>
>>>>

[Back To Main](./)
