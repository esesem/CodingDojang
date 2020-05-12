 Computational Thinking
 ======================

1. **분해**: 복잡한 문제를 작은 문제로 나눈다.
2. **패턴 인식**: 문제 안에서 유사성을 발견한다.
3. **추상화**: 문제의 핵심에만 집중하고 부차적인 것은 제외한다.
4. **알고리즘**: 이렇게 정의한 문제를 해결하는 절차이다.

복잡한 문제를 해결하는 것은 어렵지만, 작은 문제를 해결하는 것은 비교적 쉽다. 작은 문제를 해결하다 보면 복잡한 문제를 해결하게 된다. 컴퓨터 공학에서 배우는 알고리즘은 대부분 정형화된 문제에 대해 검증된 해법을 제시하는 과목이다.

현실에서 컴퓨터로 해결하려는 문제는 정형화된 문제가 아니라 비정형화된 문제가 더 많다. 그래서 비정형화된 문제를 컴퓨터로 해결하는 과정, 즉 문제를 이해하고 분해, 패턴 인식, 추상화, 알고리즘 작성까지를 컴퓨테이셔널 씽킹이라고 한다.





Short-Circuit Evalution
=======================

논리 연산에서 중요한 부분이 **단락 평가(short-circuit evalution)**이다. 단락 평가는 첫 번째 값만으로 결과가 확실할 때 두 번째 값은 확인(평가)하지 않는 방법을 말한다. 즉, `and` 연산자는 두 값이 모두 참이라야 참이므로 첫 번째 값이 거짓이면 두 번째 값은 확인하지 않고 바로 거짓으로 결정한다.

```python
# 첫 번째 값이 거짓이므로 두 번째 값은 확인하지 않고 거짓으로 결정
print(False and True)           # False
print(False and False)          # False
```

`or` 연산자는 두 값 중 하나만 참이므로 첫 번째 값이 참이면 두 번째 값은 확인하지 않고 바로 참으로 결정한다.

```python
# 첫 번째 값이 참이므로 두 번째 값은 확인하지 않고 참으로 결정
print(True or True)             # True
print(True or False)            # True
```

특히 파이썬에서 논리 연산자는 이 단락 평가에 따라 반환하는 값이 결정된다. `True`, `False`를 논리 연산자로 확인하면 `True`, `False`가 나왔는데, `True and 'Python'`의 결과는 무엇이 나올까?

```python
True and 'Python'               # 'Python'
```

문자열 `'Python'`도 bool로 따지면 `True`라서 `True and True`가 되어 `True`가 나올 것 같지만 `'Python'`이 나온다. 왜냐하면 파이썬에서 논리 연산자는 마지막으로 단락 평가를 실시한 값을 그대로 반환하기 때문이다. 따라서 논리 연산자는 무조건 bool을 반환하지 않는다.

다음과 같이 마지막으로 단락 평가를 실시한 값이 bool이면 bool을 반환하게 된다.

```python
'Python' and True               # True
'Python' and False              # False
```



딕셔너리의 키의 순서
====================

파이썬 3.5 이하에서는 키의 순서가 정해져 있지 않다. 하지만, 파이썬 3.6부터는 딕셔너리를 생성했을 때와 키를 추가했을 때의 순서를 따르므로 순서가 보장된다.



```python
# 파이썬 3.6
>>> lux = {'health': 490, 'health': 800, 'mana': 334, 'melee': 550, 'armor': 18.72}
>>> lux
{'health': 490, 'health': 800, 'mana': 334, 'melee': 550, 'armor': 18.72}
```

```python
# 파이썬 3.5
>>> lux = {'health': 490, 'health': 800, 'mana': 334, 'melee': 550, 'armor': 18.72}
>>> lux
{'armor': 18.72, 'health': 800, 'health': 490, 'melee': 550}
```

만약 파이썬 3.5 이하에서 키의 순서가 보장되도록 만들려면 `collections` 모듈의 `OrderedDict`를 사용하면 된다.

```python
>>> from collections import OrderedDict
>>> lux = OrderedDict({'health': 490, 'health': 800, 'mana': 334, 'melee': 550, 'armor': 18.72})
>>> lux
OrderedDict([('health', 800), ('mana', 334), ('melee', 550), ('armor', 18.72)])
```

사실 `OrderedDict`는 키의 순서를 보장하기 위해 사용하는 것이 아니라, 딕셔너리를 키로 정렬하고 싶을 때 사용한다. 그래서 파이썬 3.6에도 여전히 `OrderedDict`가 남아있다.