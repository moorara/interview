# Web Security

## Attacks

  - **SQL Injection**
    - A technique where attacker can inject malicious SQL commands into an SQL statement, via web page input.
    - Defense:
      - Validation: Blacklisting, Whitelisting, ...
      - Sanitization: Escaping, Prepared Statements
  - **Session Hijacking**
    - The exploitation of a valid session by stealing a cookie and impersonating a  legitimate user to access information or services in a server.
    - Defense:
      - Cookies should be unpredictable, randomly chosen, and sufficiently long
      - Application can also require separate correlating information to accept requests.
      - Have timeout for sessions and delete them once the session ends.
  - **Cross-Site Scripting (XSS)**
    - Persistent (Stored):
      - The data provided by the attacker is saved by the server, and then permanently returned to other users without html escaping.
    - Non-persistent (Reflected):
      - The data provided by a web client, is used immediately by server-side scripts to display a page to user, without sanitizing the request.
      - A reflected attack is typically delivered via email or a neutral web site pointing to a trusted site but containing the XSS vector.
    - XSS attacks exploit the trust a client browser has in data sent from a legitimate website.
    - Defense:
      - Validation: Whitelisting headers, cookies, query strings, form fields, etc.
      - Sanitization: remove all executable portions of user-provided content that will appear in html pages.
  - **Cross-Site Request Forgery (XSRF/CSRF)**
    - Malicious exploit of a website whereby unauthorized requests are sent from a user that the website trusts.
    - XSRF attacks exploit the trust a legitimate website has in data sent from the client browser.
    - Defense:
      - Secretized Links: include a secret in every link/form via hidden fields, custom headers, or directly encoded in URL.
      - Use the REFERER header it has been set by client's browser: trust requests from pages a user can legitimately reach.
  - **Server-Side Request Forgery (SSRF)**
    - An attacker can send crafted requests from back-end server of a vulnerable web application to read or modify internal resources.


## OAuth 2.0 and OpenID Connect

  - OAuth 2.0 is used for **authorization**.
  - OpenID Connect is used for **authentication**.

### Terminology

  - **Roles**
    - Client
    - Resource Owner
    - Resource Server
    - Authorization Server
  - **Misc**
    - Redirect URI
    - Scope
    - Consent
    - Authorization Code
    - Client ID and Client Secret
  - **Endpoints**
    - Authorization Endpoint
    - Token Endpoint
    - User Endpoint (OIDC)
  - **Tokens**
    - Access Token
    - Refresh Token
    - ID Token (OIDC)
  - **Channels**
    - Back Channel (highly secure communication channel)
    - Front Channel (less secure communication channel)

### Authorization Grant Flows

  - Authorization Code (front channel and back channel)
  - Implicit (front channel only)
  - Resource Owner Password Credentials (back channel only)
  - Client Credentials (back channel only)

### JSON Web Token (JWT)

  - `base64(header).base64(payload).<signature>`:
    - **Header**
      - Type: `JWT`
      - Signing Algorithm: `HS256`, `RSA`
    - **Payload**
      - Registered Claims
      - Public Claims
      - Private Claims
    - **Signature**
      - `signing_algorithm(base64(header) + "." + base64(payload), secret)`

