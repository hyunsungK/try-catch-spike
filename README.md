# TRY CATCH

 Try-Catch를 어떻게 사용하면 좋을까? 일반적인 Try-Catch의 Golden Rule을 두 가지로 나뉜다.
 
 - 1. 가장 작게 발생 지점에서 예외를 잡고 처리한다.
 - 2. 일반적인 프로시저 언어에서 가장 밖에서 예외를 잡아서 처리한다.

<br/>

해당 문서에서는 이런 추상적인 표현보다는 구체적인 패턴으로 나눠서 기억과 활용을 돕도록 해보겠다.

## Patterns

어떤 패턴들이 있는지 살펴 보자.

### The “Big Tarp” Pattern

```
try:
    main_loop()
except Exception:
    logger.exception("Fatal error in main loop")
```


### The “Pinpoint” Pattern

```
from openburrito import find_burrito_joints, BurritoCriteriaConflict
# "criteria" is an object defining the kind of burritos you want.
try:
    places = find_burrito_joints(criteria)
except BurritoCriteriaConflict as err:
    logger.warn("Cannot resolve conflicting burrito criteria: {}".format(err.message))
    places = list()
```

### The “Transformer” Pattern

```
try:
    something()
except SomeError as err:
    logger.warn("...")
    raise DifferentError() from err
In Python 2, you must drop the “from err”:

try:
    something()
except SomeError as err:
    logger.warn("...")
    raise DifferentError()
```

### The “Message and Raise” Pattern

```
try:
    something()
except SomeError:
    logger.warn("...")
    raise
```



## Reference
- [Golen Rule](https://stackoverflow.com/questions/14973642/how-using-try-catch-for-exception-handling-is-best-practice/14980639)
- [Pattern](https://www.loggly.com/blog/exceptional-logging-of-exceptions-in-python/)