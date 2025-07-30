
# Lab: Reflected XSS into HTML Context with Nothing Encoded

## Lab Description

This lab contains a simple **reflected cross-site scripting (XSS)** vulnerability in the search functionality. The application reflects user input directly into the **HTML body** without performing any output encoding or input sanitization.

The goal is to exploit the vulnerability by injecting a script payload that causes a JavaScript `alert()` to execute.

---

## Objective

- Identify and exploit a reflected XSS vulnerability.
- Inject a payload that successfully executes `alert(1)` in the victim's browser.

---

## Environment Setup

- **Target URL:** `https://<lab-url>/?search=...`
- **Tools Used:**
  - Browser (Chrome/Firefox)
  - Optional: Burp Suite (for request inspection)

---

## Step-by-Step Exploit Walkthrough

### 1. Input Reflection Check

- Accessed the lab’s search functionality.
- Entered:

```

  <test>
  ```

* Observed the response reflected as:

  ```html
  <h1>0 search results for '<test>'</h1>
  ```

* Confirmed: input lands inside **HTML body content**, **not escaped or encoded**.

---

### 2. Payload Injection

* Injected the following payload into the `search` parameter:

  ```
  <script>alert(1)</script>
  ```

* Final URL looked like:

  ```
  https://<lab-url>/?search=<script>alert(1)</script>
  ```

---

### 3. Results and Verification

* The page rendered successfully.
* A JavaScript alert box popped up with `1`.
* Lab marked as **Solved**.

---

## Payloads Used

| Purpose       | Payload                     |
| ------------- | --------------------------- |
| XSS Execution | `<script>alert(1)</script>` |

---

## Lessons Learned

* Reflected XSS occurs when user input is reflected in the response without sanitization.
* When input is placed in **raw HTML context**, a `<script>` tag can be used to execute arbitrary JavaScript.
* Proper mitigation would involve:

  * **Output encoding** of HTML special characters.
  * **Context-aware escaping** (HTML, JS, URL, etc.).
  * Consider using **Content Security Policy (CSP)**.

---

## Screenshots and Images

1. **Before Injection:**

   Screenshot showing the reflected `<test>` input in the HTML.

   ![Before Injection](./before-xss.png)

2. **After Injection:**

   Screenshot showing the `alert(1)` popup triggered by `<script>` injection.

   ![After Injection](./after-xss.png)

---

## Conclusion

This lab demonstrates how failing to sanitize or encode user input leads to a **critical XSS vulnerability**. By injecting a basic `<script>` tag into unescaped HTML, an attacker can execute malicious JavaScript in the context of the victim’s browser.

```

