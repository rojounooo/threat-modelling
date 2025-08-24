# Threat Model – To-Do List Web App


## Scope & Assets

Service: 
    - A to-do list web application where users can register, log in, and manage notes.

Assets to protect:

    - User credentials (username + password)
    - Session tokens (cookies / JWTs)
    - User notes (confidentiality + integrity)
    - Service availability

##  System Decomposition

Flow:
    - User enters credentials in a web form.
    - Credentials sent over HTTPS to backend API.
    - Backend verifies user with DB (hashed + salted password).
    - If valid, server issues a session token (JWT/cookie).
    - Token stored client-side, used for future requests.
    - Users create, delete, or update notes; backend updates DB.

Trust boundaries:

    - User device ↔ Server (internet boundary)
    - Server ↔ Database

## Threats (STRIDE + Web App threats)
| Category                   | Example Threats                                                                                      |
| -------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Spoofing**               | Credential stuffing, phishing, session hijacking                                                     |
| **Tampering**              | SQL injection altering DB, modifying session tokens, unauthorized note edits                         |
| **Repudiation**            | User denies creating/deleting notes, denies login attempts                                           |
| **Information Disclosure** | Database leak (plaintext/weak hashes), XSS leaking tokens, insecure APIs exposing other users’ notes |
| **Denial of Service**      | Brute-force login attempts, flooding with fake tasks                                                 |
| **Elevation of Privilege** | Exploit misconfigured roles to become admin                                                          |

## Risk Assessment 
| Threat                         | Likelihood | Impact    | Risk Level      |
| ------------------------------ | ---------- | --------- | --------------- |
| Credential stuffing            | High       | High      | **High**        |
| Weak password storage          | Medium     | Very High | **High**        |
| SQL Injection                  | High       | High      | **High**        |
| XSS                            | Medium     | High      | **Medium–High** |
| CSRF                           | Medium     | Medium    | **Medium**      |
| DoS (brute force / spam tasks) | Medium     | Medium    | **Medium**      |


## Mitigations

Authentication:
    - Rate limiting, CAPTCHA, MFA
    - Strong password hashing (bcrypt/Argon2 + salt)

Session Security:
    - HTTPS everywhere, secure cookie flags (HttpOnly, SameSite)

Injection protection:
    - Parameterized queries / ORM
    - Least privilege DB account

XSS Protection:
    - Input sanitization, output encoding
    - Content Security Policy (CSP)

CSRF Protection:
    - CSRF tokens, SameSite cookies

Availability:
    - Rate limiting on login + note creation
    - WAF or API gateway protections

Auditing & Logging:
    - Centralized login + note action logs

## Validation & Iteration

    - Conduct penetration testing & code review.
    - Review logs regularly.
    - Update threat model when new features (e.g., sharing notes, password reset, API keys) are introduced.