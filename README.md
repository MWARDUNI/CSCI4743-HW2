# CSCI4743-HW2


Section 1 – “Comprehend and Apply” Questions
1.1. (10 points): Compare Stream Ciphers and Block Ciphers in terms of (1) diffusion, (2)
confusion, and (3) error propagation. A) Which one has higher diffusion/confusion/error
propagation? B) Which ones have lower diffusion/confusion/error propagation? Explain and
justify your answers. For block ciphers, make sure to consider “modes of operation” in your response.

Comparison of Stream Ciphers and Block Ciphers:

A) Higher Diffusion/Confusion/Error Propagation:

> Block Ciphers generally have higher diffusion and confusion properties compared to Stream Ciphers. This is because Block Ciphers operate on fixed-size blocks of data, and their design incorporates complex diffusion and confusion layers, such as substitution boxes (S-boxes) and permutation operations. These layers ensure that even a small change in the input block results in a significant change in the output block, providing strong diffusion. Additionally, the key is mixed into the cipher in a highly nonlinear way, creating confusion.

> As for error propagation, Block Ciphers have higher error propagation when used in certain modes of operation, such as Electronic Codebook (ECB) mode or Cipher Block Chaining (CBC) mode without proper error handling. In these modes, a single bit error in the ciphertext can affect an entire block of the plaintext.

B) Lower Diffusion/Confusion/Error Propagation:

> Stream Ciphers typically have lower diffusion and confusion properties compared to Block Ciphers. This is because Stream Ciphers operate on individual bits or bytes of data, and their design focuses more on generating a pseudorandom keystream that is combined with the plaintext. The diffusion and confusion properties rely heavily on the strength of the keystream generation algorithm.

> As for error propagation, Stream Ciphers generally have lower error propagation. If a single bit error occurs in the ciphertext, it typically affects only the corresponding bit or byte in the plaintext, and the error does not propagate further.

> However, modes of operation for Block Ciphers can affect their diffusion, confusion, and error propagation properties. For example, the Cipher Feedback (CFB) and Output Feedback (OFB) modes of operation can provide better error propagation characteristics for Block Ciphers, as errors in the ciphertext only affect a limited number of plaintext bits or bytes.



1.2. (10 points): A blockchain-based cryptocurrency uses proof-of-work to limit the rate of
block generation and uses SHA-256 as the hash function. Assume generating and comparing
2^10 (1024) hashes take 1 minute on a machine with average processing/memory capability.
The cryptocurrency designers want to set the average time of creating the correct proof-of-
work for a new block to 4 minutes. Explain how this could be achieved (hint: how many
leading zeros)

Setting the average time for creating the correct proof-of-work:

To set the average time of creating the correct proof-of-work for a new block to 4 minutes, the designers need to adjust the difficulty level of the proof-of-work puzzle. In this case, the puzzle involves finding a hash value with a certain number of leading zeros.

Given:

Generating and comparing 2^10 (1024) hashes take 1 minute on an average machine.
The desired average time for creating the correct proof-of-work is 4 minutes.
To achieve this, the designers need to set the difficulty level such that, on average, it takes 4 times as many hash computations as it takes to generate and compare 2^10 (1024) hashes.

Since generating and comparing 1024 hashes take 1 minute, generating and comparing 4 × 1024 = 4096 hashes should take approximately 4 minutes on an average machine.

Therefore, the designers should set the difficulty level such that the correct proof-of-work requires finding a hash value with approximately log2(4096) ≈ 12 leading zeros.

By adjusting the required number of leading zeros to 12, the average time for creating the correct proof-of-work should be around 4 minutes on an average machine.

To achieve an average block creation time of 4 minutes using proof-of-work with SHA-256, we need to adjust the difficulty of the mining process by requiring a certain number of leading zeros in the hash output. Let's break this down step by step:

1. Given:
   - Generating and comparing $2^{10}$ (1024) hashes take 1 minute on an average machine.
   - The desired average block creation time is 4 minutes.

2. Let's assume the required number of leading zeros in the hash output is $n$.

3. Probability of finding a hash with $n$ leading zeros is:

   $P(n) = \frac{1}{2^{n}}$

4. Expected number of hashes needed to find a valid hash with $n$ leading zeros is:

   $E(n) = \frac{1}{P(n)} = 2^{n}$

5. Since generating and comparing $2^{10}$ hashes take 1 minute, the time required to find a valid hash with $n$ leading zeros is:

   $T(n) = \frac{E(n)}{2^{10}}$ minutes

