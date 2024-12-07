### **파이썬의 문자열과 리스트 변환**

파이썬에서 문자열과 리스트는 둘 다 시퀀스(Sequence) 타입입니다. 문자열은 문자만 포함하는 반면, 리스트는 다양한 데이터 타입을 담을 수 있다는 점이 차이점입니다. 하지만 필요에 따라 문자열을 리스트로, 또는 리스트를 문자열로 변환해야 하는 경우가 있습니다. 파이썬에서는 이를 위해 **`split()`**, **`join()`**, **`splitlines()`**와 같은 메서드를 제공합니다.

---

## **1. 문자열을 리스트로 변환**

### **1.1 `split()` 메서드**
`split()` 메서드는 문자열을 특정 구분자를 기준으로 나누어 리스트로 반환합니다.

#### **기본 동작**
- **구분자(Separator):** 구분자를 지정하지 않으면 **공백**이 기본값으로 사용됩니다.
- **반환 값:** 나뉜 문자열의 부분 문자열 리스트를 반환하며, 구분자는 결과에 포함되지 않습니다.

```python
definition = "Coin of the realm is the legal money of the country"

print(definition.split())  
# ['Coin', 'of', 'the', 'realm', 'is', 'the', 'legal', 'money', 'of', 'the', 'country']

print(definition.split("legal"))  
# ['Coin of the realm is the ', ' money of the country']
```

#### **`maxsplit` 매개변수**
`split()` 메서드에는 나누는 횟수를 제한하는 `maxsplit` 매개변수가 있습니다.
- **기본값:** 모든 가능한 경우를 나눕니다.
- **`maxsplit`:** 나누는 횟수를 제한하며, 리스트의 요소 수는 `maxsplit + 1`이 됩니다.

```python
print(definition.split("of", 1))
# ['Coin ', ' the realm is the legal money of the country']

print(definition.split("of"))
# ['Coin ', ' the realm is the legal money ', ' the country']
```

#### **구분자가 없는 경우**
지정한 구분자가 문자열에 없으면 원래 문자열을 그대로 포함하는 리스트를 반환합니다.

```python
print(definition.split("hi!"))
# ['Coin of the realm is the legal money of the country']
```

#### **입력을 여러 변수에 나누기**
입력값을 `split()`을 이용해 변수 여러 개에 바로 할당할 수도 있습니다.

```python
name, surname = input().split()  # 입력: Forrest Gump

print(name)     # Forrest
print(surname)  # Gump
```

주의: 입력값의 개수가 변수의 개수와 일치하지 않으면 **`ValueError`**가 발생합니다.

---

## **2. 리스트를 문자열로 변환**

### **2.1 `join()` 메서드**
`join()` 메서드는 리스트와 같은 **반복 가능한(iterable)** 객체를 문자열로 변환합니다.
- **구분자(Separator):** 결과 문자열에서 각 요소를 연결하는 데 사용됩니다.
- **요소 타입:** 반복 가능한 객체의 모든 요소가 **문자열**이어야 합니다.

```python
word_list = ["dog", "cat", "rabbit", "parrot"]

print(" ".join(word_list))       # "dog cat rabbit parrot"
print("".join(word_list))        # "dogcatrabbitparrot"
print("_".join(word_list))       # "dog_cat_rabbit_parrot"
print(" and ".join(word_list))   # "dog and cat and rabbit and parrot"
```

#### **숫자 리스트를 문자열로 변환**
리스트의 요소가 문자열이 아닌 경우(예: 정수) 변환하기 전에 **명시적으로 문자열로 변환**해야 합니다.

```python
int_list = [1, 2, 3]
# print(" ".join(int_list))  # TypeError 발생!

str_list = [str(i) for i in int_list]
print(" ".join(str_list))  # "1 2 3"
```

---

## **3. 여러 줄 문자열 분리**

### **3.1 `splitlines()` 메서드**
`splitlines()` 메서드는 문자열을 줄 바꿈 기준으로 나누어 리스트로 반환합니다.
- **기본 동작:** 줄 바꿈 문자를 기준으로 분리.
- **`keepends` 매개변수:** 줄 바꿈 문자를 포함하려면 `True`로 설정.

```python
long_text = "first line\nsecond line\rthird line\r\nfourth line"

print(long_text.splitlines())
# ['first line', 'second line', 'third line', 'fourth line']

print(long_text.splitlines(keepends=True))
# ['first line\n', 'second line\r', 'third line\r\n', 'fourth line']
```

---

## **4. 문자열 메서드 연결(Chaining)**

문자열 메서드는 연결(chaining)하여 사용할 수 있습니다. 예를 들어, 문자열을 소문자로 변환한 뒤 공백 기준으로 나누는 작업을 한 줄로 처리할 수 있습니다.

```python
sent = "Mary had a little lamb"
new_sent = sent.lower().split()
print(new_sent)
# ['mary', 'had', 'a', 'little', 'lamb']
```

### **주의 사항**
1. **순서:** 메서드의 순서에 따라 결과가 달라질 수 있습니다.
   ```python
   sent.split().lower()  
   # AttributeError: 'list' object has no attribute 'lower'
   ```
2. **PEP 8 준수:** 한 줄의 길이가 79자를 넘지 않도록 유지하세요.

---

## **5. 요약**

### **문자열 -> 리스트**
- **`split(separator, maxsplit)`**: 문자열을 구분자로 나누어 리스트로 반환.
- **`splitlines(keepends)`**: 줄 바꿈 기준으로 나누어 리스트로 반환.

### **리스트 -> 문자열**
- **`join(separator)`**: 리스트를 구분자로 연결하여 문자열로 변환.

### **주요 사항**
1. 문자열 메서드는 **원본 문자열을 변경하지 않음**.
2. 변환된 결과를 재사용하려면 변수에 저장.
3. 필요한 경우 `print()`로 직접 출력 가능.
4. 더 세부적인 기능은 [공식 문서](https://docs.python.org/3/library/stdtypes.html#string-methods)를 참조.

이제 문자열과 리스트 간 변환을 자유자재로 다룰 수 있을 것입니다! 😊