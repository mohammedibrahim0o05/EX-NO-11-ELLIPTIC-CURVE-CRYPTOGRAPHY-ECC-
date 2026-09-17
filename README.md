# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC

### Name Mohammed Ibrahim MN 
### Roll No 212223100034

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
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y


def inverse(a, p):
    a = (a % p + p) % p

    for i in range(1, p):
        if (a * i) % p == 1:
            return i

    return -1


def add(P, Q, a, p):
    if P.x == Q.x and P.y == Q.y:
        l = ((3 * P.x * P.x + a) * inverse(2 * P.y, p)) % p
    else:
        l = ((Q.y - P.y) * inverse(Q.x - P.x, p)) % p

    l = (l % p + p) % p

    x = (l * l - P.x - Q.x) % p
    y = (l * (P.x - x) - P.y) % p

    return Point(x, y)


def multiply(P, k, a, p):
    R = P

    for i in range(k - 1):
        R = add(R, P, a, p)

    return R


print("ECC Key Exchange")

p = int(input("Enter prime number: "))
a = int(input("Enter value of a: "))
gx = int(input("Enter Gx: "))
gy = int(input("Enter Gy: "))

Allahbakash = int(input("Enter Allahbakash private key: "))
V = int(input("Enter V private key: "))

G = Point(gx, gy)

# Generate public keys
pubAllahbakash = multiply(G, Allahbakash, a, p)
pubV = multiply(G, V, a, p)

# Generate shared secrets
secret1 = multiply(pubV, Allahbakash, a, p)
secret2 = multiply(pubAllahbakash, V, a, p)

print("\nShared Secret by Allahbakash: ({}, {})".format(
    secret1.x, secret1.y
))

print("Shared Secret by V: ({}, {})".format(
    secret2.x, secret2.y
))

```



## Output:
<img width="1470" height="895" alt="image" src="https://github.com/user-attachments/assets/fa2efc40-4e65-468d-9dd0-c145b842736f" />



## Result:
The program is executed successfully

