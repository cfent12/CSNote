[..](../README.md)

# `params` 컬렉션

`params` 수정자는 array type으로 제한되지 않습니다.</br>
이제 `System.Span<T>`, `System.ReadOnlySpan<T>` 및 `System.Collections.Generic.IEnumerable<T>`을 구현하고 `Add` 메서드가 있는 유형을 포함하여 인식된 모든 컬렉션 유형에 매개변수를 사용할 수 있습니다.

콘크리트 유형 외에도 인터페이스 `System.Collections.Generic.IEnumerable<T>`, `System.Collections.Generic.IReadOnlyCollection<T>`, `System.Collections.Generic.IReadOnlyList<T>`, `System.Collections.Generic.ICollection<T>`, `System.Collections.Generic.IList<T>`도 사용할 수 있습니다.

## 예제

1. 기본 `params` 컬렉션 사용
    ```cs
    using System;

    public class Program
    {
        // 가변 인수 목록을 받아들이는 메서드
        public static void PrintNumbers(params int[] numbers)
        {
            foreach (var number in numbers)
            {
                Console.WriteLine(number);
            }
        }

        public static void Main()
        {
            // 여러 개의 정수를 가변 인수로 전달
            PrintNumbers(1, 2, 3, 4, 5);
            
            // 배열을 가변 인수로 전달
            int[] numbersArray = { 6, 7, 8, 9, 10 };
            PrintNumbers(numbersArray);
        }
    }
    ```

2. `params` 키워드를 사용하여 컬렉션 전달
    ```cs
    using System;
    using System.Collections.Generic;

    public class Program
    {
        // 가변 인수 목록으로 리스트를 받아들이는 메서드
        public static void PrintNames(params List<string>[] namesLists)
        {
            foreach (var names in namesLists)
            {
                foreach (var name in names)
                {
                    Console.WriteLine(name);
                }
            }
        }

        public static void Main()
        {
            // 여러 개의 리스트를 가변 인수로 전달
            List<string> namesList1 = new List<string> { "Alice", "Bob" };
            List<string> namesList2 = new List<string> { "Charlie", "Dave" };
            
            PrintNames(namesList1, namesList2);
        }
    }
    ```

3. `params` 키워드를 사용하여 다양한 컬렉션 타입 전달
    ```cs
    using System;
    using System.Collections.Generic;

    public class Program
    {
        // 가변 인수 목록으로 다양한 컬렉션을 받아들이는 메서드
        public static void PrintCollections(params IEnumerable<string>[] collections)
        {
            foreach (var collection in collections)
            {
                foreach (var item in collection)
                {
                    Console.WriteLine(item);
                }
            }
        }

        public static void Main()
        {
            // 리스트와 배열을 가변 인수로 전달
            List<string> namesList = new List<string> { "Eve", "Frank" };
            string[] namesArray = { "Grace", "Heidi" };
            
            PrintCollections(namesList, namesArray);
        }
    }
    ```
