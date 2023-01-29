# Dart

---

# 온라인에서 구동 가능

- [https://dartpad.dev/](https://dartpad.dev/)

---

# Dart의 indent에 관하여

- Dart의 indent(tab)은 2칸
- 2칸인 이유는 다음과 같다
    1. C++, Java, JavaScript 등에 대한 Google의 스타일 가이드에서 2칸을 추천한다.
    2. 중첩된 코드에서 가독성이 높다.
        
        ```dart
        if (someVeryLongCondition +
            thatWrapsToTheNextLine) 
        {
          theBody();
        }
        ```
        

---

# Hello World

```dart
void main() 
{
  print("hello world");
}
```

- Dart는 main 함수에서 시작(없으면 오류)
- 세미콜론 필요

---

# Variables

- 지역변수: `var name = "kevin";`
- 전역변수, class나 property 내의 변수: `자료형 name = value;` 예) `String name = "kevin";`
- 선언하며 값이 할당된 변수에 다른 자료형을 넣으려 하면 오류 발생
    
    ```dart
    var name = "kevin"; // String
    name = 1; // Error
    ```
    

## Dynamic Type

- 선언할 때 값을 할당하지 않거나 `dynamic` 키워드를 사용하여 선언
- 모든 자료형을 할당 가능, 후에 변경도 가능
- if문을 통해 자료형 체크하면 옵션 auto complete 기능 제공
- 정말 필요할 때만 사용
    
    ```dart
    var name; // dynamic
    dynamic name; // dynamic
    
    name = "kevin";
    name = 1;
    name = true;
    
    if(name is String)
    {
    	name.// option auto complete 기능 사용 가능(vs code 기준)
    }
    ```
    

## Nullable Variables

- 모든 변수는 기본적으로 `null`이 될 수 없는 non-nullable
- 자료형 뒤에 `?`를 붙여주면 nullable 형 선언 가능
- 변수명 뒤에 `?`를 붙인 다음 속성 요청 가능
    - `null`이라면 `null` 반환
    - `null`이 아니라면 속성 반환
    
    ```dart
    String name = "kevin";
    name = null; // Error
    
    String? name = "kevin";
    name = null;
    
    // null인지 검사할 때는 다음과 같은 방법 사용
    // isEmpty() 함수는 문자열의 길이가 0인지 아닌지 판단
    if (name != null)
    {
    	name.isEmpty;
    }
    name?.isEmpty; // name == null 이므로 null 반환
    ```
    

## Final Variables

- 선언할 때 한번 값을 할당하면 바꿀 수 없는 변수
- 타 언어의 `const`와 같음
    
    ```dart
    final name = "kevin";
    final String name = "kevin";
    ```
    

## Late Variables

- 초기 데이터 없이 먼저 변수를 생성할 때 사용
- 값이 할당되기 전에 호출 시 오류 발생
- API에서 값을 받을 때 응용 가능
    
    ```dart
    late final name;
    print(name); // Error
    // API
    name = value;
    ```
    

## Constant Variables

- 컴파일 단계에서 값을 알고 있는 변수를 선언 때 사용
    
    ```dart
    const token = "1234567";
    const data = fetchApi(); // Error
    ```
    

---

# Data Types

- 거의 모든 데이터 타입들이 객체(class)
- String, bool, int, double, num(int, double의 부모 클L래스)

## List

```dart
var numbers = [1, 2, 3, 4, 5];
List<int> numbers = [1, 2, 3, 4, 5];
```

- vscode나 dartpad에서 맨 끝을 쉼표로 마무리하면 자동 줄바꿈을 해준다.
    
    ```dart
    var numbers = [
    	1,
    	2,
    	3,
    	4,
    	5,
    ];
    ```
    

## Collection If

- list를 선언할 때 if문을 넣어 선택적으로 요소를 넣거나 뺄 수 있다.
    
    ```dart
    var giveFive = true;
    var numbers = [
    	1,
    	2,
    	3,
    	4,
    	if(giveFive) 5,
    ];
    ```
    

## String Interpolation

- 문자열 중간에 변수를 넣으려면 `$변수명` or `${변수명}`
    
    ```dart
    var name = "kevin";
    var age = 10;
    var words = "name is $name and age is ${age + 2}."
    ```
    

## Collection For

- list를 선언할 때 for문을 넣어 한번에 많은 요소를 추가할 수 있다.
    
    ```dart
    var ab = ['a', 'b'];
    var cdeab = [
    	'c',
    	'd',
    	'e',
    	for (var word in ab) word,
    ];
    ```
    

## Map

