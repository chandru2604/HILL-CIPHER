# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```
#include <stdio.h>
#include <string.h>

int mod26(int x) {
    return (x % 26 + 26) % 26;
}

/* Function to find multiplicative inverse modulo 26 */
int modInverse(int det) {
    det = mod26(det);
    for (int i = 1; i < 26; i++) {
        if ((det * i) % 26 == 1)
            return i;
    }
    return -1;
}

int main() {
    char plaintext[100], ciphertext[100];
    int key[2][2], invKey[2][2];
    int i;

    printf("Enter plaintext (UPPERCASE, even length): ");
    scanf("%s", plaintext);

    printf("Enter 2x2 key matrix:\n");
    for (i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            scanf("%d", &key[i][j]);
        }
    }

    /* ---------- ENCRYPTION ---------- */
    printf("\nEncrypted Text: ");
    for (i = 0; i < strlen(plaintext); i += 2) {
        int p1 = plaintext[i] - 'A';
        int p2 = plaintext[i + 1] - 'A';

        int c1 = mod26(key[0][0] * p1 + key[0][1] * p2);
        int c2 = mod26(key[1][0] * p1 + key[1][1] * p2);

        ciphertext[i] = c1 + 'A';
        ciphertext[i + 1] = c2 + 'A';

        printf("%c%c", ciphertext[i], ciphertext[i + 1]);
    }
    ciphertext[i] = '\0';

    /* ---------- DECRYPTION ---------- */
    int det = key[0][0] * key[1][1] - key[0][1] * key[1][0];
    int detInv = modInverse(det);

    if (detInv == -1) {
        printf("\n\nKey matrix inverse does not exist!");
        return 0;
    }

    /* Inverse key matrix */
    invKey[0][0] = mod26( detInv * key[1][1]);
    invKey[0][1] = mod26(-detInv * key[0][1]);
    invKey[1][0] = mod26(-detInv * key[1][0]);
    invKey[1][1] = mod26( detInv * key[0][0]);

    printf("\nDecrypted Text: ");
    for (i = 0; i < strlen(ciphertext); i += 2) {
        int c1 = ciphertext[i] - 'A';
        int c2 = ciphertext[i + 1] - 'A';

        int p1 = mod26(invKey[0][0] * c1 + invKey[0][1] * c2);
        int p2 = mod26(invKey[1][0] * c1 + invKey[1][1] * c2);

        printf("%c%c", p1 + 'A', p2 + 'A');
    }

    return 0;
}
```
## OUTPUT
<img width="1763" height="1063" alt="image" src="https://github.com/user-attachments/assets/bc562689-c737-4fa9-a193-1c88039b65ca" />

## RESULT
The program was executed sucessfully