6. To achieve an average block creation time of 4 minutes, we need:

   $T(n) = 4$

   $\frac{E(n)}{2^{10}} = 4$

   $E(n) = 4 \times 2^{10} = 2^{12}$

7. From step 4, we know that $E(n) = 2^{n}$. Therefore:

   $2^{n} = 2^{12}$

   $n = 12$

To achieve an average block creation time of 4 minutes using proof-of-work with SHA-256, the cryptocurrency designers should set the difficulty by requiring 12 leading zeros in the hash output. This way, miners will need to generate and compare approximately $2^{12}$ hashes on average to find a valid proof-of-work, which will take around 4 minutes on a machine with average processing/memory capability.




1.3. (10 points) Alice and Bob agree to use the p=23 and g=5. Alice chooses the secret key
a=6, and Bob chooses the secret key b=16. Using the Diffie-Hellman Key Exchange
Protocol, determine the common secret key shared between Alice and Bob. Show the steps
taken to reach this result.

$A = {g^{a} mod p}$
  = 5^6 mod 23
  = 8

B = g^b mod p
  = 5^16 mod 23
  = 3

Alice:
s = B^a mod 23
  = 3^6 mod 23
  = 16
  
Bob:
s = A^b mod 23
  = 8^16 mod 23
  = 16



1.4. (10 points) A) If anyone can solve the Discrete Logarithm Problem (DLP), they can
easily break this cipher. Explain which cipher and why this is the case. B) If anyone can
solve the integer factorization problem, they can easily break this cipher. Explain which
cipher and why this is the case. Focus on the ciphers discussed in the class.

> A) The cipher that can be easily broken if someone solves the Discrete Logarithm Problem (DLP) is the Diffie-Hellman key exchange and the Elliptic Curve Cryptography (ECC), along with cryptosystems like ElGamal encryption. The Diffie-Hellman key exchange is a method of securely exchanging cryptographic keys over a public channel and is one of the first public-key protocols invented. Similarly, ECC is a public key encryption technique based on elliptic curve theory that can be used to create faster, smaller, and more efficient cryptographic keys. ElGamal encryption is another cryptographic system that relies on the discrete logarithm problem for its security.

> The discrete logarithm problem is the mathematical backbone of these systems. It involves finding the exponent x in the equation g^x = h mod p, where g, h, and p are known, and g is a generator of a finite group of order p. In the context of cryptography, this problem is deliberately made difficult to solve to ensure the security of the cryptographic system. If someone were able to efficiently solve the DLP, they could derive the private keys from the public keys in systems like Diffie-Hellman and ECC, allowing them to decrypt messages and forge signatures, effectively breaking the security of these systems.

> B) The cipher that can be easily broken if someone solves the integer factorization problem is the RSA algorithm. RSA (Rivest-Shamir-Adleman) is one of the first public-key cryptosystems and is widely used for secure data transmission. The security of RSA is based on the practical difficulty of factoring the product of two large prime numbers, the factoring problem.

> In RSA, the encryption key is public and it is different from the decryption key which is kept secret (private). A user of RSA creates and then publishes a public key based on two large prime numbers, along with an auxiliary value. The prime numbers must be kept secret. Anyone can use the public key to encrypt a message, but with currently published methods, if the public key is large enough, only someone with knowledge of the prime numbers can feasibly decode the message. If the integer factorization problem could be solved efficiently, an attacker could easily factor the large number that comprises the public key into its two prime factors. This would allow the attacker to derive the private key from the public key, decrypt messages, and break the cipher.



1.5. (10 points) Alice publishes her RSA public key: modulus N = 221 (what is p and q?) and
exponent e = 5. Bob wants to send Alice the message m=50. What ciphertext does Bob send
to Alice? Show the steps taken to reach this result.

1. Find the prime factors p and q of the modulus N:
   - N = 221 = 13 × 17
   - So, p = 13 and q = 17

2. Calculate the totient function φ(N):
   - φ(N) = (p - 1)(q - 1)
   - φ(221) = (13 - 1)(17 - 1)
   - φ(221) = 12 × 16 = 192

3. Check if the public exponent e is valid:
   - e should be coprime with φ(N)
   - gcd(e, φ(N)) should be 1
   - gcd(5, 192) = 1, so e = 5 is a valid public exponent

4. Encrypt the message m using the public key (N, e):
   - Ciphertext c ≡ m^e (mod N)
   - c ≡ 50^5 (mod 221)
   - 50^5 = 312,500,000
   - c ≡ 50^5 (mod 221)
   - So, the ciphertext c = 33

Bob will send the ciphertext c = 33 to Alice.




