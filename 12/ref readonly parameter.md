[..](../README.md)

# `ref readonly` parameters

C#은 읽기 전용 참조를 전달하는 방법으로 `in` parameter를 추가했습니다. `in` parameter는 변수와 값을 모두 허용하며 인수에 대한 주석 없이 사용할 수 있습니다.

`ref readonly` parameter를 추가하면 `ref` parameter 또는 `in` parameter를 사용할 수 있는 API의 명확성을 높일 수 있습니다.:

- `in`이 도입되기 전에 만든 API는 인수가 수정되지 않은 경우에도 `ref`를 사용할 수 있습니다. 이러한 API는 `ref readonly`로 업데이트할 수 있습니다. 
`ref` parameter가 `in`으로 변경된 경우와 마찬가지로 호출자에 대한 호환성이 손상되는 변경은 아닙니다.
예제는 System.Runtime.InteropServices.Marshal.QueryInterface입니다.
- `in` parameter를 사용하지만 논리적으로 변수가 필요한 API입니다. 
값 표현식이 작동하지 않습니다. 
예제는 System.ReadOnlySpan<T>.ReadOnlySpan<T>(T)입니다.
- 변수가 필요하지만 해당 변수를 변경하지 않기 때문에 `ref`를 사용하는 API입니다. 
예제는 System.Runtime.CompilerServices.Unsafe.IsNullRef입니다.

이는 값 타입의 큰 구조체를 전달할 때 복사 비용을 줄이는 데 유용합니다.

## 예제

```cs
public struct LargeStruct
{
    public int Value1;
    public int Value2;
    public int Value3;
}

public class Program
{
    // ref readonly 매개 변수를 사용하여 읽기 전용 참조로 전달
    public static int Sum(ref readonly LargeStruct largeStruct)
    {
        return largeStruct.Value1 + largeStruct.Value2 + largeStruct.Value3;
    }

    public static void Main()
    {
        LargeStruct myStruct = new LargeStruct { Value1 = 1, Value2 = 2, Value3 = 3 };
        int result = Sum(ref myStruct);
        Console.WriteLine(result); // Output: 6
    }
}
```
