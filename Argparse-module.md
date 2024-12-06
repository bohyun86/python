이번 주제에서는 Python의 **`argparse` 모듈**을 사용하여 **명령줄 인수(command line arguments)**를 다루는 방법에 대해 알아보겠습니다. `argparse`는 Python에서 프로그램을 더 사용자 친화적으로 만들기 위해 자주 사용되는 도구로, 사용자가 명령줄에서 직접 필요한 매개변수와 값을 지정할 수 있도록 합니다. 이를 통해 프로그램은 사용자가 제공한 인수를 받아 처리하고, 유연하게 동작할 수 있습니다.

### 1. `argparse` 시작하기

#### 1.1 모듈 불러오기
먼저 **`argparse` 모듈**을 불러옵니다. 이 모듈은 사용자가 프로그램을 실행할 때 **명령줄 인수**를 정의하고 사용할 수 있도록 도와줍니다.

```python
import argparse
```

#### 1.2 `ArgumentParser` 객체 생성
다음으로는 **`ArgumentParser` 객체**를 생성합니다. 이 객체는 프로그램에서 사용할 **모든 인수 정보**를 저장하게 됩니다.

```python
parser = argparse.ArgumentParser(description="이 프로그램은 제공한 재료를 바탕으로 레시피를 출력합니다.")
```

- **`ArgumentParser`**는 Python에서 **클래스**로 정의된 객체입니다.
- `description` 매개변수는 프로그램의 용도를 설명하는 데 사용됩니다. 이는 사용자에게 프로그램의 목적을 이해시키는 데 도움이 됩니다.

### 2. 인수 추가하기 (`add_argument` 메서드 사용)

#### 2.1 인수 추가
이제 **`add_argument()`** 메서드를 사용하여 인수를 추가할 수 있습니다.

```python
parser.add_argument("-i1", "--ingredient_1")  # 선택적 인수 (옵션)
parser.add_argument("ingredient_1")           # 위치 인수
```

- **옵션 인수**는 **`-` 또는 `--`**로 시작하는 인수입니다. 예를 들어, `-i1` 또는 `--ingredient_1`처럼 사용할 수 있습니다.
  - 일반적으로 단일 대시(`-`)는 짧은 버전의 이름을, 이중 대시(`--`)는 전체 이름을 나타냅니다.
- **위치 인수**는 **접두사 없이** 사용되며, 항상 사용자가 제공해야 하는 인수입니다. 예를 들어 `ingredient_1`처럼 사용할 수 있습니다.

#### 2.2 액션 파라미터 (`action` 파라미터)
특정 상황에서, **`action` 파라미터**를 사용하여 인수의 동작을 정의할 수 있습니다.

```python
parser.add_argument("--salt", action="store_true")
```

- 위 코드에서는 `--salt` 인수가 **`True`**로 설정되면 소금을 사용할 수 있게 설정합니다.
- **`action="store_true"`**는 해당 인수가 제공되면 **`True`** 값을 저장하고, 그렇지 않으면 **`False`**로 설정됩니다.
- 반대로 **`action="store_false"`**를 사용하면 기본값이 `True`이고, 인수가 제공되면 `False`로 설정됩니다.

#### 2.3 기본값 설정 (`default` 파라미터)
**기본값**을 설정하려면 **`default`** 파라미터를 사용할 수 있습니다.

```python
parser.add_argument("--pepper", default=False)
```

- 위 코드에서 **`--pepper`**의 기본값은 **`False`**입니다.
- 사용자가 명령줄에서 값을 명시하지 않으면 기본값이 사용됩니다.

#### 2.4 선택 항목 제한 (`choices` 파라미터)
인수의 값을 특정 항목으로 **제한**하고 싶을 때는 **`choices`** 파라미터를 사용할 수 있습니다.

```python
parser.add_argument("-i2", "--ingredient_2",
                    choices=["pasta", "rice", "potato", "onion",
                             "garlic", "carrot", "soy_sauce", "tomato_sauce"],
                    help="목록에서 하나의 재료를 선택해야 합니다.")
```

- **`choices`**를 사용하면 사용자가 지정된 **리스트 내의 값**만 사용할 수 있게 됩니다.
- **`help`**는 사용자에게 인수 사용법을 안내하는 간단한 설명을 제공합니다.

### 3. 인수 파싱하기 (`parse_args` 메서드)