1.6. (10 points) Make a 3AES algorithm using the original AES-128 algorithm (similar to
how 3DES is built using DES). Discuss its properties (min and max key sizes, block size).
Also, analyze its robustness against brute-force attacks (hint: birthday attack).


## 3AES Algorithm

The 3AES algorithm applies the AES-128 cipher three times with different 128-bit keys. The encryption process is as follows:

1. Encrypt the plaintext block using AES-128 with key $K_1$, resulting in intermediate ciphertext $C_1$.
2. Decrypt $C_1$ using AES-128 with key $K_2$, resulting in intermediate plaintext $P_2$.
3. Encrypt $P_2$ using AES-128 with key $K_3$, resulting in the final ciphertext $C_3$.

The decryption process applies the inverse operations in reverse order.

## Properties

- **Key sizes:** The 3AES algorithm uses three 128-bit keys, so the total key size is 384 bits. The minimum and maximum key sizes are both 384 bits.

- **Block size:** Since AES-128 operates on 128-bit blocks, the block size of 3AES is also 128 bits.

## Robustness Against Attacks

### Brute-force Attack

In a brute-force attack, the attacker tries all possible key combinations until the correct key is found. For 3AES with a 384-bit key, the number of possible keys is $2^{384}$. This is an extremely large keyspace, making brute-force attacks infeasible with current computing power.

### Birthday Attack

In the case of 3AES, the attacker would need to find a collision in the 128-bit block size.

According to the birthday paradox, the probability of a collision after $q$ queries is approximately:

$P(q) \approx 1 - e^{-q^2/2n}$

where $n = 2^{128}$ (the number of possible outputs).

To have a 50% probability of finding a collision, the number of queries needed is:

$q \approx \sqrt{2n \cdot \ln(2)} \approx 2^{64}$

This is still an extremely large number of queries, making the birthday attack impractical against 3AES.

In conclusion, the 3AES algorithm, with its 384-bit key and 128-bit block size, provides strong security against brute-force and birthday attacks. However, it is important to note that the increased key size comes with a performance cost, as the encryption and decryption processes are three times slower compared to the original AES-128.



Section 2: “Analyze and Create” Questions

2.1. Design an Authentication Mechanism (40 points): You are designing a variation of the
Kerberos authentication system (like Kerberos) for an organization. Users must be authenticated
before accessing classified documents on server V. All entities within the original Kerberos
protocol exist here (Client C, Service Server V, Authentication Server AS, Ticket-granting server
TGS). Still, instead of using pre-shared symmetric keys and symmetric ciphers, we want to use
public/private keys and public-key (asymmetric) ciphers to exchange the session keys (KC, TGS:
Session key between client and TGS and KC, V: Session key between client and service server V).
Each entity (C, V, AS, TGS) has a pair of public/private keys. The public key of AS is known to
all other entities, but only AS knows the public keys of C, V, and TGS (each entity knows its
own public key as well). The private keys are securely stored on the entities, and each entity
knows its own private key. The client machine uses passwords to initiate the authentication
process, but the actual authentication and session key exchange must rely on public-key
cryptography. Only the AS is able to verify whether a given password is correct or not
(centralized authentication) using a centralized credentials database. Still, no symmetric ciphers
are used in the process.

The entities will use RSA as the public key cipher for communication.

A) Using what you learned about Kerberos and public-key ciphers, design this protocol.
Formally and informally define every communication step and use discussed notations (in
our discussion on Kerberos) to show what specific messages are exchanged between which
entities and why.


B) Discuss how your protocol is resistant to replay attacks and satisfies properties like key
freshness and forward/backward secrecy in your design.

Replay Attack Resistance:
The protocol is resistant to replay attacks due to the use of session keys and tickets that are specific to each authentication session. If an attacker intercepts a message and tries to replay it later, the following measures prevent the attack from succeeding:

1. The ticket $E_{PR_{AS}}(C, TGS, K_{C,TGS})$ is encrypted with the $AS$'s private key, which only the $AS$ can decrypt. If an attacker replays this ticket, the $TGS$ will detect that the ticket is not fresh and reject it.

2. The ticket $E_{PR_{TGS}}(C, V, K_{C,V})$ is encrypted with the $TGS$'s private key, which only the $TGS$ can decrypt. If an attacker replays this ticket, the server $V$ will detect that the ticket is not fresh and reject it.

3. The session keys $K_{C,TGS}$ and $K_{C,V}$ are unique for each authentication session. Even if an attacker replays an old session key, it will not be accepted by the $TGS$ or $V$ because they expect a fresh session key for each new session.

