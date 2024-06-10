[..](../README.md)

# 기본 람다 parameter

이제 람다 식의 parameter에 대한 기본값을 정의할 수 있습니다. 
구문 및 규칙은 모든 메서드 또는 로컬 함수에 인수에 대한 기본값을 추가하는 것과 같습니다.

## 예제

```cs
public class Program
{
    public static void Main()
    {
        // 기본 람다 매개 변수 설정
        Func<int, int, int> add = (x = 1, y = 2) => x + y;

        Console.WriteLine(add());       // Output: 3 (x=1, y=2)
        Console.WriteLine(add(5));      // Output: 7 (x=5, y=2)
        Console.WriteLine(add(5, 10));  // Output: 15 (x=5, y=10)
    }
}
```
