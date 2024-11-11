# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC
## DATE:17.10.2024
## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)

## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.
2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.
3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).
4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.
5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```
from tinyec import registry
import secrets

def generate_public_key(private_key, curve):
    public_key = private_key * curve.g
    return public_key

def ecc_diffie_hellman():
    curve_name = input("Enter the name of the elliptic curve (e.g., 'brainpoolP256r1'): ")
    curve = registry.get_curve(curve_name)

    private_key_a = int(input("User A, enter your private key (a large integer): "))
    public_key_a = generate_public_key(private_key_a, curve)
    print(f"User A's Public Key: ({public_key_a.x}, {public_key_a.y})")

    private_key_b = int(input("User B, enter your private key (a large integer): "))
    public_key_b = generate_public_key(private_key_b, curve)
    print(f"User B's Public Key: ({public_key_b.x}, {public_key_b.y})")

    shared_secret_a = private_key_a * public_key_b  # User A's computation
    shared_secret_b = private_key_b * public_key_a  # User B's computation
    print(f"\nUser A's Shared Secret: ({shared_secret_a.x}, {shared_secret_a.y})")
    print(f"User B's Shared Secret: ({shared_secret_b.x}, {shared_secret_b.y})")

    if shared_secret_a == shared_secret_b:
        print("\nThe shared secret key has been successfully established!")
    else:
        print("\nError: The shared secrets do not match.")

ecc_diffie_hellman()

```
## Output:
![image](https://github.com/user-attachments/assets/1460637e-3806-4d22-a0b3-93207784fc5f)

## Result:
The program is executed successfully
