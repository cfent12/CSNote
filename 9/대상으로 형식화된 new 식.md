[..](../README.md)

# 대상으로 형식화된 new 식

C# 9에서 도입된 "대상으로 형식화된 new 식(Target-typed new expressions)"은 객체를 생성할 때 사용할 타입을 명시적으로 지정하지 않아도 되는 기능입니다. 
이는 코드의 가독성과 간결성을 높이며, 특히 타입을 추론할 수 있는 경우 유용합니다.

## 설명

- **기본 개념**: 객체를 생성할 때, new 식의 대상 타입이 명확히 지정된 경우 타입명을 생략할 수 있습니다.
- **용도**: 변수 선언, 속성 초기화, 메서드 호출 등 다양한 상황에서 사용할 수 있습니다.
- **장점**: 코드의 중복을 줄이고, 읽기 쉽게 만들며, 타입 추론을 통해 코드의 명확성을 높입니다.

## 예제

1. 변수 선언에서의 사용
    - 기존 방식
        ```cs
        Person person = new Person("Alice", 30);
        ```

    - C# 9의 대상 형식화된 new 식 사용
        ```cs
        Person person = new("Alice", 30);
        ``` 

2. 속성 초기화에서의 사용
    - 기존 방식
        ```cs
        class Example
        {
            public Person PersonProperty { get; set; } = new Person("Bob", 25);
        }
        ```

    - C# 9의 대상 형식화된 new 식 사용
        ```cs
        class Example
        {
            public Person PersonProperty { get; set; } = new("Bob", 25);
        }
        ``` 

3. 메서드 호출에서의 사용
    - 기존 방식
        ```cs
        void PrintPerson(Person person)
        {
            Console.WriteLine($"{person.Name}, {person.Age}");
        }

        PrintPerson(new Person("Charlie", 40));
        ```

    - C# 9의 대상 형식화된 new 식 사용
        ```cs
        void PrintPerson(Person person)
        {
            Console.WriteLine($"{person.Name}, {person.Age}");
        }

        PrintPerson(new("Charlie", 40));
        ``` 

4. 복합 사용
    ```cs
    using System;
    using System.Collections.Generic;

    class Person
    {
        public string Name { get; }
        public int Age { get; }

        public Person(string name, int age)
        {
            Name = name;
            Age = age;
        }
    }

    class Program
    {
        static void Main()
        {
            // 변수 선언에서 사용
            Person person = new("Alice", 30);

            // 속성 초기화에서 사용
            List<Person> people = new()
            {
                new("Bob", 25),
                new("Charlie", 40)
            };

            // 메서드 호출에서 사용
            PrintPerson(new("Dave", 35));

            foreach (var p in people)
            {
                Console.WriteLine($"{p.Name}, {p.Age}");
            }
        }

        static void PrintPerson(Person person)
        {
            Console.WriteLine($"{person.Name}, {person.Age}");
        }
    }
    ```
