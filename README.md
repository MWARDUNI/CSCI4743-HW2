# CSCI4743-HW2

Here's a variation of the Kerberos authentication system using public/private keys and asymmetric ciphers for exchanging session keys:

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
