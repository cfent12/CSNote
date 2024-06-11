[..](../README.md)

# CallerArgumentExpression 특성 진단

System.Runtime.CompilerServices.CallerArgumentExpressionAttribute를 사용하여, 컴파일러가 다른 인수의 텍스트 표현으로 바꿀 매개 변수를 지정할 수 있습니다. 
이 기능은 라이브러리가 보다 구체적인 진단을 만들 수 있도록 지원합니다. 

`CallerArgumentExpression` 특성은 메서드 호출에서 특정 인수의 표현식을 가져올 수 있게 해줍니다. 
이 특성은 주로 디버깅과 로깅 시 유용합니다.

## 예제

```cs
using System;
using System.Runtime.CompilerServices;

public static class Validator
{
    public static void ValidateNotNull(object arg, [CallerArgumentExpression("arg")] string? paramName = null)
    {
        if (arg == null)
        {
            throw new ArgumentNullException(paramName);
        }
    }
}

public class Program
{
    public static void Main()
    {
        string? testString = null;

        try
        {
            Validator.ValidateNotNull(testString);
        }
        catch (ArgumentNullException ex)
        {
            Console.WriteLine($"Argument null: {ex.ParamName}");
        }
    }
}
```

`System.Runtime.CompilerServices` 네임스페이스를 사용하여 `CallerArgumentExpression` 특성을 활용하는 예제입니다.

이 예제에서 `ValidateNotNull` 메서드는 `CallerArgumentExpression` 특성을 사용하여 호출된 인수의 표현식을 가져옵니다. `testString`이 `null`일 때 `ArgumentNullException`이 발생하고, 인수 이름 (`testString`)이 출력됩니다.
