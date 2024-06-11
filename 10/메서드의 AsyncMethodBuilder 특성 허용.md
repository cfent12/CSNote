[..](../README.md)

# 메서드의 AsyncMethodBuilder 특성 허용

C# 10 이상에서는 지정된 작업과 유사한 형식을 반환하는 모든 메서드에 대해 메서드 작성기 형식을 지정하는 것에 더해, 단일 메서드에 대해 여러 비동기 메서드 작성기를 지정할 수 있습니다. 
사용자 지정 비동기 메서드 작성기를 이용하면, 지정된 메서드가 사용자 지정 작성기를 활용할 수 있는 고급 성능 조정 시나리오를 사용할 수 있습니다.

C# 10에서는 AsyncMethodBuilder 특성을 메서드에 적용할 수 있습니다. 
이를 통해 특정 메서드에 대해 사용자 정의 AsyncMethodBuilder를 사용할 수 있습니다. 
이 특성은 비동기 메서드의 성능을 미세 조정할 때 유용합니다.

## 예제

1. 먼저 사용자 정의 AsyncMethodBuilder를 정의합니다.
    ```cs
    using System.Runtime.CompilerServices;
    using System.Threading.Tasks;

    public struct CustomAsyncMethodBuilder
    {
        private AsyncTaskMethodBuilder _builder;

        public static CustomAsyncMethodBuilder Create() => new CustomAsyncMethodBuilder { _builder = AsyncTaskMethodBuilder.Create() };

        public void Start<TStateMachine>(ref TStateMachine stateMachine) where TStateMachine : IAsyncStateMachine
        {
            _builder.Start(ref stateMachine);
        }

        public void SetStateMachine(IAsyncStateMachine stateMachine)
        {
            _builder.SetStateMachine(stateMachine);
        }

        public void SetResult()
        {
            _builder.SetResult();
        }

        public void SetException(Exception exception)
        {
            _builder.SetException(exception);
        }

        public Task Task => _builder.Task;

        public void AwaitOnCompleted<TAwaiter, TStateMachine>(ref TAwaiter awaiter, ref TStateMachine stateMachine)
            where TAwaiter : INotifyCompletion
            where TStateMachine : IAsyncStateMachine
        {
            _builder.AwaitOnCompleted(ref awaiter, ref stateMachine);
        }

        public void AwaitUnsafeOnCompleted<TAwaiter, TStateMachine>(ref TAwaiter awaiter, ref TStateMachine stateMachine)
            where TAwaiter : ICriticalNotifyCompletion
            where TStateMachine : IAsyncStateMachine
        {
            _builder.AwaitUnsafeOnCompleted(ref awaiter, ref stateMachine);
        }
    }
    ```

2. 이제 메서드에 AsyncMethodBuilder 특성을 적용하여 사용자 정의 AsyncMethodBuilder를 사용합니다.
    ```cs
    using System;
    using System.Runtime.CompilerServices;
    using System.Threading.Tasks;

    public class Program
    {
        [AsyncMethodBuilder(typeof(CustomAsyncMethodBuilder))]
        public static async Task CustomAsyncMethod()
        {
            await Task.Delay(1000);
            Console.WriteLine("Task completed with custom async method builder.");
        }

        public static async Task Main(string[] args)
        {
            await CustomAsyncMethod();
        }
    }
    ```
