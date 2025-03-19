# Cryptography---19CS412-classical-techqniques
# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
PROGRAM:
```C
CaearCipher.
 
  #include <stdio.h>
 #include <string.h>
 #include <ctype.h>
 int main() {
 char plain[100], cipher[100];
 int key, i, length;
 printf("Enter the plain text: ");
 scanf("%s", plain);
printf("Enter the key value: ");
 scanf("%d", &key);
 printf("\nPLAIN TEXT: %s", plain);
 printf("\nENCRYPTED TEXT: ");
 length = strlen(plain);
 for (i = 0; i < length; i++) {
 cipher[i] = plain[i] + key;
 // Handling uppercase letters
 if (isupper(plain[i]) && cipher[i] > 'Z') {
 cipher[i] = cipher[i]- 26;
 }
 // Handling lowercase letters
 if (islower(plain[i]) && cipher[i] > 'z') {
 cipher[i] = cipher[i]- 26;
 }
 printf("%c", cipher[i]);
 }
 cipher[length] = '\0'; // Null-terminate the cipher text string
 printf("\nDECRYPTED TEXT: ");
 for (i = 0; i < length; i++) {
 plain[i] = cipher[i]- key;
 // Handling uppercase letters
 if (isupper(cipher[i]) && plain[i] < 'A') {
 plain[i] = plain[i] + 26;
 }
 // Handling lowercase letters
if (islower(cipher[i]) && plain[i] < 'a') {
 plain[i] = plain[i] + 26;
 }
 printf("%c", plain[i]);
 }
 plain[length] = '\0'; // Null-terminate the plain text string
 return 0;
 }
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/be61696b-692c-4d1f-a1d3-692acc086813)

OUTPUT:
Simulating Caesar Cipher


Input : Anna University
Encrypted Message : Dqqd Xqlyhuvlwb Decrypted Message : Anna University

## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
```c
 
#include<stdio.h>
#include<string.h>
#include<ctype.h>
#define MX 5

void playfair(char ch1, char ch2, char key[MX][MX])
{
    int i, j, w, x, y, z;
    FILE *out;
    if ((out = fopen("cipher.txt", "a+")) == NULL)
    {
        printf("File Corrupted.");
    }
    for (i = 0; i < MX; i++)
    {
        for (j = 0; j < MX; j++)
        {
            if (ch1 == key[i][j])
            {
                w = i;
                x = j;
            }
            else if (ch2 == key[i][j])
            {
                y = i;
                z = j;
            }
        }
    }
    if (w == y)
    {
        x = (x + 1) % 5;
        z = (z + 1) % 5;
        printf("%c%c", key[w][x], key[y][z]);
        fprintf(out, "%c%c", key[w][x], key[y][z]);
    } 
    else if (x == z) 
    {
        w = (w + 1) % 5;
        y = (y + 1) % 5;
        printf("%c%c", key[w][x], key[y][z]);
        fprintf(out, "%c%c", key[w][x], key[y][z]);
    } 
    else 
    {
        printf("%c%c", key[w][z], key[y][x]);
        fprintf(out, "%c%c", key[w][z], key[y][x]);
    }
    fclose(out);
}

