## CRYPTOGRAPHY
## HILL CIPHER EX. NO: 1(C) AIM:

## IMPLEMENTATION OF HILL CIPHER

## AIM:
To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:
Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B = 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, against modulus 26. To decrypt the message, each block is multiplied by the inverse of the m trix used for
encryption. The matrix usedfor encryption is the cipher key, and it shold be chosenrandomly from the set of invertible n × n matrices (modulo 26).

## ALGORITHM:
STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix. STEP-4: Multiply the two matrices to obtain the cipher text of length three. STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int keymat[3][3] = {
    { 1, 2, 1 },
    { 2, 3, 2 },
    { 2, 2, 1 }
};

int invkeymat[3][3] = {
    { -1, 0, 1 },
    { 2, -1, 0 },
    { -2, 2, -1 }
};

char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

// Function to encode 3 letters using Hill Cipher
void encode(char a, char b, char c, char *ret) {
    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    int x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    int y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    int z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];

    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}

// Function to decode 3 letters using Hill Cipher inverse matrix
void decode(char a, char b, char c, char *ret) {
    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    int x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    int y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    int z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];

    // Adjust for negative values
    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
}

int main() {
    char msg[1000] = "Azeem's Kingdom";
    char enc[1000] = "";
    char dec[1000] = "";
    char buffer[4];
    int n;

    printf("Simulation of Hill Cipher\n");
    printf("\nInput message: %s\n", msg);

    // Convert message to uppercase
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }

    // Pad the message with 'X' if length not divisible by 3
    n = strlen(msg) % 3;
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }

    printf("\nPadded message: %s\n", msg);

    // Encode
    for (int i = 0; i < strlen(msg); i += 3) {
        encode(msg[i], msg[i + 1], msg[i + 2], buffer);
        strcat(enc, buffer);
    }

    printf("\nEncoded message: %s\n", enc);

    // Decode
    for (int i = 0; i < strlen(enc); i += 3) {
        decode(enc[i], enc[i + 1], enc[i + 2], buffer);
        strcat(dec, buffer);
    }

    printf("\nDecoded message: %s\n", dec);
    return 0;
}

```
## OUTPUT:
![Screenshot 2025-04-07 091551](https://github.com/user-attachments/assets/4bbb1dc1-41f2-4a47-864f-9c543d90e30e)

## RESULT:
Thus The Hill Cipher Program is completed successfully.
