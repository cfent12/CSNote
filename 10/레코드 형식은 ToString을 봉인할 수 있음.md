[..](../README.md)

# 레코드 형식은 ToString을 봉인할 수 있음

C# 10에서는 레코드 형식에서 `ToString`을 재정의할 때 `sealed` 한정자를 추가할 수 있습니다. 
`ToString` 메서드를 봉인하면 컴파일러가 파생된 레코드 형식에 대해 `ToString` 메서드를 합성할 수 없습니다. 
`sealed` `ToString`은 모든 파생된 레코드 형식이 공통 기본 레코드 형식에 정의된 `ToString` 메서드를 사용하게 합니다.

이를 통해 파생 클래스에서 `ToString` 메서드를 오버라이드하지 못하도록 할 수 있습니다.

## 예제

```cs
using System;

public record Person(string FirstName, string LastName)
{
    // ToString 메서드를 sealed로 선언
    public sealed override string ToString() => $"{FirstName} {LastName}";
}

public record Employee(string FirstName, string LastName, string Position) : Person(FirstName, LastName)
{
    // ToString 메서드를 오버라이드하려고 하면 컴파일 에러 발생
    // public override string ToString() => $"{base.ToString()}, {Position}";
}

public class Program
{
    public static void Main()
    {
        var employee = new Employee("Jane", "Smith", "Manager");
        Console.WriteLine(employee); // Output: Jane Smith
    }
}
```
