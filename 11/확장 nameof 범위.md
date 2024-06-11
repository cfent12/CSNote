[..](../README.md)

# 확장 `nameof` 범위

C# 11에서는 `nameof` 연산자의 확장된 사용 범위가 추가되어, 매개변수 이름뿐만 아니라 메서드 이름, 속성 이름, 그리고 로컬 함수 이름 등 다양한 범위에서 `nameof` 연산자를 사용할 수 있게 되었습니다. 이는 코드의 가독성을 높이고, 리팩토링 시 오류를 줄일 수 있습니다.

이 기능은 null 허용 분석을 위한 특성을 추가하는 데 가장 유용합니다.

## 예제

1. 메서드 이름에 `nameof` 사용
    ```cs
    using System;

    public class Program
    {
        public static void Main()
        {
            Console.WriteLine(nameof(Main)); // Output: Main
            Console.WriteLine(nameof(HelperMethod)); // Output: HelperMethod
            HelperMethod();
        }

        public static void HelperMethod()
        {
            Console.WriteLine(nameof(HelperMethod)); // Output: HelperMethod
        }
    }
    ```

2. 속성 이름에 `nameof` 사용
    ```cs
    using System;

    public class Person
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
    }

    public class Program
    {
        public static void Main()
        {
            Console.WriteLine(nameof(Person.FirstName)); // Output: FirstName
            Console.WriteLine(nameof(Person.LastName)); // Output: LastName
        }
    }
    ```

3. 로컬 함수 이름에 `nameof` 사용
    ```cs
    using System;

    public class Program
    {
        public static void Main()
        {
            Console.WriteLine(nameof(Main)); // Output: Main
            LocalFunction();

            void LocalFunction()
            {
                Console.WriteLine(nameof(LocalFunction)); // Output: LocalFunction
            }
        }
    }
    ```

4. 매개변수 이름에 `nameof` 사용
    ```cs
    using System;

    public class Program
    {
        public static void PrintParameterName(string parameter)
        {
            Console.WriteLine(nameof(parameter)); // Output: parameter
        }

        public static void Main()
        {
            PrintParameterName("Hello, world!");
        }
    }
    ```
