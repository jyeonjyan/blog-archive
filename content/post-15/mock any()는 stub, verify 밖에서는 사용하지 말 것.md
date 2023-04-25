![](../../assets/15/mockito.png)

## 목표
* mock `argument matchers`를 사용할 수 있는 범위를 알 수 있다.
* 에러가 발생하는 경우를 알고 성공적으로 테스트를 고칠 수 있다.


## 구성
* org.springframework.boot:spring-boot-starter-test
* springmockk:2.0.3

## 문제 상황 및 해결 방법

```kotlin
@Test
@DisplayName("이 테스트는 실패한다.")
fun thisTestWillBeFail() {
    // stubbing
    val someObj = mockk<SomethingObj>()
    every { someObj.findSomething(any()) } returns "Something"

    // Given
    val sut = somethingService()

    // When, Then
    assertDoesNotThrow { sut.doA(anyString()) }
}
```

이 테스트는 아래와 같은 오류를 내며 결국 실패한다.
```plain_text
Failed to load ApplicationContext
java.lang.IllegalStateException: Failed to load ApplicationContext

/** 생략 **/

You cannot use argument matchers outside of verification or stubbing.
Examples of correct usage of argument matchers:
    when(mock.get(anyInt())).thenReturn(null);
    doThrow(new RuntimeException()).when(mock).someVoidMethod(anyObject());
    verify(mock).someMethod(contains("foo"))

This message may appear after an NullPointerException if the last matcher is returning an object 
like any() but the stubbed method signature expect a primitive argument, in this case,
use primitive alternatives.
    when(mock.get(any())); // bad use, will raise NPE
    when(mock.get(anyInt())); // correct usage use

This message may appear after an NullPointerException if the last matcher is returning an object 
like any() but the stubbed method signature expect a primitive argument, in this case,
use primitive alternatives.
    when(mock.get(any())); // bad use, will raise NPE
    when(mock.get(anyInt())); // correct usage use

Also, this error might show up because you use argument matchers with methods that cannot be mocked.
Following methods *cannot* be stubbed/verified: final/private/equals()/hashCode().
Mocking methods declared on non-public parent classes is not supported.
```

음 이 에러가 뜨는 이유가 뭘까?  

이 오류가 발생하면 이 예외가 발생할 수 있는 여러 케이스들을 모두 안내해주기 때문에 어디가 잘못 됐는지 쉽게 발견하기 어렵다.

여기서는 `You cannot use argument matchers outside of verification or stubbing.` 문장에 집중해야한다. **`verification or stubbing` 에서만 `argument matchers` 사용이 가능하다고 볼 수 있다.**

이 내용을 기반으로 내가 위에 작성한 테스트 코드를 차근차근 뜯어보자 
* `stubbing` 부분에서 (`every { someObj.findSomething(any()) }`) 사용한 `argument matchers` = `any()`는 mock 객체에 stubbing을 수행하며 사용한것이기에 문제가 없다.
* 테스트 함수(`SUT`)를 호출하는 부분(**에러에서 말하는 outside**)에서 `sut.doA(anyString())` `anyString()` 이라는 `argument matchers` 를 사용한 것은 문제가 있다.

그렇다면 아래와 같이 코드를 수정할 수 있다.
```kotlin
@Test
@DisplayName("이 테스트는 성공한다.")
fun thisTestWillBeFail() {
    // stubbing
    val someObj = mockk<SomethingObj>()
    every { someObj.findSomething(any()) } returns "Something"

    // Given
    val sut = somethingService()

    // When, Then
    assertDoesNotThrow { sut.doA("blah blah") }
}
```

이렇게 되면 테스트 대상(SUT)에 문자열 `"blah blah"`를 실제로 전달하여, mock 라이브러리에서 제공하는 `argument matcher`를 사용하지 않게 되고, 이를 통해 해당 오류를 궁극적으로 해결할 수 있게 됩니다.

### ps

Q: 근데.. 첫번째 제시해준 테스트도 어쩔때는 성공하고 어쩔때는 실패해요..!  
A: 내 로컬에서도 간헐적으로 그런 현상이 발생했다. 근데 간헐적으로 성공하는 이유를 알아내는것 그리고 그 노력은 중요하지 않다. verify, stub을 제외하고는 사용하지 않는게 맞기 때문이다.


읽어주셔서 감사합니다.