Key Freshness:
The protocol ensures key freshness by generating new session keys for each authentication session. The $AS$ generates a new $K_{C,TGS}$ for each ticket granting ticket (TGT) request, and the $TGS$ generates a new $K_{C,V}$ for each service ticket request. This ensures that each session uses a unique key, preventing the use of old or stale keys.

Forward Secrecy:
Forward secrecy is maintained because the session keys are not derived from any long-term keys. Instead, they are randomly generated by the $AS$ and $TGS$ for each session. If an attacker compromises a session key, they cannot use it to decrypt any future communication because each new session will use a different session key.

Backward Secrecy:
Backward secrecy is also maintained due to the use of unique session keys for each authentication session. If an attacker compromises a session key, they cannot use it to decrypt any past communication because each previous session used a different session key.

In the context of the office building analogy:
- Replay attack resistance is like an attacker trying to use an old access pass (ticket) to enter the building or secure room. The security guard and floor manager will recognize that the pass is not fresh and deny access.

- Key freshness is like the security guard and floor manager creating new, unique access passes (session keys) for each employee's visit, ensuring that old passes cannot be reused.

- Forward secrecy is like an attacker obtaining an employee's access pass for a specific visit. They cannot use this pass to access the building or secure room in the future because new passes are issued for each visit.
	
- Backward secrecy is like an attacker obtaining an employee's access pass for a specific visit. They cannot use this pass to determine which rooms the employee accessed in the past because each previous visit used a different, unique access pass.

C) Compare your protocol to the original Kerberos protocol. How did the use of public-key
ciphers impact your design?

### Similarities:

 - 1. The overall structure of the protocol remains the same, with the client authenticating through the $AS$ and $TGS$ to obtain a service ticket for accessing the server $V$.
 - 2. The protocol still relies on a centralized authentication server ($AS$) to verify the client's identity and a ticket granting server ($TGS$) to issue service tickets.
 - 3. The use of tickets and session keys to establish secure communication channels between the client and the servers is maintained.

### Differences and Impact of Public-Key Ciphers:

 - 1. Key Distribution: In the original Kerberos protocol, symmetric keys are pre-shared between the client and $AS$, $AS$ and $TGS$, and $TGS$ and $V$. With public-key ciphers, the need for pre-shared symmetric keys is eliminated. Instead, each entity has a pair of public/private keys, with the public keys known to the $AS$. This simplifies key distribution and management.
 - 2. Authentication: In the original protocol, the client's identity is verified by the $AS$ using a pre-shared symmetric key. In the modified protocol, the client's password is encrypted with the $AS$'s public key, allowing the $AS$ to authenticate the client without needing a pre-shared key. This enhances security by eliminating the need to store long-term symmetric keys.
 - 3. Ticket Granting: The original protocol uses symmetric keys shared between the $AS$ and $TGS$, and between the $TGS$ and $V$ to encrypt the tickets. The modified protocol uses the private keys of the $AS$ and $TGS$ to encrypt the tickets, which can be verified by the $TGS$ and $V$ using the corresponding public keys. This eliminates the need for shared symmetric keys between these entities.
 - 4. Performance: Public-key cryptography is generally more computationally expensive than symmetric-key cryptography. As a result, the modified protocol may have higher computational overhead compared to the original Kerberos protocol. However, this impact can be mitigated by using efficient public-key algorithms and optimizing the implementation.

Make your assumptions if you believe key information is not available, but clearly explain and
justify them in your response. Note that you just need to design the protocol, but no
implementation is required.

### Assumptions:

 - 1. The $AS$ securely stores and manages the public keys of all entities ($C$, $V$, and $TGS$) in addition to the credentials database for password verification.

 - 2. The private keys are securely stored by each entity and are not compromised. If a private key is compromised, the security of the entire system could be jeopardized.

 - 3. The communication channels between the entities are secure, and there is a mechanism to prevent tampering and eavesdropping of messages.

In conclusion, the use of public-key ciphers in the modified Kerberos protocol eliminates the need for pre-shared symmetric keys, simplifies key distribution, and enhances authentication security. However, it may introduce additional computational overhead compared to the original protocol. The assumptions made in the design, such as secure key management and storage, are critical to maintaining the security of the system.
 
### Version 2

Notation:
- $C$: Client
- $V$: Service Server
- $AS$: Authentication Server
- $TGS$: Ticket-granting Server
- $PU_X$: Public key of entity $X$
- $PR_X$: Private key of entity $X$
- $E_{PU_X}(M)$: Message $M$ encrypted with the public key of entity $X$
- $E_{PR_X}(M)$: Message $M$ encrypted with the private key of entity $X$
- $K_{C,TGS}$: Session key between client and TGS
- $K_{C,V}$: Session key between client and service server $V$

