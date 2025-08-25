## Assumptions 
- Users access the service through modern browsers with HTTPS support
- Backend and database are hosted in a trusted cloud environment
- No third-party authentication (e.g. Google, Microsoft, Github login)
- Notes are private to each user 

## Data Classification

- Credentials: High sensitivity 
- Session Tokens: High sensitivity
- Notes: Medium sensitivity

## Authentication & Session Security

- Rate limiting on login attempts to prevent brute-force attacks 
- MFA recommended for high-risk accounts 
- Session cookies are flagged `HttpOnly` and `SameSite` to prevent theft
- JWTs are signed with a strong secret

## Input Validation / Injection Mitigation 

- All API inputs are validated and sanitised 
- SQL statements use parameterised queries to prevent SQL Injections
- Output encoding is applied to prevent XSS

## Logging & Monitoring 

- Login attempts and note actions are logged centrally 
- Alerts on suspicious login activity (e.g. multiple failed attempts)

## Risk Controls

- Regular updates to dependencies to patch known vulnerabilities 
- HTTPS enforced for all client-service communication
- WAF and firewall rules to protect against DoS or common attacks 
- CSRF tokens implemented to prevent forged requests 
- Regular backups of the database with secure, offsite storage
- Periodic restoration testing to verify backup integrity