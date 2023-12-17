# XOR Encryption in C#

XOR encryption, or exclusive OR encryption, stands as one of the fundamental concepts in cryptography. The XOR binary operation, which outputs true (1) for differing bits and false (0) for matching bits, forms the basis of this encryption method.

In the encryption process, XOR is applied bit by bit between each element of the plaintext and a key of equal length. This results in encrypted text that appears random at first glance. The reverse operation, XOR between the encrypted text and the same key, restores the original plaintext.

While XOR encryption offers basic protection against direct reading of plaintext, it's crucial to note that it falls short for real security applications due to inherent vulnerabilities.

## Example in C#: XOR Encryption Implementation

Now, let's delve into the implementation of XOR encryption using the C# programming language. In this example, we'll create a simple function to encrypt and decrypt text using XOR encryption.

> 💡 Apologies for the French texts in my code; it's challenging for me to code in English when including texts in my console.

```csharp
using System;
using System.Text;

class Program
{
    // Main Function
    static void Main()
    {
        while (true)
        {
            Console.WriteLine("1. Chiffrer un texte");
            Console.WriteLine("2. Déchiffrer un texte");
            Console.WriteLine("0. Quitter");
            Console.Write("Choisissez une option : ");

            string choice = Console.ReadLine();

            switch (choice)
            {
                case "1":
                    EncryptText();
                    break;
                case "2":
                    DecryptText();
                    break;
                case "0":
                    Environment.Exit(0);
                    break;
                default:
                    Console.WriteLine("Option non valide. Veuillez réessayer.");
                    break;
            }
        }
    }

    // Text Encryption
    static void EncryptText()
    {
        Console.Clear();
        Console.Write("Entrez le texte à chiffrer : ");
        string text = Console.ReadLine();

        Console.Write("Entrez la clé : ");
        string key = Console.ReadLine();

        string encryptedBinary = EncryptToBinary(text, key);
        Console.WriteLine("Texte chiffré en binaire : " + encryptedBinary);
        Console.WriteLine("Texte chiffré : " + Decrypt(encryptedBinary, key));
    }

    // Text Decryption
    static void DecryptText()
    {
        Console.Clear();
        Console.Write("Entrez le texte à déchiffrer (en binaire) : ");
        string encryptedBinary = Console.ReadLine();

        Console.Write("Entrez la clé : ");
        string key = Console.ReadLine();

        Console.WriteLine("Texte déchiffré : " + Decrypt(encryptedBinary, key));
    }

    // Text to Binary Conversion
    static string StringToBinary(string text)
    {
        StringBuilder binary = new StringBuilder();
        foreach (char c in text)
        {
            binary.Append(Convert.ToString(c, 2).PadLeft(8, '0'));
        }
        return binary.ToString();
    }

    // Binary Encryption
    static string EncryptToBinary(string text, string key)
    {
        StringBuilder encrypted = new StringBuilder();

        for (int i = 0; i < text.Length; i++)
        {
            char xorResult = (char)(text[i] ^ key[i % key.Length]);
            encrypted.Append(Convert.ToString(xorResult, 2).PadLeft(8, '0'));
        }

        return encrypted.ToString();
    }

    // Decryption
    static string Decrypt(string encryptedBinary, string key)
    {
        StringBuilder decryptedText = new StringBuilder();

        for (int i = 0; i < encryptedBinary.Length; i += 8)
        {
            string binaryChunk = encryptedBinary.Substring(i, 8);
            char decryptedChar = (char)Convert.ToByte(binaryChunk, 2);

            // Apply XOR operation with the key to decrypt
            char xorResult = (char)(decryptedChar ^ key[i / 8 % key.Length]);
            decryptedText.Append(xorResult);
        }

        return decryptedText.ToString();
    }
}
```

### Explanation of the Code

1. **Main Function (`Main`):**
    - The `while (true)` loop allows the program to run continuously until the user chooses to exit (option 0).
    - The menu displays options to encrypt (1), decrypt (2), or exit (0).
    - The user inputs their choice, and the `switch` loop directs the program to the appropriate function.

2. **Text Encryption (`EncryptText`):**
    - The user is prompted to input the text to encrypt and the key.
    - The `EncryptToBinary` function is called to perform the encryption.
    - The encrypted text in binary and the decrypted text are displayed.

3. **Text Decryption (`DecryptText`):**
    - The user is prompted to input the encrypted text in binary and the key.
    - The `Decrypt` function is called to perform the decryption.
    - The decrypted text is displayed.

4. **Text to Binary Conversion (`StringToBinary`):**
    - This function takes a text string as input and converts each character into its 8-bit binary representation.
    - This is necessary to handle special characters and individual bytes.

5. **Binary Encryption (`EncryptToBinary`):**
    - For each character in the text, XOR operation is performed with the corresponding character from the key.
    - The result is converted to binary and added to the encrypted binary string.

6. **Decryption (`Decrypt`):**
    - This function takes the encrypted binary string as input and performs decryption by applying XOR operation with the key.
    - The result is converted to characters and added to the decrypted string.

### Usage of Binary Representation

- Text-to-binary conversion is done to handle special characters and ensure each character is represented in 8 bits.
- The reason is simple; after spending several hours trying to make my IDE compatible with special characters, I failed, so I decided to convert to binary.

