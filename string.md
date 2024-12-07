Python의 **문자열(string)**은 매우 중요한 데이터 유형 중 하나입니다. 문자열은 **변경할 수 없는(immutable)** 데이터 유형이므로, 문자열을 "수정"하는 메서드는 항상 수정된 문자열의 **복사본**을 반환하며, 원본 문자열은 변경되지 않습니다. 따라서, 문자열 메서드 사용 시 결과를 저장하거나, 원본을 그대로 유지할지 여부를 고려해야 합니다.

아래에서는 문자열 메서드의 주요 기능과 사용 방법을 **한글로 자세히** 설명하겠습니다.

---

## **1. 문자열 "수정" 메서드**

이 그룹의 메서드는 문자열을 특정 방식으로 변환한 **새 문자열을 반환**합니다. 원본 문자열은 변경되지 않습니다.

### **문법**
```python
string.method_name(arguments)
```
또는
```python
variable_name.method_name(arguments)
```
- `string` 또는 `variable_name`은 문자열.
- `method_name`은 호출할 메서드 이름.
- `arguments`는 선택적으로 필요한 인자.

---

### **주요 메서드**

1. **`str.replace(old, new, count)`**
   - 문자열의 **일부를 다른 문자열로 교체**합니다.
   - `count`는 선택 사항으로, 지정된 경우 처음 `count`개의 일치하는 부분만 교체.

   ```python
   message = "hello world"
   print(message.replace("world", "Python"))  # hello Python
   print(message.replace("o", "O", 1))       # hellO world
   ```

2. **`str.upper()`**
   - 문자열을 모두 **대문자**로 변환.

   ```python
   message = "hello"
   print(message.upper())  # HELLO
   ```

3. **`str.lower()`**
   - 문자열을 모두 **소문자**로 변환.

   ```python
   message = "HELLO"
   print(message.lower())  # hello
   ```

4. **`str.title()`**
   - **각 단어의 첫 글자를 대문자로 변환**.

   ```python
   message = "hello world"
   print(message.title())  # Hello World
   ```

5. **`str.swapcase()`**
   - **대문자는 소문자로, 소문자는 대문자로 변환**.

   ```python
   message = "Hello World"
   print(message.swapcase())  # hELLO wORLD
   ```

6. **`str.capitalize()`**
   - 문자열의 **첫 글자를 대문자로, 나머지는 소문자로 변환**.

   ```python
   message = "hELLO wORLD"
   print(message.capitalize())  # Hello world
   ```

---

### **예제**
```python
message = "bonjour and welcome to Paris!"

# 대문자로 변환
print(message.upper())  # BONJOUR AND WELCOME TO PARIS!

# 각 단어의 첫 글자를 대문자로 변환
title_message = message.title()
print(title_message)  # Bonjour And Welcome To Paris!

# 문자열 교체
replaced_message = message.replace("Paris", "Lyon")
print(replaced_message)  # bonjour and welcome to Lyon!

# 원본 문자열은 그대로 유지됨
print(message)  # bonjour and welcome to Paris!
```

---

## **2. 문자열에서 문자 제거**

입력 문자열에서 불필요한 문자나 공백을 제거해야 할 때 사용할 수 있는 메서드들입니다.

### **주요 메서드**

1. **`str.lstrip([chars])`**
   - 문자열의 **왼쪽**에서 특정 문자를 제거.
   - `chars`를 지정하지 않으면 **공백 제거**.

   ```python
   whitespace_string = "   hello"
   print(whitespace_string.lstrip())  # "hello"
   print("!!hello!!".lstrip("!"))     # "hello!!"
   ```

2. **`str.rstrip([chars])`**
   - 문자열의 **오른쪽**에서 특정 문자를 제거.
   - `chars`를 지정하지 않으면 **공백 제거**.

   ```python
   whitespace_string = "hello   "
   print(whitespace_string.rstrip())  # "hello"
   print("hello!!".rstrip("!"))       # "hello"
   ```

3. **`str.strip([chars])`**
   - 문자열의 **양쪽**에서 특정 문자를 제거.
   - `chars`를 지정하지 않으면 **공백 제거**.

   ```python
   whitespace_string = "   hello   "
   print(whitespace_string.strip())  # "hello"
   print("!!hello!!".strip("!"))     # "hello"
   ```

---

### **예제**
```python
whitespace_string = "     hey      "
normal_string = "incomprehensibilities"

# 왼쪽 공백 제거
print(whitespace_string.lstrip())  # "hey      "

# 오른쪽 공백 제거
print(whitespace_string.rstrip())  # "     hey"

# 양쪽 공백 제거
print(whitespace_string.strip())  # "hey"

# 특정 문자 제거
print(normal_string.lstrip("is"))  # "ncomprehensibilities"
print(normal_string.rstrip("is"))  # "incomprehensibilitie"
print(normal_string.strip("is"))   # "ncomprehensibilitie"
```

---

### **주의사항**
- `strip()`, `lstrip()`, `rstrip()`은 **모든 가능한 조합**의 문자를 제거하므로, 결과가 예기치 않게 비어있을 수 있습니다.

#### **예제**
```python
word = "Mississippi"

# 오른쪽에서 "i", "p", "s" 제거
print(word.rstrip("ips"))  # "M"

# 양쪽에서 "M", "i", "p", "s" 제거
print(word.strip("Mips"))  # ""
```

---

## **3. 문자열 메서드 사용 시 유의사항**

1. **문자열은 변경 불가능(immutable)**:
   - 메서드를 호출하면 **새 문자열**이 반환되며, 원본은 변경되지 않습니다.
   - 수정된 결과를 저장하려면 **새 변수에 할당**해야 합니다.

2. **원본 유지**:
   - 원본 문자열이 필요하다면 수정된 결과를 다른 변수에 저장하세요.

3. **한 번만 사용할 경우**:
   - 결과를 저장하지 않고 바로 사용할 수도 있습니다.
   - 예: `print(message.upper())`

---

## **4. 요약**

- **문자열 "수정" 메서드**: `replace()`, `upper()`, `lower()`, `title()`, `swapcase()`, `capitalize()`.
- **문자열에서 문자 제거 메서드**: `strip()`, `lstrip()`, `rstrip()`.
- **불변성**: 문자열은 변경되지 않으므로, 수정된 문자열은 새 변수에 저장해야 함.

Python 문자열 메서드는 텍스트를 조작하는 데 강력한 도구를 제공합니다. 추가적으로 궁금한 점이 있다면 알려주세요! 😊