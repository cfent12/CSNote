[..](../README.md)

# 전역 using 지시문

지시문이 컴파일의 모든 소스 파일에 적용되도록 컴파일러에 지시하려면 using 지시문에 `global` 한정자를 추가할 수 있습니다.

Global using directives를 사용하면 파일마다 반복해서 using 문을 작성할 필요 없이, 프로젝트 전역에서 사용할 수 있는 using 문을 한 곳에 모아서 선언할 수 있습니다.

## 예제

1. GlobalUsings.cs 파일 생성:
    ```cs
    // GlobalUsings.cs 파일
    global using System;
    global using System.Collections.Generic;
    ```

2. Program.cs 파일:
    ```cs
    // Program.cs 파일
    // 별도의 using 선언 없이 전역에서 사용할 수 있음
    public class Program
    {
        public static void Main()
        {
            List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
            foreach (var number in numbers)
            {
                Console.WriteLine(number);
            }
        }
    }
    ```
