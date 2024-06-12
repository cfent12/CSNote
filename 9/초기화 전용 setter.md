[..](../README.md)

# 초기화 전용 setter

초기화 전용 setter는 `set` 키워드 대신 `init` 키워드를 사용하여 정의됩니다. 
`init` 키워드를 사용하면 객체 생성 시에만 속성 값을 설정할 수 있고, 객체가 생성된 후에는 속성 값을 변경할 수 없습니다. 
이는 객체의 불변성을 유지하는 데 매우 유용합니다.

초기화 전용 setter는 다음과 같은 상황에서 유용합니다:
- **불변 객체(Immutable Object)**: 객체의 상태를 변경할 수 없게 하여, 객체가 생성된 후에는 그 상태가 유지되도록 합니다.
- **레코드 타입**: C# 9에서 도입된 레코드 타입과 잘 어울리며, 레코드의 불변성을 유지하는 데 사용됩니다.
- **데이터 전송 객체(Data Transfer Object, DTO)**: DTO의 속성을 초기화 시에만 설정하고 이후에는 변경할 수 없도록 하여 데이터 무결성을 유지합니다.

## 예제

```cs
public class Person
{
    public string FirstName { get; init; }
    public string LastName { get; init; }

    public override string ToString() => $"{FirstName} {LastName}";
}

public class Program
{
    public static void Main()
    {
        var person = new Person
        {
            FirstName = "John",
            LastName = "Doe"
        };

        // person.FirstName = "Jane"; // 컴파일 오류: 'FirstName' 속성은 'init' 전용입니다.

        Console.WriteLine(person); // Output: John Doe
    }
}
```