int main() 
{
    int i, j, k = 0, l, m = 0, n;
    char key[MX][MX], keyminus[25], keystr[10], str[25] = {0};
    char alpa[26] = {'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    printf("\nEnter key: ");
    fgets(keystr, sizeof(keystr), stdin);
    keystr[strcspn(keystr, "\n")] = 0; // Remove newline character

    printf("\nEnter the plain text: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; // Remove newline character
    n = strlen(keystr);
    for (i = 0; i < n; i++) 
    {
        if (keystr[i] == 'j') keystr[i] = 'i';
        else if (keystr[i] == 'J') keystr[i] = 'I';
        keystr[i] = toupper(keystr[i]);
    }
    for (i = 0; i < strlen(str); i++) {
        if (str[i] == 'j') str[i] = 'i';
        else if (str[i] == 'J') str[i] = 'I';
        str[i] = toupper(str[i]);
    }
    j = 0;
    for (i = 0; i < 26; i++)
    {
        for (k = 0; k < n; k++)
        {
            if (keystr[k] == alpa[i]) break;
            else if (alpa[i] == 'J') break;
        }
        if (k == n)
        {
            keyminus[j] = alpa[i];
            j++;
        }
    }
    k = 0;
    for (i = 0; i < MX; i++) 
    {
        for (j = 0; j < MX; j++)
        {
            if (k < n)
            {
                key[i][j] = keystr[k];
                k++;
            } 
            else
            {
                key[i][j] = keyminus[m];
                m++;
            }
            printf("%c ", key[i][j]);
        }
        printf("\n");
    }
    printf("\n\nEntered text :%s\nCipher Text :",str);
    for (i = 0; i < strlen(str); i++) 
    {
        if (str[i] == 'J') str[i] = 'I';
        if (str[i + 1] == '\0') playfair(str[i], 'X', key);
        else
        {
            if (str[i + 1] == 'J') str[i + 1] = 'I';
            if (str[i] == str[i + 1]) playfair(str[i], 'X', key);
            else 
            {
                playfair(str[i], str[i + 1], key);
                i++;
            }
        }
  
    }
     printf("\nDecrypted text:%s",str);
    return 0;
}
```

## OUTPUT:
 
![image](https://github.com/user-attachments/assets/656d5dbb-9087-4cf0-a31a-9e58a07a258d)


## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
PROGRAM:
```C
#include <stdio.h>
 #include <string.h>
 int main() {
 unsigned int a[3][3] = {{6, 24, 1}, {13, 16, 10}, {20, 17, 15}};
 unsigned int b[3][3] = {{8, 5, 10}, {21, 8, 21}, {21, 12, 8}};
 int i, j, t = 0;
 unsigned int c[3], d[3];
 char msg[4]; // buffer for exactly 3 characters plus null terminator
 printf("Enter plain text (3 letters): ");
scanf("%3s", msg); // ensure input is limited to 3 characters
 // Ensure the message has exactly 3 characters
 if (strlen(msg) != 3) {
 printf("Error: The plain text must be exactly 3 letters.\n");
 return 1;
 }
 // Convert plain text to numerical values (A=0, B=1, ..., Z=25)
 for (i = 0; i < 3; i++) {
 c[i] = msg[i]- 'A';
 printf("%d ", c[i]); // display numerical representation of characters
 }
 // Encrypt the message using matrix 'a'
 for (i = 0; i < 3; i++) {
 t = 0;
 for (j = 0; j < 3; j++) {
 t += a[i][j] * c[j];
 }
 d[i] = t % 26; // mod 26 for alphabet range
 }
 // Output encrypted cipher text
 printf("\nEncrypted Cipher Text: ");
 for (i = 0; i < 3; i++) {
 printf("%c", d[i] + 'A');
 }
 // Decrypt the message using matrix 'b'
 for (i = 0; i < 3; i++) {
 t = 0;
for (j = 0; j < 3; j++) {
 t += b[i][j] * d[j];
 }
 c[i] = t % 26; // mod 26 for alphabet range
 }
 // Output decrypted cipher text
 printf("\nDecrypted Cipher Text: ");
 for (i = 0; i < 3; i++) {
 printf("%c", c[i] + 'A');
 }
 getchar(); // Use getchar() to wait for input
 return 0;
 }
 ```

## OUTPUT:
  ![image](https://github.com/user-attachments/assets/d47c96a2-619b-4c2e-aadd-0fec73717053)

## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
```c
PROGRAM:
#include <stdio.h>
 #include <ctype.h>
 #include <string.h>
 #include <stdlib.h>
 void encipher();
 void decipher();
int main() {
 int choice;
 while (1) {
 printf("\n1. Encrypt Text");
 printf("\t2. Decrypt Text");
 printf("\t3. Exit");
 printf("\n\nEnter Your Choice: ");
 scanf("%d", &choice);
 if (choice == 3)
 return 0; // Proper exit from main()
 else if (choice == 1)
 encipher();
 else if (choice == 2)
 decipher();
 else
 printf("Please Enter a Valid Option.\n");
 }
 }
 void encipher() {
 unsigned int i, j;
 char input[50], key[10];
 printf("\n\nEnter Plain Text: ");
 scanf("%s", input);
 printf("\nEnter Key Value: ");
 scanf("%s", key);
 printf("\nResultant Cipher Text: ");
for (i = 0, j = 0; i < strlen(input); i++, j++) {
 if (j >= strlen(key)) {
 j = 0; // Reset key index if it exceeds the key length
 }
 printf("%c", 65 + (((toupper(input[i])- 65) + (toupper(key[j])- 65)) % 26));
 // Encryption formula
 }
 printf("\n"); // New line after output
 }
 void decipher() {
 unsigned int i, j;
 char input[50], key[10];
 int value;
 printf("\n\nEnter Cipher Text: ");
 scanf("%s", input);
 printf("\nEnter the Key Value: ");
 scanf("%s", key);
 printf("\nDecrypted Plain Text: ");
 for (i = 0, j = 0; i < strlen(input); i++, j++) {
 if (j >= strlen(key)) {
 j = 0; // Reset key index if it exceeds the key length
 }// Decryption formula
 value = (toupper(input[i])- 65)- (toupper(key[j])- 65);
 if (value < 0) {
 value += 26; // Correct the negative wrap-around in alphabet
 }
printf("%c", 65 + (value % 26));
 }
 printf("\n"); // New line after output
 }
 ```

## OUTPUT:
 ![image](https://github.com/user-attachments/assets/6b1948f0-a435-4a6d-b89b-8a33be729037)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:

PROGRAM:
```c
 #include <stdio.h>
 #include <string.h>
 int main() {
 int i, j, k, l;
 char a[20], c[20], d[20];
 printf("\n\t\tRAIL FENCE TECHNIQUE\n");
 // Safely getting input string using fgets instead of gets
 printf("\nEnter the input string: ");
 fgets(a, sizeof(a), stdin);
 // Removing the newline character if it exists
a[strcspn(a, "\n")] = '\0';
 l = strlen(a); // Get the length of the input string
 // Rail fence encryption: first collect even indices, then odd
 for (i = 0, j = 0; i < l; i++) {
 if (i % 2 == 0) {
 c[j++] = a[i];
 }
 }
 for (i = 0; i < l; i++) {
 if (i % 2 == 1) {
 c[j++] = a[i];
 }
 }
 c[j] = '\0'; // Null-terminate the encrypted string
 printf("\nCipher text after applying rail fence: %s\n", c);
 // Rail fence decryption
 if (l % 2 == 0) {
 k =l / 2;
 } else {
 k =(l / 2) + 1;
 }
 // Reconstructing the original text
 for (i = 0, j = 0; i < k; i++) {
 d[j] = c[i];
 j += 2;
 }
 for (i = k, j = 1; i < l; i++) {
d[j] = c[i];
 j += 2;
 }
 d[l] = '\0'; // Null-terminate the decrypted string
 printf("\nText after decryption: %s\n", d);
 return 0; // Properly return from main
 }
 ```
## OUTPUT:
 
![image](https://github.com/user-attachments/assets/1b0a429d-1ba5-4ae6-945f-7e673bc278bd)

## RESULT:
The program is executed successfully
