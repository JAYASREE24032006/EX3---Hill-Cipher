# EX3 - HILL CIPHER
## AIM :
To implement a program to encrypt a plain text and decrypt a cipher text using Hill Cipher substitution technique.
## THEORY :
The Hill cipher is a polygraphic substitution cipher that encrypts blocks of plaintext using linear algebra. By representing letters as numerical vectors and applying an invertible key matrix, it produces ciphertext. This method enhances security over simple ciphers but is vulnerable to known-plaintext attacks and requires careful key management.
## ALGORITHM :
### STEP 1 :
Design of Hill Cipher algorithnm

### STEP 2 :
Implementation using C or pyhton code

### STEP 3 :
Testing algorithm with different key values. 

## PROGRAM :
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
void encode(char a, char b, char c, char ret[])
{
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;
    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];
    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}
void decode(char a, char b, char c, char ret[])
{
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;
    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];
    ret[0] = key[(x % 26 < 0) ? (26 + x % 26) : (x % 26)];
    ret[1] = key[(y % 26 < 0) ? (26 + y % 26) : (y % 26)];
    ret[2] = key[(z % 26 < 0) ? (26 + z % 26) : (z % 26)];
    ret[3] = '\0';
}
int main() 
{
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;
    strcpy(msg, "JAYASREE");
    printf("Input message : %s\n", msg);
    for (int i = 0; i < strlen(msg); i++) 
    {
        msg[i] = toupper(msg[i]);
    }
    n = strlen(msg) % 3;
    if (n != 0)
    {
        for (int i = 1; i <= (3 - n); i++) 
        {
            strcat(msg, "X");
        }
    }
    printf("Padded message : %s\n", msg);
    for (int i = 0; i < strlen(msg); i += 3) 
    {
        char a = msg[i];
        char b = msg[i + 1];
        char c = msg[i + 2];
        char encoded[4];
        encode(a, b, c, encoded);
        strcat(enc, encoded);
    }
    printf("Encoded message : %s\n", enc);
    for (int i = 0; i < strlen(enc); i += 3) 
    {
        char a = enc[i];
        char b = enc[i + 1];
        char c = enc[i + 2];
        char decoded[4];
        decode(a, b, c, decoded);
        strcat(dec, decoded);
    }
    printf("Decoded message : %s\n", dec);
    return 0;
}
```

## OUTPUT :
![image](https://github.com/user-attachments/assets/cbb160b7-210c-442c-915b-0255cda42ce6)



## RESULT :
The program to encrypt a plain text and decrypt a cipher text using Hill Cipher substitution technique is executed successfully.