### Encryption Simulation

1. **Program Launch:**
    - Choose option 1 to encrypt text.
2. **Data Input:**
    - Enter the text to encrypt: `hello`
    - Enter the key: `key`
3. **Encryption Result:**
    - The program displays the encrypted text in binary: `0110110101100101011011000110110001101100`
    - The program also displays the decrypted text: `hello`

    This result is achieved by performing XOR bit-wise operation between each character of "hello" and the key "key".

### Decryption Simulation

1. **Program Launch:**
    - Choose option 2 to decrypt text.
2. **Data Input:**
    - Enter the encrypted text (in binary): `0110110101100101011011000110110001101100`
    - Enter the key: `key`
3. **Decryption Result:**
    - The program displays the decrypted text: `hello`

    Decryption is done by applying the same XOR operation between the encrypted text and the key.

---

## Conclusion

In summary, this project provided an opportunity to explore XOR encryption through an implementation in C#. Although the algorithm is simple, it offers a didactic introduction to cryptography. The detailed C# code illustrates how to apply XOR to encrypt and decrypt text.

However, it is essential to recognize the

 limitations of XOR in the context of security. XOR encryption using System;
using System.Text;

class Program
{
    static void Main()
    {
        while (true)
        {
            Console.WriteLine("1. Chiffrer un texte");
            Console.WriteLine("2. Déchiffrer un texte");
            Console.WriteLine("0. Quitter");
            Console.Write("Choisissez une option : ");

            string choice = Console.ReadLine();

            switch (choice)
            {
                case "1":
                    EncryptText();
                    break;
                case "2":
                    DecryptText();
                    break;
                case "0":
                    Environment.Exit(0);
                    break;
                default:
                    Console.WriteLine("Option non valide. Veuillez réessayer.");
                    break;
            }
        }
    }

    static void EncryptText()
    {
        Console.Clear();
        Console.Write("Entrez le texte à chiffrer : ");
        string text = Console.ReadLine();

        Console.Write("Entrez la clé : ");
        string key = Console.ReadLine();

        string encryptedBinary = EncryptToBinary(text, key);
        Console.WriteLine("Texte chiffré en binaire : " + encryptedBinary);
        Console.WriteLine("Texte chiffré : " + Decrypt(encryptedBinary, key));
    }

    static void DecryptText()
    {
        Console.Clear();
        Console.Write("Entrez le texte à déchiffrer (en binaire) : ");
        string encryptedBinary = Console.ReadLine();

        Console.Write("Entrez la clé : ");
        string key = Console.ReadLine();

        Console.WriteLine("Texte déchiffré : " + Decrypt(encryptedBinary, key));
    }

    static string StringToBinary(string text)
    {
        StringBuilder binary = new StringBuilder();
        foreach (char c in text)
        {
            binary.Append(Convert.ToString(c, 2).PadLeft(8, '0'));
        }
        return binary.ToString();
    }

    static string EncryptToBinary(string text, string key)
    {
        StringBuilder encrypted = new StringBuilder();

        for (int i = 0; i < text.Length; i++)
        {
            char xorResult = (char)(text[i] ^ key[i % key.Length]);
            encrypted.Append(Convert.ToString(xorResult, 2).PadLeft(8, '0'));
        }

        return encrypted.ToString();
    }

    static string Decrypt(string encryptedBinary, string key)
    {
        StringBuilder decryptedText = new StringBuilder();

        for (int i = 0; i < encryptedBinary.Length; i += 8)
        {
            string binaryChunk = encryptedBinary.Substring(i, 8);
            char decryptedChar = (char)Convert.ToByte(binaryChunk, 2);

            // Appliquer l'opération XOR avec la clé pour déchiffrer
            char xorResult = (char)(decryptedChar ^ key[i / 8 % key.Length]);
            decryptedText.Append(xorResult);
        }

        return decryptedText.ToString();
    }
}alone does not withstand more advanced attacks, such as key attacks, making it inappropriate for high-security requirements. This underscores the importance of considering more robust and complex algorithms when security is a priority.

## For More…

Here's a few examples of interesting situations if you want to see more:

- [Example with the Text "Erasmus Latvia"](https://www.notion.so/Example-with-the-Text-Erasmus-Latvia-529cad3007504faa993da9c8e540fc2a?pvs=21)
- [XOR Encryption with Short Text](https://www.notion.so/XOR-Encryption-with-Short-Text-e8111debe9f2494b81898b9e85c1e595?pvs=21)
- [XOR Encryption with Longer Text and Key](https://www.notion.so/XOR-Encryption-with-Longer-Text-and-Key-ee18d620a3114df4ac6638f35dd226ee?pvs=21)
- [Concrete Case: Password Encryption](https://www.notion.so/Concrete-Case-Password-Encryption-a5e7d1116a484a8e82b0e9a04f057633?pvs=21)

Ps: I am trying to improve my code so on the document it's the first version, but I will still be working on it until December 22. So here's the history of my .cs: [Main.cs](https://www.notion.so/Main-cs-7fa48c6dd6404d1cac5144148216ee2e?pvs=21)
