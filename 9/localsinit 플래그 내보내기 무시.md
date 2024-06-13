[..](../README.md)

# localsinit 플래그 내보내기 무시

C# 9에서는 `localsinit` 플래그를 생략하여 최적화된 코드를 생성할 수 있는 기능이 추가되었습니다. 
이 플래그는 일반적으로 메서드 내의 모든 로컬 변수를 기본값으로 초기화하는 역할을 합니다. 
이를 생략하면 성능이 향상될 수 있지만, 주의해서 사용해야 합니다.

## 설명

- **기본 동작**: C# 컴파일러는 메서드의 로컬 변수를 0으로 초기화합니다. 이는 IL 코드에서 `localsinit` 플래그를 설정함으로써 이루어집니다.
- **localsinit 플래그 생략**: `localsinit` 플래그를 생략하면 로컬 변수 초기화를 생략하여 성능을 향상시킬 수 있습니다. 그러나 이는 개발자가 로컬 변수 초기화에 대해 더 많은 책임을 지게 됩니다.

## 사용법

- `SkipLocalsInit` 특성을 사용하여 `localsinit` 플래그를 생략할 수 있습니다.
- 이 특성은 클래스, 구조체, 메서드에 적용할 수 있습니다.

## 예제

1. `localsinit` 플래그 생략
    ```cs
    using System;
    using System.Runtime.CompilerServices;

    class Program
    {
        // 메서드에 SkipLocalsInit 특성 적용
        [SkipLocalsInit]
        static void WithoutLocalsInit()
        {
            int x; // 초기화되지 않은 로컬 변수
            Console.WriteLine(x); // 미정의 동작(컴파일러에 따라 다를 수 있음)
        }

        static void Main()
        {
            try
            {
                WithoutLocalsInit();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
    }
    ```

2. 실전 예제: 초기화 책임을 개발자가 지는 경우
    ```cs
    using System;
    using System.Runtime.CompilerServices;

    class Program
    {
        // 메서드에 SkipLocalsInit 특성 적용
        [SkipLocalsInit]
        static void WithoutLocalsInit()
        {
            int x = 0; // 로컬 변수 명시적 초기화
            Console.WriteLine(x); // 예상된 결과 출력
        }

        static void Main()
        {
            WithoutLocalsInit();
        }
    }
    ```

3. 클래스 또는 어셈블리 수준 적용
    - 클래스 수준 적용
        ```cs
        using System;
        using System.Runtime.CompilerServices;

        [SkipLocalsInit]
        class MyClass
        {
            static void Method1()
            {
                int x;
                unsafe
                {
                    int* px = &x;
                    Console.WriteLine(*px);
                }
            }

            static void Method2()
            {
                int y = 10;
                Console.WriteLine(y);
            }
        }
        ```

    - 어셈블리 수준 적용
        ```cs
        using System;
        using System.Runtime.CompilerServices;

        [assembly: SkipLocalsInit]

        class Program
        {
            static void Method1()
            {
                int x;
                unsafe
                {
                    int* px = &x;
                    Console.WriteLine(*px);
                }
            }

            static void Method2()
            {
                int y = 10;
                Console.WriteLine(y);
            }

            static void Main()
            {
                Method1();
                Method2();
            }
        }
        ```
