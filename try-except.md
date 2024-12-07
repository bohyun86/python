예외 처리는 Python에서 **사용자 입력**과 같은 **통제하기 어려운 부분**을 안전하게 처리할 수 있는 중요한 도구입니다. 예외 처리를 잘 활용하면 프로그램이 **예상치 못한 오류** 때문에 중단되지 않도록 방지할 수 있습니다. 이번 주제에서는 Python의 **try-except 구문**을 사용하여 오류를 처리하는 방법을 배워봅시다.

### 1. 예외 상황을 다루는 예시: 간단한 나눗셈 계산기
다음과 같은 간단한 나눗셈 계산기를 생각해봅시다. 사용자가 두 숫자를 입력하면 나누기 연산을 수행하는 프로그램입니다:

```python
number_one = int(input("첫 번째 숫자를 입력하세요: "))
number_two = int(input("두 번째 숫자를 입력하세요: "))
result = number_one / number_two
print("나눗셈 결과: ", result)
```

정상적으로 숫자를 입력할 경우 잘 작동합니다:

```
첫 번째 숫자를 입력하세요: 5
두 번째 숫자를 입력하세요: 2
나눗셈 결과: 2.5
```

그러나 **0으로 나누기**와 같은 불가능한 연산을 시도하면 어떻게 될까요?

```
첫 번째 숫자를 입력하세요: 5
두 번째 숫자를 입력하세요: 0
Traceback (most recent call last):
  ...
ZeroDivisionError: division by zero
```

프로그램이 **충돌**하며, 오류 메시지가 나타납니다. 이를 방지하기 위해 **try-except 구문**을 사용할 수 있습니다.

### 2. 예외 처리 구문 사용하기: try-except
위 코드에서 나눗셈이 발생하는 부분을 **try-except 블록**으로 감싸면 오류 발생 시 프로그램이 중단되지 않도록 할 수 있습니다:

```python
number_one = int(input("첫 번째 숫자를 입력하세요: "))
number_two = int(input("두 번째 숫자를 입력하세요: "))

try:
    result = number_one / number_two
except ZeroDivisionError:
    print("예외 처리 결과 ***0으로 나눌 수 없습니다!")
else:
    print("나눗셈 결과: ", result)
finally:
    print("마무리 작업 ***계산기를 사용해 주셔서 감사합니다!")
```

#### 각 키워드의 역할
- **try**: 여기서 정의된 코드 블록을 실행하려고 시도합니다.
- **except**: **예외가 발생**하면, 지정된 예외에 해당하는 코드를 실행합니다.
- **else**: **예외가 발생하지 않았을 때** 실행됩니다. 주로 try에서 오류 없이 정상적으로 실행되었을 때 다음 작업을 정의하는 데 유용합니다.
- **finally**: **예외가 발생하든 안 하든 항상 실행**되는 코드입니다. 주로 자원 해제, 파일 닫기 등 마무리 작업에 사용됩니다.

이제 프로그램을 다시 실행해 보면, 0으로 나누기를 시도하더라도 예외 처리 덕분에 프로그램이 멈추지 않고 처리됩니다:

```
첫 번째 숫자를 입력하세요: 5
두 번째 숫자를 입력하세요: 0
예외 처리 결과 ***0으로 나눌 수 없습니다!
마무리 작업 ***계산기를 사용해 주셔서 감사합니다!
```

### 3. 여러 예외 처리하기
사용자가 숫자 대신 잘못된 값을 입력하면 어떻게 될까요?

```
첫 번째 숫자를 입력하세요: 5
두 번째 숫자를 입력하세요: one
Traceback (most recent call last):
  ...
ValueError: invalid literal for int() with base 10: 'one'
```

이 경우 **ValueError**가 발생합니다. 이 문제를 해결하려면 **여러 개의 except 블록**을 사용할 수 있습니다:

```python
try:
    result = number_one / number_two
except ZeroDivisionError:
    print("예외 처리 결과 ***0으로 나눌 수 없습니다!")
except ValueError:
    print("숫자만 입력하세요!")
```

또는 **여러 예외를 한꺼번에 처리**할 수도 있습니다:

```python
except (ValueError, TypeError):
    print("숫자만 입력 가능합니다!")
```

### 4. 일반적인 예외 처리하기
모든 예외를 예측하기 어렵다면 **가장 일반적인 예외 처리**를 사용할 수 있습니다. 예를 들어, **Exception** 클래스를 사용하면 대부분의 예외를 포괄적으로 처리할 수 있습니다:

```python
except Exception:
    print("알 수 없는 오류가 발생했습니다. 다시 시도하세요!")
```

이렇게 하면 **GeneratorExit**, **KeyboardInterrupt**, **SystemExit**을 제외한 대부분의 예외를 처리할 수 있으며, 프로그램이 갑자기 종료되지 않도록 방지할 수 있습니다.

### 5. 정리
- Python에서는 예외 상황을 처리하기 위해 **try-except 블록**을 사용합니다.
- **else 블록**은 예외가 발생하지 않았을 때 실행되며, **finally 블록**은 예외와 상관없이 항상 실행됩니다.
- 여러 개의 **except 블록**을 사용하여 다양한 예외를 처리할 수 있으며, **Exception** 클래스를 사용하여 대부분의 예외를 포괄적으로 처리할 수 있습니다.
- 이러한 예외 처리를 잘 활용하면 프로그램이 더욱 **안정적**이고 **효율적**으로 동작하도록 만들 수 있습니다.

예외 처리는 프로그램을 견고하게 만들어주며, **사용자의 예측 불가능한 입력**이나 **환경적인 요인**으로 인해 발생할 수 있는 오류를 잘 처리하여 프로그램이 멈추지 않고 안전하게 동작하도록 도와줍니다. 😊