# 배열
배열은 같은 종류의 데이터들이 순차적으로 저장되어 있는 자료구조를 뜻한다.<br/>
## 배열 선언과 초기화
```java
int[ ] studentIDs = new int[10]; //int형 요소가 10개인 배열을 선언
int[ ] studentIDs = new int[ ] {101, 102, 103}; //int형 요소가 3개인 배열을 선언과 동시에 101, 102, 103으로 초기화
```
자바에서 배열을 선언하면 그와 동시에 각 요소의 값이 정수는 0, 실수는 0.0, 객체 배열은 null로 초기화된다. 

## length
자바에서 배열 길이는 처음에 선언한 배열의 전체 요소 개수를 의미한다. 전체 길이를 알고 싶은 배열 이름 뒤에 도트(.) 연산자를 붙이고 length 속성을 쓰면 배열 길이를 반환한다. 하지만 배열을 사용할 때 처음 선언한 배열 길이만큼 값을 저장해서 사용하는 경우는 많지 않다. 따라서 **전체 배열 길이**와 **현재 배열에 유효한 값이 저장되어 있는 배열 요소 개수**가 같다고 혼동하면 안된다. 
```java
public class Array {

	public static void main(String[] args) {
		double[ ] data =  new double[5];
		
		data[0] = 10.0;
		data[1] = 20.0;
		data[2] = 30.0;
		
		for(int i = 0; i < data.length; i++) {
			System.out.println(data[i]);
		}

	}

}
```
>배열 data에는 세 번째 요소까지만 유효한 값이 저장되어있지만 length속성으로 인해 모든 배열 요소의 값들을 출력하고 있다. 유효한 값이 저장된 배열 요소만 출력하려면 아래 코드와 같이 수정한다.
>>**출력**</br>
10.0</br>
20.0</br>
30.0</br>
0.0</br>
0.0

```java
public class Array {

	public static void main(String[] args) {
		double[ ] data =  new double[5];
		int size = 0;
		
		data[0] = 10.0; size++;
		data[1] = 20.0; size++;
		data[2] = 30.0; size++;
		
		for(int i = 0; i < size; i++) {
			System.out.println(data[i]);
		}

	}

}
```
>**출력**</br>
10.0</br>
20.0</br>
30.0


## 객체 배열 
Book이라는 클래스가 존재할때 Book 클래스를 사용한 객체 배열을 생성해보자. 
```java
Book[ ] library = new Book[5];
```
코드의 내용만 보면 Book 인스턴스 5개가 생성된 것처럼 보인다. 하지만 이 코드는 Book 인스턴스 주소 값을 담을 공간 5개를 생성하는 의미를 가진다. 즉 이 코드를 실행하면 아래 그림과 같이 Book 주소 값을 담을 공간이 5개 만들어지고 자동으로 각 공간은 '비어있다'는 의미의 null 값으로 초기화된다.