Authentication process:
1. $C \rightarrow AS$: $C, E_{PU_{AS}}(password)$
   - Client sends its identity and password encrypted with the public key of $AS$.

2. $AS \rightarrow C$: $E_{PU_C}(K_{C,TGS}), E_{PU_{TGS}}(C, K_{C,TGS})$
   - $AS$ verifies the password using the centralized credentials database.
   - If the password is correct, $AS$ generates a session key $K_{C,TGS}$ for communication between $C$ and $TGS$.
   - $AS$ sends the session key $K_{C,TGS}$ encrypted with the public key of $C$ and a ticket containing $C$'s identity and $K_{C,TGS}$ encrypted with the public key of $TGS$.

3. $C \rightarrow TGS$: $E_{PU_{TGS}}(C, K_{C,TGS}), E_{PR_C}(timestamp)$
   - Client decrypts the session key $K_{C,TGS}$ using its private key.
   - Client sends the ticket (containing $C$'s identity and $K_{C,TGS}$) encrypted with $TGS$'s public key and a timestamp encrypted with $C$'s private key.

4. $TGS \rightarrow C$: $E_{PU_C}(K_{C,V}), E_{PU_V}(C, K_{C,V})$
   - $TGS$ decrypts the ticket using its private key to obtain $C$'s identity and $K_{C,TGS}$.
   - $TGS$ verifies the timestamp by decrypting it with $C$'s public key.
   - If the timestamp is valid, $TGS$ generates a new session key $K_{C,V}$ for communication between $C$ and $V$.
   - $TGS$ sends the session key $K_{C,V}$ encrypted with $C$'s public key and a ticket containing $C$'s identity and $K_{C,V}$ encrypted with $V$'s public key.

5. $C \rightarrow V$: $E_{PU_V}(C, K_{C,V}), E_{PR_C}(timestamp)$
   - Client decrypts the session key $K_{C,V}$ using its private key.
   - Client sends the ticket (containing $C$'s identity and $K_{C,V}$) encrypted with $V$'s public key and a new timestamp encrypted with $C$'s private key.

6. $V \rightarrow C$: $E_{K_{C,V}}(timestamp+1)$
   - $V$ decrypts the ticket using its private key to obtain $C$'s identity and $K_{C,V}$.
   - $V$ verifies the timestamp by decrypting it with $C$'s public key.
   - If the timestamp is valid, $V$ increments the timestamp and encrypts it with the session key $K_{C,V}$ to prove its identity to $C$.

In this variation, the session keys $K_{C,TGS}$ and $K_{C,V}$ are exchanged using public-key cryptography (RSA) instead of symmetric ciphers. The private keys are securely stored on each entity, and the public keys are used for encryption. The $AS$ is responsible for verifying the password using a centralized credentials database, but no symmetric ciphers are used in the process.


Informal:

Imagine a high-security office building where employees (clients) need to access classified documents stored in a secure room (service server V). To enter the building and the secure room, employees must go through a two-step authentication process.

At the entrance of the building, there is a security guard (authentication server AS) who verifies the employee's identity. Each employee has a unique ID card (public key) and a corresponding secret code (private key). The security guard has a master list of all employee ID cards and a special machine that can read the secret codes.

When an employee approaches the security guard, they present their ID card and whisper their password to the guard. The guard uses the special machine to verify the password and, if correct, gives the employee two envelopes. The first envelope contains a temporary access code (session key) for the employee to use with the floor manager (ticket-granting server TGS). This envelope can only be opened by the employee using their secret code. The second envelope is sealed and addressed to the floor manager, containing the employee's identity and the same temporary access code.

The employee then goes to the floor where the secure room is located and presents the sealed envelope to the floor manager. The floor manager opens the envelope, verifies the employee's identity, and checks the temporary access code. If everything is valid, the floor manager gives the employee two new envelopes. The first envelope contains another temporary access code for the employee to use with the secure room. The second envelope is sealed and addressed to the secure room, containing the employee's identity and the new temporary access code.

Finally, the employee approaches the secure room and presents the sealed envelope to the room's security system. The security system opens the envelope, verifies the employee's identity, and checks the temporary access code. If everything is valid, the security system allows the employee to enter the room and access the classified documents.

Throughout this process, the employee's secret code (private key) is never shared, and all communication between the employee, security guard, floor manager, and secure room is done using the employee's ID card (public key) and the respective ID cards of the other entities. This ensures that only authorized employees can access the classified documents and that the communication remains secure.
