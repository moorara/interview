# Software Security

## Security Services

  - Availability
  - Confidentiality
  - Integrity
    - Authentication
    - Authorization
    - Non-repudiation


## Cryptography Secrecy

  - **Perfect Secrecy:**
    - Observing the ciphertext should not reveal any additional information about the distribution of the plaintext.
    - Encryption scheme (Gen, Enc, Dec) with message space M and ciphertext space C is perfectly secret
      if for every distribution over M every m ∈ M, and every c ∈ C with Pr[C = c] > 0,
      it holds that: Pr[M = m | C = c] = Pr[M = m]
    - **One-Time Pad:**
      - Let M = {0,1}<sup>n</sup>
      - Gen: choose a uniform key k ∈ {0,1}<sup>n</sup>
      - Enc<sub>k</sub>(m) = k ⊕ m
      - Dec<sub>k</sub>(c) = k ⊕ c
      - One-time pad is perfectly secret if each key is used for encrypting only once (|K|>|M|)!
  - **Computational Secrecy:**
    - It would be ok if an encryption scheme leaked information with tiny probability to attackers with bounded computational resources.


## Encryption Algorithms

  - **Symmetric**
    - Block Ciphers:
      - DES, 3DES
      - IDEA
      - RC5, RC6
      - AES
      - Blowfish
      - CAST-128
    - Stream Ciphers:
      - RC4
      - Rabbit
      - Trivium
  - **Asymmetric (Public-Key)**
    - Diffie–Hellman (Key Exchange)
    - ElGamal
    - RSA


## Message Authentication

  - **Hash-based Message Authentication Code (HMAC)**
    - HMAC is a function that receives a cryptographic **secret key** and a **hash function**
    - Hash Functions:
      - MD5, MD6
      - SHA-1, SHA-256, SHA-512
      - RIPEMD, RIPEMD-128, RIPEMD-256


## Internet Security

  - **IPsec**
    - Layer: Internet/Network
    - Internet Protocol security uses cryptographic security services to protect communications over Internet Protocol networks.
    - Encapsulating Security Payload (ESP) and Authentication Header (AH) are the two IPSec protocols for providing these security services:
      - Network-level peer authentication
      - Data origin authentication
      - Data integrity
      - Data confidentiality (encryption)
      - Replay protection
    - IPsec includes protocols for
      - Mutual authentication between agents at the beginning of the session
      - Negotiation of cryptographic keys to be used during the session.
    - IPsec can be used in protecting data flows
      - Between a pair of hosts (host-to-host)
      - Between a pair of security gateways (network-to-network)
      - Between a security gateway and a host (network-to-host).
    - Transport mode:
      - IPsec Transport mode is used for end-to-end communications.
      - Only the payload of the IP packet is encrypted and/or authenticated.
      - The original IP headers remain intact, except that the IP protocol field is changed to ESP or AH.
    - Tunnel mode**
      - Tunnel mode is used to encrypt traffic between secure IPsec gateways.
      - Tunnel mode is commonly used between gateways, or at an end-station to a gateway.
      - The entire original IP packet is encrypted and/or authenticated.
      - IPsec wraps the original packet, encrypts it, adds a new IP header and sends it to the other side of the VPN tunnel (IPsec peer).

  - **TLS/SSL**
    - Layer: Application
    - The TLS protocol provide authentication, integrity and confidentiality (encryption) for client-server applications.
    - Other protocols can operate either with or without TLS/SSL in to ways:
      - Using a different port number for TLS version of protocol
      - Using a protocol-specific mechanism to request the server switch the connection to TLS
    - Client and server negotiate a stateful connection by a handshaking procedure to agree on parameters used during the secure session.
      - The handshake begins when a client connects to a server requesting a secure connection and suggests a list of ciphers and hash functions.
      - The server picks a cipher and hash function that it also supports and notifies the client of the decision.
      - The server sends back its digital certificate including the server name, the trusted certificate authority (CA) and the server's public key.
      - The client validates the certificate and may contact the the trusted CA and confirm the validity of the certificate.
      - For generating the session key used for the secure session, the client either:
        - Encrypts a random number with the server's public key and sends it to the server for generating a unique session key.
        - Uses Diffie-Hellman to securely generate a random and unique session key which has also the forward secrecy property.
      - This ends the handshake and begins the secure session which is encrypted and decrypted with the session key until the connection closes.

  - Forward Secrecy:
    - Forward secrecy is a property of secure communication protocols.
    - A secure communication protocol has forward secrecy property if compromise of long-term keys does not compromise past session keys.


## Security by Design Principles

  - Minimize attack surface area
  - Establish secure defaults
  - Principle of **Least privilege**
  - Principle of **Defense in depth**
  - Fail securely
  - Don’t trust services
  - Separation of duties
  - Avoid security by obscurity
  - Keep security simple
  - Fix security issues correctly


## Zero-Trust Security

  - The network is always assumed to be hostile.
  - External and internal threats exist on the network at all times.
  - Network locality is not sufficient for deciding trust in a network.
  - Every user, device, and/or agent is **authenticated** and **authorized**.
  - Policies must be dynamic and calculated from many sources of data.


## Attacks

### Memory Attacks

  - Buffer Overflow
    - Stack-based
    - Heap-based
  - Integer Overflow
  - Read Overflow
  - Stale Memory Attacks
  - Format String Attacks

