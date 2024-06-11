[..](../README.md)

# 상수 `string`에 대한 패턴 일치 `Span<char>` 또는 `ReadOnlySpan<char>`

C# 11에서는 상수 문자열에 대한 패턴 일치를 `Span<char>` 및 `ReadOnlySpan<char>`와 함께 사용할 수 있습니다.
`Span<char>` 및 `ReadOnlySpan<char>`를 사용하는 패턴 일치 기능이 개선되어, 상수 string에 대해 보다 효율적인 패턴 일치를 지원합니다. 
이는 성능과 메모리 효율성을 향상시키며, 특히 문자열 처리가 많은 코드에서 유용합니다.

## 예제

1. `ReadOnlySpan<char>`를 사용한 패턴 일치
```cs
using System;

public class Program
{
    public static string MatchPattern(ReadOnlySpan<char> input)
    {
        return input switch
        {
            "Hello" => "Greeting detected",
            "World" => "World detected",
            "CSharp" => "Programming language detected",
            _ => "Unknown pattern"
        };
    }

    public static void Main()
    {
        ReadOnlySpan<char> span1 = "Hello".AsSpan();
        ReadOnlySpan<char> span2 = "World".AsSpan();
        ReadOnlySpan<char> span3 = "CSharp".AsSpan();
        ReadOnlySpan<char> span4 = "Unknown".AsSpan();

        Console.WriteLine(MatchPattern(span1)); // Output: Greeting detected
        Console.WriteLine(MatchPattern(span2)); // Output: World detected
        Console.WriteLine(MatchPattern(span3)); // Output: Programming language detected
        Console.WriteLine(MatchPattern(span4)); // Output: Unknown pattern
    }
}
```

2. `Span<char>`를 사용한 패턴 일치
```cs
using System;

public class Program
{
    public static string MatchPattern(Span<char> input)
    {
        return input switch
        {
            "Hello" => "Greeting detected",
            "World" => "World detected",
            "CSharp" => "Programming language detected",
            _ => "Unknown pattern"
        };
    }

    public static void Main()
    {
        Span<char> span1 = "Hello".ToCharArray();
        Span<char> span2 = "World".ToCharArray();
        Span<char> span3 = "CSharp".ToCharArray();
        Span<char> span4 = "Unknown".ToCharArray();

        Console.WriteLine(MatchPattern(span1)); // Output: Greeting detected
        Console.WriteLine(MatchPattern(span2)); // Output: World detected
        Console.WriteLine(MatchPattern(span3)); // Output: Programming language detected
        Console.WriteLine(MatchPattern(span4)); // Output: Unknown pattern
    }
}
```