- key와 value가 서로 대응하는 자료구조
- 다른 언어의 dict와 비슷
- `Map<자료형, 자료형>` 형태
- key나 value에 여러가지 자료형이 올 경우 object형으로 설정됨
    
    ```dart
    var data = {
    	'a': 1,
    	'b': 2,
    	...
    };
    ```
    
- 실제로 사용하는 경우는 별로 없지만 `Map<List<int>, int>` 형태로도 사용 가능

## Set

- 집합
- 원소 중복 x
    
    ```dart
    var numbers = {1, 2, 3, 4, 5};
    Set<int> numbers = {1, 2, 3, 4, 5};
    ```
    

---

# Functions

```dart
자료형 함수이름(매개변수)
{
	...
}

// 한줄 선언
자료형 함수이름(매개변수) => 반환값;
```

## Named Parameter

```dart
// 1
void func(String name, int age)
{
	...
}

// 2
void func({String name = 'default', int age = 99})
{
	...
}

// 3
void func({required String name, required int age})
{
	...
}
```

- 1: Positional Parameter로 매개 변수들의 순서를 기억해야 함
- 매개 변수들의 순서를 기억하는 대신 `func(name: 'kevin', age: 10);`와 같이 전달
- 2: 실수로 매개 변수의 값을 설정하지 않는 상황 때문에 기본값 설정 필수
    - dict처럼 매개 변수 전체를 중괄호(`{}`)로 감싸면 됨
- 3: 기본값을 설정하기 싫다면 `required` 키워드를 사용
    - 매개 변수의 값을 설정하지 않는다면 오류를 발생시켜 프로그래머에게 알려줌

## Optional Positional Parameter

- Positional Parameter에서 매개 변수의 기본값을 정하고 싶을 때 사용
- 매개 변수 주변을 대괄호(`[]`)로 감싸면 됨
- null-safty를 위해 자료형 뒤에 물음표(`?`)를 붙임
- 물음표 붙이고 값 미설정 시 null이 됨
    
    ```dart
    void func(String name, [int? age, String? country = 'Korea'])
    {
    	...
    }
    ```
    

## QQ Operator

- `value1 ?? value2`: `value1` 을 반환하는데, 만약 `null`이라면 `value2`를 반환
- nullable 변수와 같이 사용 가능
    
    ```dart
    void func(String? name) => name?.toUpperCase() ?? "none";
    ```
    
- `num ??= 1;`: `num`이 `null`이라면 `1`을 대입

## Typedef

- 자료형에 원하는 이름을 만들 때 사용
- `typedef 이름 = 자료형;`과 같이 작성
    
    ```dart
    typedef info = Map<String, String>;
    ```
    

---

# Classes

- `class 이름 {}`와 같이 선언
- 클래스 내부에 변수(property)나 함수를 선언 가능
- `var 변수명 = 클래스명;`으로 사용 가능
- 외부에서 클래스 내의 변수 호출: `이름.변수명`
- 클래스 내에서 변수 호출할 때는 변수명만 적으면 된다.
    - `this.변수명`도 가능하지만 변수명만 적는 것을 추천
    
    ```dart
    class Info
    {
    	String name = "kevin";
    	int age = 10;
    
    	void say()
    	{
    		print("name: $name, age: $age");
    	}
    }
    
    void main()
    {
    	var info = Info(); // new 키워드 사용 안해도 됨
    	info.age = 20;
    	info.say();
    }
    ```
    

## Constructor

- 클래스를 초기화할 때 property에 값을 할당할 수 있게 해주는 기능
- 클래스 내부에 클래스와 이름이 같은 method를 통해 할당 가능
    
    ```dart
    // 1
    class Info
    {
    	late final String name;
    	late final int age;
    
    	Info(String name, int age)
    	{
    		this.name = name;
    		this.age = age;
    	}
    }
    
    // 2
    class Info
    {
    	final String name;
    	final int age;
    
    	Info(this.name, this.age);
    }
    
    void main()
    {
    	var info = Info("kevin", 10);
    	...
    }
    ```
    
- 1: 클래스 내 method에서 값을 할당하기 때문에 property를 선언할 때 `late`키워드를 써야함
- 2: 클래스 초기화와 동시에 때문에 property를 선언할 때 `late`키워드 필요 X

## Named Constructor Parameter

- 함수의 경우와 비슷하게 클래스 초기화 시 property를 순서 상관 없이 설정 가능
- `required` 키워드 필요 or 기본값 설정 가능
    
    ```dart
    class Info
    {
    	String name;
    	int age;
    
    	Info({required this.name, required this.age});
    }
    
    void main()
    {
    	var info = Info(name: "kevin", age: 10);
    	...
    }
    ```
    

## Named Constructor

