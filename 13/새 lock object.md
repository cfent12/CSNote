[..](../README.md)

# 새 lock object

.NET 9 런타임에는 스레드 동기화를 위한 새로운 유형인 System.Threading.Lock 유형이 포함되어 있습니다.
이 유형은 API를 통해 더 나은 스레드 동기화를 제공합니다. 
Lock.EnterScope() 메서드는 배타적 범위에 들어갑니다.
배타적 범위를 종료하는 `Dispose()` 패턴을 지원하는 `ref struct` 구조체가 return됩니다.

C# lock 문은 잠금 대상이 `Lock` object인지 인식합니다.
그렇다면 System.Threading.Monitor를 사용하는 기존 API가 아닌 업데이트된 API를 사용합니다.
컴파일러는 `Lock` object를 다른 유형으로 변환하면 `Monitor` 기반 코드가 생성됨을 인식합니다.

- C# 13에서 new 키워드를 사용하여 lock 구문에 인라인으로 객체를 생성할 수 있지만, 각 스레드가 서로 다른 객체를 잠그게 되므로 이 방법은 올바르지 않습니다.
- 동기화를 위해서는 lock 구문에서 동일한 잠금 객체를 사용해야 합니다.
- 예제를 통해 올바른 사용 방법을 이해하고, 잠금 객체를 명시적으로 정의하여 사용하는 것이 중요합니다.

## 예제

1. 올바르지 않은 사용 예제
    ```cs
    using System;
    using System.Threading;
    using System.Threading.Tasks;

    public class Program
    {
        public static void Main()
        {
            int counter = 0;

            // 여러 작업을 병렬로 실행하여 counter 값을 증가시킴
            Parallel.For(0, 1000, i =>
            {
                // lock 구문에서 new 키워드를 사용하여 인라인으로 잠금 객체를 생성함
                lock (new object())
                {
                    counter++;
                }
            });

            // 잠금이 제대로 되지 않아 예상하지 않은 결과가 나옴
            Console.WriteLine($"Counter: {counter}");
        }
    }
    ```

    이 예제에서 `lock (new object())`는 각 반복에서 새로운 객체를 생성하고 잠금을 수행합니다. 하지만 이 방법은 각 잠금이 서로 다른 객체를 잠그기 때문에 실제로는 효과적인 잠금이 이루어지지 않습니다. 이 예제는 올바르지 않은 사용 방법을 보여줍니다.

2. 올바른 사용 예제
    ```cs
    using System;
    using System.Threading;
    using System.Threading.Tasks;

    public class Program
    {
        private static readonly object lockObj = new();

        public static void Main()
        {
            int counter = 0;

            // 여러 작업을 병렬로 실행하여 counter 값을 증가시킴
            Parallel.For(0, 1000, i =>
            {
                // lock 구문에서 미리 정의된 lockObj 객체를 사용하여 잠금 수행
                lock (lockObj)
                {
                    counter++;
                }
            });

            // 모든 작업이 완료될 때까지 대기
            Thread.Sleep(1000);

            // 잠금이 제대로 되어서 예상된 결과가 나옴
            Console.WriteLine($"Counter: {counter}");
        }
    }
    ```

    이 예제에서는 `lock (new object())` 대신 `lock (lockObj)`를 사용하여 모든 스레드가 동일한 객체에 대해 잠금을 수행하도록 합니다. 이를 통해 올바르게 동기화된 결과를 얻을 수 있습니다.
