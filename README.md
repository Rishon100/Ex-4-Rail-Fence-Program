# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
# ✅ Encrypt using Rail Fence Cipher
def encrypt_rail_fence(text, rails):
    length = len(text)

    # create rail matrix and initialize with 0
    code = [[0 for _ in range(length)] for _ in range(rails)]

    count = 0
    j = 0

    # place characters in zig-zag
    while j < length:
        if count % 2 == 0:  # moving down
            for i in range(rails):
                if j < length:
                    code[i][j] = text[j]
                    j += 1
        else:  # moving up
            for i in range(rails - 2, 0, -1):
                if j < length:
                    code[i][j] = text[j]
                    j += 1
        count += 1

    # read row-wise
    encrypted = ""
    for i in range(rails):
        for j in range(length):
            if code[i][j] != 0:
                encrypted += code[i][j]

    return encrypted


# ✅ Decrypt using Rail Fence Cipher
def decrypt_rail_fence(text, rails):
    length = len(text)

    # create rail matrix
    code = [[0 for _ in range(length)] for _ in range(rails)]

    count = 0
    j = 0

    # mark positions with 1
    while j < length:
        if count % 2 == 0:
            for i in range(rails):
                if j < length:
                    code[i][j] = 1
                    j += 1
        else:
            for i in range(rails - 2, 0, -1):
                if j < length:
                    code[i][j] = 1
                    j += 1
        count += 1

    # fill cipher text row-wise
    pos = 0
    for i in range(rails):
        for j in range(length):
            if code[i][j] == 1:
                code[i][j] = text[pos]
                pos += 1

    # read zig-zag to decrypt
    decrypted = ""
    count = 0
    j = 0
    pos = 0

    while j < length:
        if count % 2 == 0:
            for i in range(rails):
                if j < length and code[i][j] != 0:
                    decrypted += code[i][j]
                    j += 1
        else:
            for i in range(rails - 2, 0, -1):
                if j < length and code[i][j] != 0:
                    decrypted += code[i][j]
                    j += 1
        count += 1

    return decrypted


# ✅ Main
print("Simulating Rail Fence Cipher")
text = input("Enter a Secret Message: ")
rails = int(input("Enter number of rails: "))

encrypted = encrypt_rail_fence(text, rails)
print("Encrypted Message:", encrypted)

decrypted = decrypt_rail_fence(encrypted, rails)
print("Decrypted Message:", decrypted)
```
# OUTPUT

<img width="470" height="245" alt="image" src="https://github.com/user-attachments/assets/86f97abb-0ad8-4d40-854d-572155766ab9" />

# RESULT

The implementation of rail fence transposition technique using c program is successful.

