[..](../README.md)

# 숫자 `IntPtr` 및 `UIntPtr`

이제 `nint` 및 `nuint` 형식은 각각 System.IntPtr 및 System.UIntPtr의 별칭을 지정합니다.

이는 포인터 타입을 더 유연하게 사용할 수 있게 해주며, 특히 낮은 수준의 메모리 조작이나 상호 운용 시 유용합니다.

## 예제

1. `IntPtr` 연산 예제
    ```cs
    using System;

    public class Program
    {
        public static void Main()
        {
            // IntPtr 생성
            IntPtr ptr1 = new IntPtr(10);
            IntPtr ptr2 = new IntPtr(20);

            // 덧셈
            IntPtr sum = ptr1 + ptr2;
            Console.WriteLine($"Sum: {sum}"); // Output: Sum: 30

            // 뺄셈
            IntPtr difference = ptr2 - ptr1;
            Console.WriteLine($"Difference: {difference}"); // Output: Difference: 10

            // 곱셈 (곱셈은 지원하지 않음)
            // IntPtr product = ptr1 * ptr2;

            // 나눗셈 (나눗셈은 지원하지 않음)
            // IntPtr quotient = ptr2 / ptr1;

            // 증가 및 감소
            ptr1++;
            Console.WriteLine($"Incremented ptr1: {ptr1}"); // Output: Incremented ptr1: 11

            ptr2--;
            Console.WriteLine($"Decremented ptr2: {ptr2}"); // Output: Decremented ptr2: 19
        }
    }
    ```

2. `UIntPtr` 연산 예제
    ```cs
    using System;

    public class Program
    {
        public static void Main()
        {
            // UIntPtr 생성
            UIntPtr ptr1 = new UIntPtr(10);
            UIntPtr ptr2 = new UIntPtr(20);

            // 덧셈
            UIntPtr sum = ptr1 + ptr2;
            Console.WriteLine($"Sum: {sum}"); // Output: Sum: 30

            // 뺄셈
            UIntPtr difference = ptr2 - ptr1;
            Console.WriteLine($"Difference: {difference}"); // Output: Difference: 10

            // 곱셈 (곱셈은 지원하지 않음)
            // UIntPtr product = ptr1 * ptr2;

            // 나눗셈 (나눗셈은 지원하지 않음)
            // UIntPtr quotient = ptr2 / ptr1;

            // 증가 및 감소
            ptr1++;
            Console.WriteLine($"Incremented ptr1: {ptr1}"); // Output: Incremented ptr1: 11

            ptr2--;
            Console.WriteLine($"Decremented ptr2: {ptr2}"); // Output: Decremented ptr2: 19
        }
    }
    ```
