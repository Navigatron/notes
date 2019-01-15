[up](../index.md)

## ssh

### ssh-trans

connect to the server and verify the server's identity. Form the Tunnel.

### ssh-auth

Authenticate the Client, via password or keys. Server opens tunnel on its end.

- password
    - not recommended
- RSA keys
    - private key
    - public key

1. Client asks to connet
2. Server sends 'challenge'
3. Client does something with it and it's private key
4. Server checks against something involving a public key

Those last two steps aren't very well explained.

### ssh-conn

Expose functionality so that things can use the tunnel we've created.

### sshd

The server daemon that listens for new connections.

### Applications
- SFTP - secure file transfer
- SHTTP - web stuff
- SCP - secure copy

## Reading

SSH second edition  
Chapters 1, 2, and 3  
Section 9.4: X forwarding
