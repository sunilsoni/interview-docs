---
layout: default
title: Vulnerabilities
parent: Misc
resource: true
desc: "Common Java Vulnerabilities interview questions and answers."
categories: [Common Java Vulnerabilities]
---

# Common Java Vulnerabilities
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

 
---

## Code Injection

Certainly! Below is an in-depth explanation of Code Injections in Markdown format, as requested:


### Code Injections

Code injection is a prevalent form of attack where an adversary can execute malicious code in a system by taking advantage of the insecure coding practices followed by developers. In Java, this vulnerability primarily manifests when user inputs are not properly sanitized or validated before being used in the program. This allows an attacker to manipulate the code behavior to their advantage.

### Understanding Code Injection

To better understand how code injection works, it's essential to grasp the fundamental idea behind it. When a program accepts input from an external source (e.g., user input, file, network), and this input is not properly validated, it could contain malicious code or commands. If this input is then used within the program in a way that gets executed, it can lead to code injection.

A simple illustration in Java could be using user input in a script execution scenario without proper validation. In such a case, an attacker could inject malicious code that would be executed as part of the application, leading to potentially severe security breaches.

### Example:

Consider the following simplistic Java example that accepts user input and executes it as a script:


```java
import javax.script.*;

public class CodeInjectionExample {
    public static void main(String[] args) throws ScriptException {
        ScriptEngineManager manager = new ScriptEngineManager();
        ScriptEngine engine = manager.getEngineByName("JavaScript");
        String userInput = args[0];
        engine.eval(userInput);  // Unsafe
    }
}
```

In the code above, we are using the `javax.script` package to create a `ScriptEngineManager` and then a `ScriptEngine` for JavaScript. We then accept user input from the command line arguments and pass it directly to the `engine.eval()` method, which executes the input as a script. If an attacker provides malicious JavaScript code as input, it would be executed, leading to a code injection vulnerability.

### Mitigating Code Injection

Preventing code injection involves a multi-step approach that includes input validation, the use of safe APIs, and adhering to the principle of least privilege.

#### Input Validation and Sanitization:
Ensure that all input is validated and sanitized before it's used in your code. Validation means checking that the input meets certain criteria (e.g., a date is in the correct format), while sanitization involves cleaning or transforming the input to remove any potentially harmful content.

#### Use Safe APIs:
Whenever possible, use safe APIs that either do not allow for code execution or provide built-in protections against injection attacks.

#### Principle of Least Privilege:
Run your code with the least amount of privilege necessary to perform its tasks. This way, even if an attacker manages to inject code, the damage they can do is limited.

#### Parameterized Statements:
For database access, use parameterized statements or prepared statements, which ensure that user input is always treated as data and not executable code.

#### Escape Special Characters:
Ensure that special characters in user input that could be used to facilitate code injection are escaped.

#### Security Headers and Policies:
Implement security headers and policies like Content Security Policy (CSP) to mitigate the risk of code injection.

#### Regular Code Reviews and Security Testing:
Regular code reviews and security testing can help identify and fix code injection vulnerabilities before they can be exploited.

By following these best practices and being mindful of the potential risks associated with user input, developers can significantly mitigate the risk of code injection vulnerabilities in their Java applications.


 





## Injection Flaws 
Injection flaws, particularly SQL injection, are common in Java EE applications. Injection occurs when user-supplied data is sent to an interpreter as part of a command or query. The attacker’s hostile data tricks the interpreter into  executing unintended commands or changing data.


**Primary Defenses:**
Option 1: Use of Prepared Statements (with Parameterized Queries)
Option 2: Use of Stored Procedures
Option 3: Allow-list Input Validation
Option 4: Escaping All User Supplied Input


**Additional Defenses:**
Also: Enforcing Least Privilege
Also: Performing Allow-list Input Validation as a Secondary Defense



---

## Cross Site Scripting (XSS)

Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script, to a different end user. Flaws that allow these attacks to succeed are quite widespread and occur anywhere a web application uses input from a user within the output it generates without validating or encoding it.

An attacker can use XSS to send a malicious script to an unsuspecting user. The end user’s browser has no way to know that the script should not be trusted, and will execute the script. Because it thinks the script came from a trusted source, the malicious script can access any cookies, session tokens, or other sensitive information retained by the browser and used with that site. These scripts can even rewrite the content of the HTML page.

Types of XSS attacks

There are three main types of XSS attacks. These are:

**Reflected XSS** :  where the malicious script comes from the current HTTP request.
**Stored XSS** :  where the malicious script comes from the website's database.
**DOM-based XSS** : where the vulnerability exists in client-side code rather than server-side code.


---

## How does XSS work?

Cross-site scripting works by manipulating a vulnerable web site so that it returns malicious JavaScript to users. When the malicious code executes inside a victim's browser, the attacker can fully compromise their interaction with the application.

<img src="images/cross-site-scripting.svg" width="781" border="2" />



---

## Cross Site Request Forgery(CSRF)



 
---

## For more information
1. [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
2. [Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
3. [Cross-site scripting](https://portswigger.net/web-security/cross-site-scripting)





