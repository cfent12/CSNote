[..](../README.md)

# GetEnumerator 루프에 대한 확장 foreach 지원

확장 메서드를 사용하여 `GetEnumerator` 루프에 대한 지원을 제공하는 기능은 C# 9.0에서 도입되었습니다. 이 기능을 통해 `foreach` 루프에서 `GetEnumerator` 메서드를 확장 메서드로 사용할 수 있습니다. 이렇게 하면, 특정 형식이 `IEnumerable` 인터페이스를 구현하지 않더라도 `foreach` 루프를 사용할 수 있게 됩니다. 

## 설명

`foreach` 루프가 foreach 패턴을 충족하는 확장 메서드 `GetEnumerator` 메서드를 인식하고, 그렇지 않으면 오류가 발생할 경우 식을 반복하도록 허용합니다. 
이렇게 하면 비동기 및 패턴 기반 분해를 포함하여 C#의 다른 기능이 구현되는 방식과 일치하도록 foreach을(를) 조정합니다.

## 장점

- 기존 코드를 수정하지 않고도 foreach 루프를 지원할 수 있습니다.
- IEnumerable 인터페이스를 구현하지 않는 사용자 정의 형식을 foreach 루프로 사용할 수 있습니다.

## 단점

- 모든 변경은 언어에 추가적인 복잡성을 더해주며, 이것은 `foreach`같은 것으로 `foreach`설계되지 않은 것들을 잠재적으로 허용할 수 있습니다, 예를 들어 `Range`와 같은 것입니다.

## 예제

```cs
public static class MyExtensions
{
    public static CustomEnumerator GetEnumerator(this MyType obj) // MyType에 대한 확장 메서드
    {
        // CustomEnumerator 객체 생성 및 반환
        return new CustomEnumerator(obj);
    }
}

public class MyType
{
    // ...
}

public struct CustomEnumerator
{
    private readonly MyType _obj;
    private int _index;

    public CustomEnumerator(MyType obj)
    {
        _obj = obj;
        _index = -1;
    }

    public bool MoveNext()
    {
        _index++;
        return _index < 10; // 예시: 10회 반복
    }

    public int Current
    {
        get { return _index; } // 예시: 현재 인덱스 반환
    }
}

public class Example
{
    public static void Main(string[] args)
    {
        MyType myObject = new MyType();
        foreach (int item in myObject) // 확장 메서드 GetEnumerator 사용
        {
            Console.WriteLine(item);
        }
    }
}
```