#### 3.1 `parse_args()` 사용하기
**`parse_args()`** 메서드를 사용하여 명령줄에서 전달된 인수를 **파싱**합니다.

```python
args = parser.parse_args()
```

- 이제 `args` 객체를 통해 사용자가 제공한 인수의 **값**에 접근할 수 있습니다.
- 예를 들어 **`args.ingredient_2`**를 사용하면 `ingredient_2`에 전달된 값을 얻을 수 있습니다.

### 4. 전체 코드 예제 (`recipe_book.py`)

다음은 설명한 모든 내용을 포함한 전체 코드입니다.

```python
import argparse

# ArgumentParser 객체 생성
parser = argparse.ArgumentParser(description="이 프로그램은 제공한 재료를 바탕으로 레시피를 출력합니다.")

# 인수 추가
parser.add_argument("-i1", "--ingredient_1", choices=["pasta", "rice", "potato",
                    "onion", "garlic", "carrot", "soy_sauce", "tomato_sauce"],
                    help="목록에서 하나의 재료를 선택해야 합니다.")
parser.add_argument("-i2", "--ingredient_2", choices=["pasta", "rice", "potato",
                    "onion", "garlic", "carrot", "soy_sauce", "tomato_sauce"],
                    help="목록에서 하나의 재료를 선택해야 합니다.")
parser.add_argument("--salt", action="store_true", help="소금을 사용하려면 이 인수를 지정하세요.")
parser.add_argument("--pepper", default="False", help="후추를 사용하려면 'True'로 변경하세요.")

# 인수 파싱
args = parser.parse_args()

# 인수로 받은 재료 리스트 생성
ingredients = [args.ingredient_1, args.ingredient_2]
if args.salt:
    ingredients.append("salt")
if args.pepper == "True":
    ingredients.append("pepper")

# 결과 출력
print(f"제공한 재료는 다음과 같습니다: {ingredients}")
```

### 5. 명령줄에서 프로그램 실행하기

#### 5.1 명령줄 예시
이제 명령줄에서 프로그램을 실행해 봅시다. 다음은 사용자가 제공한 인수의 예시입니다:

```sh
python recipe_book.py -i1 rice -i2 onion --salt
# 출력:
# 제공한 재료는 다음과 같습니다: ['rice', 'onion', 'salt']
```

이 예시에서는 사용자가 `rice`와 `onion`을 재료로 선택하고, 소금을 추가하기 위해 `--salt` 인수를 지정했습니다.

### 6. 도움말 옵션 (`--help` 또는 `-h`)

#### 6.1 도움말 메시지 보기
명령줄에서 **`--help`** 또는 **`-h`**를 입력하면 프로그램의 사용법에 대한 정보를 볼 수 있습니다.

```sh
python recipe_book.py --help
# 출력:
# usage: recipe_book.py [-h] [-i1 {pasta,rice,potato,onion,garlic,carrot,soy_sauce,tomato_sauce}]
#                       [-i2 {pasta,rice,potato,onion,garlic,carrot,soy_sauce,tomato_sauce}]
#                       [--salt] [--pepper]
#
# 이 프로그램은 제공한 재료를 바탕으로 레시피를 출력합니다.
# 
# 선택적 인수:
#   -h, --help            도움말 메시지를 표시하고 종료합니다.
#   -i1, --ingredient_1   목록에서 하나의 재료를 선택해야 합니다.
#   -i2, --ingredient_2   목록에서 하나의 재료를 선택해야 합니다.
#   --salt                소금을 사용하려면 이 인수를 지정하세요.
#   --pepper              후추를 사용하려면 'True'로 변경하세요.
```

### 요약
이번 주제에서는 Python의 **`argparse`** 모듈을 사용하여 명령줄 인수를 처리하는 방법을 살펴보았습니다.
- **`ArgumentParser` 객체**를 생성하여 프로그램에 필요한 인수를 정의합니다.
- **`add_argument()` 메서드**를 사용하여 인수를 추가하고, **`parse_args()`**를 사용하여 인수를 파싱합니다.
- 사용자는 명령줄을 통해 프로그램에 다양한 값을 전달할 수 있으며, 이를 통해 프로그램의 유연성과 사용자 편의성을 높일 수 있습니다.

이러한 기능은 Python으로 작성한 프로그램을 **더 범용적이고 사용자 친화적**으로 만들어 줄 것입니다. 😊