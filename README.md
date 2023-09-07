## 웹에서 바로 사용해볼 수 있습니다!

[https://yeongo.pages.dev/](https://yeongo.pages.dev/)

### **왜 고연로직이 아니죠?**

"로직"이라는 단어의 바로 앞에 "고"가 붙어야 더 자연스럽습니다. "고"가 "로직"에 더 잘 어울리기 때문에 연고로직이라고 합니다.

## **문법**

> 엄준식 프로그래밍 언어에서 큰 영감을 받았습니다. 왜냐면 제가 만든거거든요..  
> [서강대학교 컴퓨터공학과 23학번 박정한](https://bento.me/3)

하나의 명령어에는 하나의 인자가 대응됩니다. 명령어와 인자는 공백 혹은 개행으로 연결할 수 있으며, 이러한 쌍을 **커맨드**라고 합니다.

`명령어 인자`

연고로직은 커맨드를 나열하여 작성합니다. 각 커맨드는 공백 혹은 개행으로 연결합니다.

`명령어 인자 명령어 인자 명령어 인자 명령어 인자 명령어 인자`

명령어와 인자는 양의 정수입니다. 명령어의 리스트는 후술합니다.

```javascript
3 7
2 9
1 6
```

위 코드는 순차적으로 실행되는 세 개의 커맨드를 가지고 있습니다.

-   3번 명령어 인자를 7로 하여 실행합니다.

-   2번 명령어 인자를 9로 하여 실행합니다.

-   1번 명령어 인자를 6으로 하여 실행합니다.

위 코드의 명령어와 인자를 2진수로 변환한 뒤, 0과 1을 각각 연, 고로 치환해줍니다.

```javascript
고고 고고고     # 3 7 -> 11 111
고연 고연연고   # 2 9 -> 10 1001
고 고고연       # 1 6 -> 1  110
```

### 자료구조

연고로직에서는 **스토리지**(Storage)와 **임시변수**(Temp)에 값을 저장할
수 있습니다. 스토리지는 실수를 저장할 수 있는 리스트이고,
임시변수는 연산을 할 수 있는 장소입니다. 일종의 레지스터와
누산기라고 생각할 수 있습니다.

### **(고급) 견오 표기법**

0과 1을 연과 고로 단순히 치환하면 항상 모든 명령어와 인자의 시작이 고가 되기 때문에 형평성에 어긋납니다. 이러한 문제를 방지하지 위해, 연고로직은 **견오**표기법을 사용합니다.

-   첫 글자는 항상 1로 해석됩니다

-   첫 글자와 같은 글자는 1, 다를 글자는 0으로 해석됩니다

-   그리하여 `연고고연`과 `고연연고`는 모두 9를 나타냅니다.

-   견오표기법은 코드 전체가 아닌 각 명령어와 인자를 파싱할 때 적용됩니다

    -   그리하여 `고연고고고 연고고연고`는 10111 10010으로 해석합니다.

### **명령어**

인자를 편의상 arg라고 표현합니다.

| **명령어** | **설명**                              | **대응되는 코드** |
| ---------- | ------------------------------------- | ----------------- |
| 1          | 너무 고결하여 사용되지 않음           | Holy              |
| 2          | arg를 리턴하고 프로그램을 종료합니다. | `return arg`      |

| **명령어** | **설명**                                    | **대응되는 코드** |
| ---------- | ------------------------------------------- | ----------------- |
| 8          | 임시변수에 arg를 저장합니다                 | `temp = arg`      |
| 9          | 임시변수에 arg를 더해서 저장합니다          | `temp += arg`     |
| 10         | 임시변수에 arg를 빼서 저장합니다            | `temp -= arg`     |
| 11         | 임시변수에 arg를 곱해서 저장합니다          | `temp *= arg`     |
| 12         | 임시변수에 arg를 나눠서 저장합니다          | `temp /= arg`     |
| 13         | 임시변수에 arg를 나머지 연산해서 저장합니다 | `temp %= arg`     |

| **명령어** | **설명**                             | **대응되는 코드** |
| ---------- | ------------------------------------ | ----------------- |
| 16         | 스토리지 커서를 arg로 설정합니다     | `cursor = arg`    |
| 17         | 스토리지 커서를 arg만큼 증가시킵니다 | `cursor += arg`   |
| 18         | 스토리지 커서를 arg만큼 감소시킵니다 | `cursor -= arg`   |

| **명령어** | **설명**                                                                      | **대응되는 코드**         |
| ---------- | ----------------------------------------------------------------------------- | ------------------------- |
| 32         | 현재 참조중인 스토리지의 값을 임시변수에 저장합니다. arg는 무시됩니다.        | `temp = storage[cursor]`  |
| 33         | 임시변수의 값을 현재 참조중인 스토리지에 저장합니다. arg는 무시됩니다.        | `storage[cursor] = temp`  |
| 34         | 임시변수의 값을 현재 참조중인 스토리지에 더해서 저장합니다. arg는 무시됩니다. | `storage[cursor] += temp` |
| 35         | 임시변수의 값을 현재 참조중인 스토리지에 빼서 저장합니다. arg는 무시됩니다.   | `storage[cursor] -= temp` |
| 36         | 임시변수의 값을 현재 참조중인 스토리지에 곱해서 저장합니다. arg는 무시됩니다. | `storage[cursor] *= temp` |
| 37         | 임시변수의 값을 현재 참조중인 스토리지에 나눠서 저장합니다. arg는 무시됩니다. | `storage[cursor] /= temp` |

| **명령어** | **설명**                                                                                       | **대응되는 코드**         |
| ---------- | ---------------------------------------------------------------------------------------------- | ------------------------- |
| 64         | stdin을 정수로 파싱하여 임시변수에 저장합니다. 입력이 numeric하지 않다면 unicode로 변환됩니다. | `temp = int(input())`     |
| 65         | 임시변수를 숫자로 출력합니다                                                                   | `print(temp)`             |
| 66         | 임시변수를 문자로 출력합니다                                                                   | `print(chr(temp))`        |
| 67         | 개행                                                                                           | `print()`                 |
| 72         | 임시변수가 0이라면 arg번째 체크포인트로 이동합니다                                             | `if temp == 0: jump(arg)` |
| 73         | 임시변수가 0이 아니라면 arg번째 체크포인트로 이동합니다                                        | `if temp != 0: jump(arg)` |
| 74         | 현재 코드 실행 위치에 arg번째 체크포인트를 설정합니다                                          | `checkpoint(arg)`         |