![스크린샷(909)](https://user-images.githubusercontent.com/101917562/179920320-22827011-659f-4f33-a6ec-c6162eedfc48.png)

이제 각 배열 요소에 인스턴스를 생성해 넣어 보겠다. Book 클래스에 구현한 생성자를 사용했다.
```java
    Book[ ] library = new Book[5];
    library[0] = new Book("태백산맥", "조정래");
    library[1] = new Book("데미안", "헤르만 헤세");
    library[2] = new Book("어떻게 살 것인가", "유시민");
    library[3] = new Book("토지", "박경리");
    library[4] = new Book("어린왕자", "생텍쥐페리");
 ``` 
    
 ![스크린샷(911)](https://user-images.githubusercontent.com/101917562/179920873-0ad73733-f775-4c81-bd7d-cdd2700ad89e.png)


각 배열 요소에는 각각 요소가 가리키는 인스턴스의 주소를 가지고 있다.

## 배열 복사하기

배열을 복사할때 자바에서는 **System.arraycopy(src, srcPos, dest, destPos, length)** 메서드를 지원한다.

| 매개변수 | 설명 |
|:----------: |:----------|
| src | 복사할 배열 이름 |
| srcPos | 복사할 배열의 첫 번째 위치 | 
| dest | 복사해서 붙여 넣을 대상 배열 이름 | 
| destPos | 복사해서 대상 배열에 붙여 넣기를 시작할 첫 번째 위치 |
| length | src에서 dest로 자료를 복사할 요소 개수 |

```java
public class ArrayCopy {

	public static void main(String[] args) {

		int[] array1 = {10 ,20, 30, 40, 50};
		int[] array2 = {1, 2, 3, 4, 5};
		
		System.arraycopy(array1, 0, array2, 1, 4);
				
		for(int i=0; i<array2.length; i++){
			System.out.println(array2[i]);
		}
	}
}
```
>array1 배열의 요소 0번부터 4개를 복사해서 대상 배열 array2의 요소 1번부터 붙여 넣는다.
>>**출력**</br>
1</br>
10</br>
20</br>
30</br>
40

## 얕은 복사와 깊은 복사
### 얕은 복사
책 이름과 저자의 이름을 멤버 변수로 갖고 있는 Book 클래스가 있다고 가정하였다.

```java
public class ObjectCopy2 {

	public static void main(String[] args) {
		Book[] bookArray1 = new Book[3];
		Book[] bookArray2 = new Book[3];
		
		bookArray1[0] = new Book("태백산맥", "조정래");
		bookArray1[1] = new Book("데미안", "헤르만 헤세");
		bookArray1[2] = new Book("어떻게 살 것인가", "유시민");
 		System.arraycopy(bookArray1, 0, bookArray2, 0, 3);
        
		
		for(int i=0; i<bookArray2.length; i++){
			bookArray2[i].showBookInfo();
		}
		
		bookArray1[0].setBookName("나목"); //bookArray1 배열의 첫 번째 요소 값 변경
		bookArray1[0].setAuthor("박완서"); //bookArray1 배열의 첫 번째 요소 값 변경
		
		System.out.println("=== bookArray1 ===");
		for(int i=0; i<bookArray1.length; i++){
			bookArray1[i].showBookInfo();
		}
		
		System.out.println("=== bookArray2 ===");
		for(int i=0; i<bookArray2.length; i++){
			bookArray2[i].showBookInfo();
		}
	}
}
```
>**출력**</br>
태백산맥,조정래</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민</br>
=== bookArray1 ===</br>
**나목,박완서**</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민</br>
=== bookArray2 ===</br>
**나목,박완서**</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민

분명 bookArray1 배열의 첫 번째 요소 값을 변경했는데 bookArray2 배열 요소 값도 변경되어 출력됐다. 그 이유는 객체 배열의 요소에 저장된 값은 인스턴스 자체가 아니고 인스턴스의 주소 값이기 때문이다. 따라서 두 배열의 서로 다른 요소가 같은 인스턴스를 가리키고 있으므로 복사되는 배열의 인스턴스 값이 변경되면 두 배열 모두 영향을 받는다. 

<div style="text-align: left"> <img src =   
"https://velog.velcdn.com/images/strangehoon/post/032099eb-9052-49b2-aa2c-a7cc0da618b1/image.png" height = "250px" width = "300px"> </div>
</br>
이와 같이 복사를 주소 값만 복사한다고 해서 **얕은 복사( copy)** 라고 한다.

### 깊은 복사
인스턴스를 따로 관리하고 싶다면 직접 인스턴스를 만들고 그 값을 복사해야 한다. 이를 **깊은 복사(deep copy)** 라고 한다.
```java
public class ObjectCopy3 {

	public static void main(String[] args) {
		Book[] bookArray1 = new Book[3];
		Book[] bookArray2 = new Book[3];
		
		bookArray1[0] = new Book("태백산맥", "조정래");
		bookArray1[1] = new Book("데미안", "헤르만 헤세");
		bookArray1[2] = new Book("어떻게 살 것인가", "유시민");
 		
		bookArray2[0] = new Book(); //객체 직접 생성
		bookArray2[1] = new Book(); //객체 직접 생성
		bookArray2[2] = new Book(); //객체 직접 생성
		
		for(int i=0; i<bookArray1.length; i++){   // 각각의 요소를 복사
			bookArray2[i].setBookName(bookArray1[i].getBookName());
			bookArray2[i].setAuthor(bookArray1[i].getAuthor());
		}
		
		for(int i=0; i<bookArray2.length; i++){  //복사된 내용 확인
			bookArray2[i].showBookInfo();
		}
		
		bookArray1[0].setBookName("나목");   //bookArray1 의 내용 수정
		bookArray1[0].setAuthor("박완서");
		
		System.out.println("=== bookArray1 ===");    //bookArray1 출력
		for(int i=0; i<bookArray1.length; i++){
			bookArray1[i].showBookInfo();
		}
		
		System.out.println("=== bookArray2 ===");    //bookArray2 출력
		for(int i=0; i<bookArray2.length; i++){
			bookArray2[i].showBookInfo();   // bookArray1 과 다른 내용으로 출력됨
		}
	}
}
```
>**출력**</br>
태백산맥,조정래</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민</br>
=== bookArray1 ===</br>
**나목,박완서**</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민</br>
=== bookArray2 ===</br>
**태백산맥,조정래**</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민

![스크린샷(914)](https://user-images.githubusercontent.com/101917562/179921413-9cec8ae4-4c00-4f70-825a-8efe5511396a.png)

복사할 배열 요소는 기존 배열 요소와 서로 다른 인스턴스를 가리키므로 기존 배열의 요소 값이 변경되어도 영향을 받지 않는다는 것을 알 수 있다.

## 향상된 for문과 배열
자바 5부터 제공되는 **향상된 for문(enhanced for loop)** 은 배열의 처음에서 끝까지 모든 요소를 참조할 때 사용하면 편리한 반복문이다. 향상된 for문은 배열 요소 값을 순서대로 하나씩 가져와 변수에 대입한다. 형식은 아래와 같다. 
```java
for(변수 : 배열) {
	반복 실행문;
}
```
다음은 향상된 for문을 사용해 int형 배열 numArray의 요소 값을 순서대로 하나씩 가져와서 int형 변수 num에 대입하는 코드다.
```java
int[ ] numArray = new int[ ] {1, 2, 3, 4, 5, 6, 7, 8, 9 ,10};
for(int num : numArray) {...}
```
## 2차원 배열
다음은 2행 4열의 이차원 배열을 선언하는 코드다
```java
int[ ][ ]arr = new int[2][4];
```
arr.length는 행의 개수를, 각 행의 길이 arr[i].length는 열의 개수를 나타낸다.

# ArrayList
배열은 프로그램에서 사용하려면 항상 배열 길이를 먼저 정해야 하고 한번 정해진 배열의 크기는 변경할 수 없다. 이러한 배열의 불편함 들을 줄이기 위해 자바에서는 ArrayList를 제공한다. 참고로 ArrayList는 java.util 패키지에 구현되어 있는 클래스이다.(각종 자료 구조와 알고리즘에 관련된 클래스가 이 패키지에 존재한다.)  따라서 ArrayList를 사용하려면 자바 클래스를 선언하기 전에 **import java.util.ArrayList;** 문장을 삽입해야 한다.
## ArrayList 클래스의 주요 매서드
| 메서드 | 설명 |
|:----------: |:----------:|
| boolean add(E e) | 요소 하나를 배열에 추가한다. E는 요소의 자료형을 의미한다. |
| int size() | 배열에 추가된 요소 전체 개수를 반환한다. | 
| E get(int index) | 배열의 index 위치에 있는 요소 값을 반환한다. | 
| E remove(int index) | 배열의 index 위치에 있는 요소 값을 제거하고 그 값을 반환한다. |
| boolean isEmpty() | 배열이 비어 있는지 확인한다. |

## ArrayList 클래스 활용하기
ArrayList의 기본 형식은 다음과 같다.
```java
ArrayList<E> 배열 이름 = new ArrayList<E>(); // <E>와 같은 형태를 제네릭 자료형이라고 한다.
``` 
다음은 ArrayList 클래스를 활용한 예제이다.
```java
package array;

import java.util.ArrayList;	//ArrayList 클래스 import

public class ArrayListTest {

	public static void main(String[] args) {

		ArrayList<Book> library = new ArrayList<Book>();	//arrayList 선언

		
		library.add( new Book("태백산맥", "조정래") );	//add() 메서드로 요소 값 추가
		library.add( new Book("데미안", "헤르만 헤세") );
		library.add( new Book("어떻게 살 것인가", "유시민") );
		
		for(int i=0; i<library.size(); i++){	//배열에 추가된 요소 개수만큼 출력
	
			Book book = library.get(i);
			book.showBookInfo();
		}
		
		System.out.println();
		System.out.println("=== 향상된 for문 사용 ===");
		for(Book book : library){
			book.showBookInfo();
		}
	}
}
```
>**출력**</br>
>태백산맥,조정래</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민<br/>
=== 향상된 for문 사용 ===</br>
태백산맥,조정래</br>
데미안,헤르만 헤세</br>
어떻게 살 것인가,유시민
