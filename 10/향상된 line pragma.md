[..](../README.md)

# 향상된 #line pragma

C# 10은 `#line` pragma에 대한 새 형식을 지원합니다. 새 형식을 직접 사용할 일은 없겠지만, 그 영향은 확인할 수 있습니다. 
이로 인해 Razor와 같은 DSL(Domain-Specific Language)에서 더욱 정교한 출력을 얻을 수 있습니다.

## 예제

```cs
using System;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Before enhanced #line pragma");

        #line 100 "EnhancedLinePragmaExample.cs"
        Console.WriteLine("This line appears to be at line 100 in EnhancedLinePragmaExample.cs");

        #line default
        Console.WriteLine("After restoring original line information");

        #line hidden
        // This code is hidden from the debugger
        Console.WriteLine("This line will not be visible in the debugger");
    }
}
```

이 예제에서 `#line` 100 "EnhancedLinePragmaExample.cs"는 다음 줄이 EnhancedLinePragmaExample.cs 파일의 100번째 줄에 있는 것처럼 보이게 합니다. `#line` default는 원래의 줄 번호 정보를 복원하고, `#line` hidden은 특정 코드를 디버거에서 숨깁니다.
