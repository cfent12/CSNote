[..](../README.md)

# `ref` 필드 및 `ref scoped` 변수

ref struct 내에 `ref` 필드를 선언할 수 있습니다. 이는 특별한 특성이나 숨겨진 내부 형식이 없는 `System.Span<T>`와 같은 형식을 지원합니다.

`ref` 선언에 scoped 한정자를 추가할 수 있습니다. 이는 참조가 이스케이프될 수 있는 범위를 제한합니다.

- `ref` 필드를 통해 구조체 내에서 참조를 저장하고 관리할 수 있습니다.
- `ref scoped` 변수를 통해 참조의 수명을 제어할 수 있습니다.

## 예제

1. `ref` 필드
    ```cs
    using System;

    public struct MyStruct
    {
        private ref int value;
        public MyStruct(ref int value)
        {
            this.value = ref value;
        }

        public void Increment()
        {
            value++;
        }
    }

    public class Program
    {
        public static void Main()
        {
            int number = 5;
            MyStruct myStruct = new MyStruct(ref number);
            myStruct.Increment();
            Console.WriteLine(number); // Output: 6
        }
    }
    ```

2. `ref scoped` 변수
    ```cs
    using System;

    public class Program
    {
        public static void Main()
        {
            int value = 10;
            ref int refValue = ref GetRefScoped(ref value);
            Console.WriteLine(refValue); // Output: 10
            refValue = 20;
            Console.WriteLine(value); // Output: 20
        }

        public static ref int GetRefScoped(ref int input)
        {
            ref scoped int result = ref input;
            return ref result;
        }
    }
    ```
