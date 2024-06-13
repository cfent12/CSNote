[..](../README.md)

# static 익명 함수

C# 9에서 도입된 `static` 익명 함수는 람다 표현식이나 익명 메서드에서 `static` 한정자를 사용할 수 있게 한 기능입니다. 
이를 통해 익명 함수가 캡처할 수 없는 외부 변수를 명확히 하여 성능을 최적화하고, 예상치 못한 캡처를 방지할 수 있습니다.

## 설명
- **기본 개념**: static 키워드를 사용하여 람다 표현식이나 익명 메서드를 선언하면 해당 익명 함수는 주변 스코프의 변수를 캡처할 수 없습니다.
- **장점**:
    - **성능 향상**: 캡처된 변수가 없으므로, 불필요한 클로저 객체를 생성하지 않아도 됩니다.
    - **명확성**: 어떤 변수가 캡처되지 않을 것임을 코드에서 명확히 알 수 있습니다.
    - **컴파일러 오류**: 캡처할 수 없는 변수를 참조하려고 하면 컴파일러가 오류를 발생시켜 문제를 조기에 발견할 수 있습니다.

## 예제

1. static 람다 표현식 사용
    ```cs
    using System;

    class Program
    {
        static void Main()
        {
            int x = 10;

            // 일반 람다 표현식 (x를 캡처할 수 있음)
            Func<int, int> regularLambda = n => n + x;

            // static 람다 표현식 (x를 캡처할 수 없음)
            Func<int, int> staticLambda = static n => n + 5;

            Console.WriteLine(regularLambda(5)); // Output: 15
            Console.WriteLine(staticLambda(5));  // Output: 10
        }
    }
    ```

1. static 익명 메서드 사용
    ```cs
    using System;

    class Program
    {
        delegate int MyDelegate(int n);

        static void Main()
        {
            int y = 20;

            // 일반 익명 메서드 (y를 캡처할 수 있음)
            MyDelegate regularDelegate = delegate (int n) { return n + y; };

            // static 익명 메서드 (y를 캡처할 수 없음)
            MyDelegate staticDelegate = static delegate (int n) { return n + 10; };

            Console.WriteLine(regularDelegate(5)); // Output: 25
            Console.WriteLine(staticDelegate(5));  // Output: 15
        }
    }
    ```
