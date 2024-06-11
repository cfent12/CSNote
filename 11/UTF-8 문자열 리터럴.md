[..](../README.md)

# UTF-8 문자열 리터럴

UTF-8 문자 인코딩을 지정하려면 문자열 리터럴에 `u8` 접미사를 지정할 수 있습니다. 
애플리케이션에 HTTP 문자열 상수 또는 유사한 텍스트 프로토콜에 대해 UTF-8 문자열이 필요한 경우 이 기능을 사용하여 UTF-8 문자열 만들기를 간소화할 수 있습니다.

## 예제

1. 기본 UTF-8 문자열 리터럴
    ```cs
    using System;

    public class Program
    {
        public static void Main()
        {
            ReadOnlySpan<byte> utf8String = "Hello, World!"u8;
            Console.WriteLine($"UTF-8 String: {utf8String.ToString()}");
            // Note: ReadOnlySpan<byte> does not have a direct ToString() method that converts UTF-8 bytes back to string,
            // so the above line will just print the type name.
        }
    }
    ```

2. UTF-8 문자열 리터럴과 메모리 사용
    ```cs
    using System;
    using System.Text;

    public class Program
    {
        public static void Main()
        {
            ReadOnlySpan<byte> utf8String = "Hello, World!"u8;
            
            // Convert ReadOnlySpan<byte> to string for display purposes
            string decodedString = Encoding.UTF8.GetString(utf8String);
            Console.WriteLine($"Decoded UTF-8 String: {decodedString}"); // Output: Decoded UTF-8 String: Hello, World!
        }
    }
    ```

3. UTF-8 문자열 리터럴과 파일 I/O
    ```cs
    using System;
    using System.IO;
    using System.Text;

    public class Program
    {
        public static void Main()
        {
            ReadOnlySpan<byte> utf8String = "Hello, File!"u8;
            string filePath = "utf8_example.txt";

            // Write UTF-8 bytes to file
            File.WriteAllBytes(filePath, utf8String.ToArray());

            // Read UTF-8 bytes from file
            byte[] fileContent = File.ReadAllBytes(filePath);

            // Convert byte array back to string
            string decodedString = Encoding.UTF8.GetString(fileContent);
            Console.WriteLine($"File content: {decodedString}"); // Output: File content: Hello, File!
        }
    }
    ```
