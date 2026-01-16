using System;
using System.Text;

class CaesarCipher
{
    static string Transform(string text, int shift)
    {
        StringBuilder result = new StringBuilder();

        foreach (char c in text)
        {
            if (char.IsLetter(c))
            {
                char offset = char.IsUpper(c) ? 'A' : 'a';
                int position = (((c - offset) + shift) % 26 + 26) % 26;
                result.Append((char)(position + offset));
            }
            else
            {
                result.Append(c);
            }
        }
        return result.ToString();
    }

    static string Encrypt(string text)
    {
        return Transform(text, 3);
    }

    static string Decrypt(string text)
    {
        return Transform(text, -3);
    }

    static void Cryptanalysis(string text)
    {
        Console.WriteLine("\n--- Criptanaliza (Brute Force) ---");
        for (int i = 0; i < 26; i++)
        {
            string attempt = Transform(text, -i);
            Console.WriteLine($"Shift -{i}: {attempt}");
        }
    }

    static void Main()
    {
        Console.Write("Introduceti textul clar: ");
        string input = Console.ReadLine();

        string encrypted = Encrypt(input);
        Console.WriteLine($"\nText Criptat: {encrypted}");

        string decrypted = Decrypt(encrypted);
        Console.WriteLine($"Text Decriptat: {decrypted}");

        Cryptanalysis(encrypted);

        Console.ReadKey();
    }
}
