# Software Security

## Security Services

  * Availability
  * Confidentiality
  * Integrity
    * Authentication
    * Authorization
    * Non-repudiation


## Cryptography

  * **Perfect Secrecy:**
    * Observing the ciphertext should not reveal any additional information about the distribution of the plaintext.
    * Encryption scheme (Gen, Enc, Dec) with message space M and ciphertext space C is perfectly secret
      if for every distribution over M every m ∈ M, and every c ∈ C with Pr[C = c] > 0,
      it holds that: Pr[M = m | C = c] = Pr[M = m]
    * **One-Time Pad:**
      * Let M = {0,1}<sup>n</sup>
      * Gen: choose a uniform key k ∈ {0,1}<sup>n</sup>
      * Enc<sub>k</sub>(m) = k ⊕ m
      * Dec<sub>k</sub>(c) = k ⊕ c
      * One-time pad is perfectly secret if each key is used for encrypting only once (|K|>|M|)!
  * **Computational Secrecy:**
    * It would be ok if an encryption scheme leaked information with tiny probability to attackers with bounded computational resources.


## Encryption Algorithms

  * **Symmetric**
    * Block Ciphers:
      * DES, 3DES
      * IDEA
      * RC5, RC6
      * AES
      * Blowfish
      * CAST-128
    * Stream Ciphers:
      * RC4
      * Rabbit
      * Trivium
  * **Asymmetric (Public-Key)**
    * Diffie–Hellman (Key Exchange)
    * ElGamal
    * RSA


## Message Authentication

  * **Hash Functions:**
    * MD5, MD6
    * SHA-1, SHA-256, SHA-512
    * RIPEMD, RIPEMD-128, RIPEMD-256
  * **Message Authentication Code (MAC):**
    * Hashed Message Authentication Code (HMAC)


## Internet Security

  * **IPsec**
    * Layer: Internet/Network
    * Internet Protocol security uses cryptographic security services to protect communications over Internet Protocol networks.
    * Encapsulating Security Payload (ESP) and Authentication Header (AH) are the two IPSec protocols for providing these security services:
      * Network-level peer authentication
      * Data origin authentication
      * Data integrity
      * Data confidentiality (encryption)
      * Replay protection
    * IPsec includes protocols for
      * Mutual authentication between agents at the beginning of the session
      * Negotiation of cryptographic keys to be used during the session.
    * IPsec can be used in protecting data flows
      * Between a pair of hosts (host-to-host)
      * Between a pair of security gateways (network-to-network)
      * Between a security gateway and a host (network-to-host).
    * Transport mode:
      * IPsec Transport mode is used for end-to-end communications.
      * Only the payload of the IP packet is encrypted and/or authenticated.
      * The original IP headers remain intact, except that the IP protocol field is changed to ESP or AH.
    * Tunnel mode**
      * Tunnel mode is used to encrypt traffic between secure IPsec gateways.
      * Tunnel mode is commonly used between gateways, or at an end-station to a gateway.
      * The entire original IP packet is encrypted and/or authenticated.
      * IPsec wraps the original packet, encrypts it, adds a new IP header and sends it to the other side of the VPN tunnel (IPsec peer).

  * **TLS/SSL**
    * Layer: Application
    * The TLS protocol provide authentication, integrity and confidentiality (encryption) for client-server applications.
    * Other protocols can operate either with or without TLS/SSL in to ways:
      * Using a different port number for TLS version of protocol
      * Using a protocol-specific mechanism to request the server switch the connection to TLS
    * Client and server negotiate a stateful connection by a handshaking procedure to agree on parameters used during the secure session.
      * The handshake begins when a client connects to a server requesting a secure connection and suggests a list of ciphers and hash functions.
      * The server picks a cipher and hash function that it also supports and notifies the client of the decision.
      * The server sends back its digital certificate including the server name, the trusted certificate authority (CA) and the server's public key.
      * The client validates the certificate and may contact the the trusted CA and confirm the validity of the certificate.
      * For generating the session key used for the secure session, the client either:
        * Encrypts a random number with the server's public key and sends it to the server for generating a unique session key.
        * Uses Diffie-Hellman to securely generate a random and unique session key which has also the forward secrecy property.
      * This ends the handshake and begins the secure session which is encrypted and decrypted with the session key until the connection closes.

  * Forward Secrecy:
    * Forward secrecy is a property of secure communication protocols.
    * A secure communication protocol has forward secrecy property if compromise of long-term keys does not compromise past session keys.


## Memory Attacks

  * Buffer Overflow
    * Stack-based
    * Heap-based
  * Integer Overflow
  * Read Overflow
  * Stale Memory Attacks
  * Format String Attacks


## Web Attacks

  * **SQL Injection**
    * A technique where attacker can inject malicious SQL commands into an SQL statement, via web page input.
    * Defense:
      * Validation: Blacklisting, Whitelisting, ...
      * Sanitization: Escaping, Prepared Statements
  * **Session Hijacking**
    * The exploitation of a valid session by stealing a cookie and impersonating a  legitimate user to access information or services in a server.
    * Defense:
      * Cookies should be unpredictable, randomly chosen, and sufficiently long
      * Application can also require separate correlating information to accept requests.
      * Have timeout for sessions and delete them once the session ends.
  * **Cross-Site Scripting (XSS)**
    * Persistent (Stored):
      * The data provided by the attacker is saved by the server, and then permanently returned to other users without html escaping.
    * Non-persistent (Reflected):
      * The data provided by a web client, is used immediately by server-side scripts to display a page to user, without sanitizing the request.
      * A reflected attack is typically delivered via email or a neutral web site pointing to a trusted site but containing the XSS vector.
    * XSS attacks exploit the trust a client browser has in data sent from a legitimate website.
    * Defense:
      * Validation: Whitelisting headers, cookies, query strings, form fields, etc.
      * Sanitization: remove all executable portions of user-provided content that will appear in html pages.
  * **Cross-Site Request Forgery (XSRF/CSRF)**
    * Malicious exploit of a website whereby unauthorized requests are sent from a user that the website trusts.
    * XSRF attacks exploit the trust a legitimate website has in data sent from the client browser.
    * Defense:
      * Secretized Links: include a secret in every link/form via hidden fields, custom headers, or directly encoded in URL.
      * Use the REFERER header it has been set by client's browser: trust requests from pages a user can legitimately reach.