- 클래스 개체를 생성하는 생성자를 여러개 만들 때 사용
- `클래스명.생성자명()`으로 사용 가능
- 콜론(`:`)으로 property 설정 가능
    
    ```dart
    class Info 
    {
      String name;
      int age;
      String team;
    
      Info.createRedPlayer({required String name, required int age})
          : this.name = name,
            this.age = age,
            this.team = "red";
    
      Info.createBluePlayer(String name, int age)
          : this.name = name,
            this.age = age,
            this.team = "blue";
      
      Info.createYellowPlayer({required this.name, required this.age})
          : this.team = "yellow";
    }
    
    void main() 
    {
      var player1 = Info.createRedPlayer(name: "kevin", age: 10);
      var player2 = Info.createBluePlayer("james", 20);
      var player3 = Info.createBluePlayer("alex", 30);
    }
    ```
    
- 아래와 같이 응용 가능
    
    ```dart
    class Info 
    {
      String name;
      int age;
      String team;
    
      Info.fromJson(Map<String, dynamic> json)
          : name = json['name'],
            age = json['age'],
            team = json['team'];
      
      void say()
      {
        print("name: $name, age: $age, team: $team");
      }
    }
    
    void main() 
    {
      var apiData = [
        {
          "name": "kevin",
          "age": 10,
          "team": "red",
        },
        {
          "name": "james",
          "age": 20,
          "team": "blue",
        },
        {
          "name": "alex",
          "age": 30,
          "team": "yellow",
        },
      ];
      
      apiData.forEach((playerData) {
        var player = Info.fromJson(playerData);
        player.say();
      });
    }
    ```
    

## Cascade Notation

- 클래스 개체의 property를 편하게 수정할 수 있도록 해주는 기능
- 클래스 객체 뒤에 `..`을 이용해 값을 설정
    
    ```dart
    class Info
    {
    	String name;
    	int age;
    
    	Info({required this.name, required this.age});
      
      void say()
      {
        print("name: $name, age: $age");
      }
    }
    
    void main()
    {
    	var info = Info(name: "kevin", age: 10)
        ..name = "james"
        ..age = 20
        ..say();
    	var a = info
    		..name = "james"
        ..age = 20
        ..say();
    }
    ```
    

## Enum

- 값을 잘못 입력해 실수하는 것을 방지하기 위해 사용
    - 예: `blue`를 `bule`로 잘못 입력
- `enum 이름 { 값 }`
    
    ```dart
    enum Team {red, blue}
    
    class Info
    {
    	String name;
    	int age;
      Team team;
    
    	Info({required this.name, required this.age, required this.team});
    }
    
    void main()
    {
    	var info = Info(name: "kevin", age: 10, team: Team.red);
    }
    ```
    

## Abstract Class

- 추상화 클래스는 다른 클래스들이 가져야 하는 method를 모아놓은 청사진
- `abstract class 추상화클래스명`
- 하위 클래스에서는 `class 클래스명 extends 추상화클래스명`
    
    ```dart
    abstract class Human
    {
      void walk();
    }
    
    class Player extends Human
    {
      void walk()
      {
        ...
      }
    }
    
    class Enemy extends Human
    {
      void walk()
      {
        ...
      }
    }
    ```
    

## Inheritance

- 중복되는 property를 하나의 클래스에 선언한 다음 상속 받아 사용
- 하위 클래스에서는 `class 클래스명 extends 상위클래스명`
- 상위 클래스의 property를 설정할 때는 `super` 키워드를 이용
- 상위 클래스의 함수를 상속받을 때는 하위 클래스의 같은 이름을 가진 함수 위에 `@override`를 적고 `super` 키워드 사용
    
    ```dart
    class Human 
    {
      String name;
    
      Human({required this.name});
    
      void say() 
    	{
        print("name: $name");
      }
    }
    
    enum Team { red, blue }
    
    class Player extends Human 
    {
      Team team;
    
      Player({required this.team, required String name}) : super(name: name);
    	// Player({required this.team, required super.name});
    
    	// 함수 이름 다르면 Error
      @override
      void say() 
    	{
        super.say();
        print("team: $team");
      }
    }
    
    void main() 
    {
      var player = Player(team: Team.red, name: "kevin");
      player.say();
    }
    ```
    

## Mixin

- 생성자가 없는 클래스
- `with` 키워드를 사용해 mixin 클래스의 property 사용 가능
    
    ```dart
    class Strong
    {
      int strength = 999;
    }
    
    class RunFast
    {
      void run()
      {
        print("Run!");
      }
    }
    
    enum Team { red, blue }
    
    class Player with Strong, RunFast
    {
      Team team;
      
      Player({required this.team});
    }
    
    void main()
    {
      var player = Player(team: Team.red);
      player.strength = 1000;
      player.run();
    }
    ```
