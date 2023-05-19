# 유니티 & C# 코딩 스탠다드
  개발하면서 느낀 점들을 정리하면서 계속 퇴고되고 있는 개인 문서입니다.  
	최대한 지키려고 노력하자..  
  Last Update: 22.02.07

## 기본 원칙
1.	정말 합당한 이유가 있지 않는 한, IDE의 자동 서식을 따른다. (비주얼 스튜디오의 “Ctrl + K + D(자동정렬 기능))

## 참조문서
- Pope Kim의 C# 코딩 표준 스탠다드 : https://docs.popekim.com/ko/coding-standards/csharp
-	언리얼4 코딩스탠다드 : https://docs.unrealengine.com/5.1/en-US/epic-cplusplus-coding-standard-for-unreal-engine/


## C# 코딩 표준
1.	클래스와 구조체의 이름은 파스칼 표기법을 따른다.
```
class GameManager;
class PlayerData;
```
  
2.	지역 변수 그리고 함수의 매개 변수의 이름은 카멜 표기법을 따른다.
```
public void DoSomething(int param)
{
    int num;
    int id;
}
```

3.	함수 이름은 기본적으로 동사+명사의 형태로 짓는다.
```
public void DoSomething()
{
    //TODO...
}
```

4.	단, Bool 값을 반환하는 함수는 Is, Can, Has 등의 참, 거짓 반환의 의미를 내포하고 있어야한다.(ex: 의문형)
```
public bool IsAlive(Person person);
public bool HasChild(Person person);
public bool CanAccept(Person person);
public bool ShouldDelete(Person person);
public bool Exists(Person person);
```

5.	클래스의 멤버변수 앞에는 underscore(_)를 붙인다. Bool 타입의 경우에는 Is, Can, Has 등의 참, 거짓 반환의 의미를 내포하고 있어야 한다. 어려울 경우 변수 앞에 b를 붙인다.
```
public class Stat
{
    private int _hp;
    private int _mp;
    private bool _bFired;
}
```

6.	Getter, Setter 같이 단순 변수 접근을 위한 함수는 프로퍼티로 표현한다. 프로퍼티는 모두 대문자로 시작한다
```
public class Stat
{
    private int _hp;
    private int _mp;
    private bool _isAlive;

    public int Hp => _hp;
    public int Mp => _mp;
    public bool IsAlive
    {
        get { return (_hp > 0); }
    }
}
```

7.	인터페이스를 선언할 때는 대문자 I 를 붙인다.
```
public interface IAttackable;
```

8.	열거형을 선언할 때는 앞에 소문자 e를 붙인다. 내부의 값은 모두 대문자로 쓴다.
```
public enum eDirection
{
    NORTH,
    SOUTH,
}
```

9.	함수 내에서 지역변수를 사용할 때는 그 지역변수를 사용하는 코드와 동일한 줄에 선언한다.
10.	double이 아닌 경우 소수점 값에 f를 붙여준다.
11.	Switch 문에는 언제나 default를 넣는다.
12.	If 중괄호 안의 내용이 한 줄이라도 반드시 중괄호를 적는다.
```
if(IsAlive)
{
    return;
}
```

13.	함수 파라미터로 멤버변수 혹은 지역변수에 동일한 이름이 들어올 경우, 함수 파라미터앞에 In을 붙인다. this를 쓰지 않는다.
```
public void DoSomething(int InCount)
{
    int count; //이미 사용중!!
}
```

14.	함수 반환값이 null이 될 수 있는 경우, 함수 이름 뒤에 OrNull을 붙인다.
```
public string GetNameOrNull();
```

15.	가급적 함수 오버로딩을 피한다.
```
public PlayerData GetPlayerDataByIndex(int index);
public PlayerData GetPlayerDataByName(string name);
```

16.	가급적 partial을 사용하지 않으며, 사용해야 될 경우 파일 이름은 클래스 이름으로 시작하고, 그 뒤에 마침표와 세부 항목 이름을 붙인다.
```
public partial class Human;
Human.Head.cs
Human.Body.cs
Human.Arm.cs
```

17. 한 줄에 변수 하나만 선언한다.

## 유니티 코딩표준
##### 1. 클래스 안에서 멤버변수, 함수의 등장순서는 다음의 규칙을 따른다. 7~9번의 경우 #region을 사용해 구분한다면, 구역별로 해당 순서를 지킨다.
1. [SerializedField]와 같이 인스펙터에서 할당하는 변수  
2. public 멤버변수
3. protected 멤버변수
4. private 멤버변수
5. 프로퍼티 변수
6. 생성자
7. 유니티 메서드(Awake, Start, Update, FixedUpdate etc)
8. public 메서드
9. protected 메서드
10. private 메서드

##### 2. 유니티 Attribute가 붙은 변수는 private을 적지 않을 수 있다.
```
[SerializedField] int _hp;
[SerializedField, Range(0, 10)] int _life;

[SerializedField]
private int _hp;
```  
##### 3. var 키워드는 해당 라인에서 타입 유형을 알 수 있을 때만 사용한다.
```
var player = GetComponent<Player>();
var animator = GetComponent<Animator>();
```
