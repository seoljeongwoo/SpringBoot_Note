# SpringBoot_Note
// 최종수정 : 2021-02-21 //
스프링 vs 스프링부트 : 재료 vs 완성품
스프링부트 : Java의 생산성 향상
COC : 설정보다는 관습 (남들과 동일하게 작성시 작성필요x)

02/19
Hello world Controller 만들기
Boot Run을 통하여 서버 실행
SpringBoot 테스트 만들기
MockMvc 테스트 만들기

@RestController 안에 @ResponseBody 와 @Controller 가 들어있음
모의 Http response와 request를 이용한 Test = MockMvc Test



02/20
JPA 의존성 추가 -> DB쿼리대신 자바를 통해 처리할수있도록 맵핑해준 라이브러리
H2 DB 의존성 추가
Entity 생성 및 테스트

JPA에 문법에 맞게 작성시 DB에 상관없이 적당한 쿼리를 생성하여 ORM이 처리하도록 되어있음
@Id = Id임을 명시
@Generatedvalue = 자동으로 생성할 변수
Repository (interface)=> DB에 값을 저장 및 불러옴 , JpaRepository<Entity,key>로 상속받음

Lombok - @Getter , @Setter , @ToString

@Getter , @Setter 를 field 에 사용시 해당 field의 getter ,setter method 생성
class 상단에 사용시 모든 field 의 getter , setter method 생성

@ToString = Field 값이 추가가 될때마다 @Overide 시 변경해야함 , 
class 상단에 사용시 자동적으로 변경 
class 상단에 @ToString 의인자로 exclude = 해당 필드값 적을시 해당필드값은 제외시키고 ToString Method 생성 
(필드값의 오타가 발생할수 있음)
Field 에 exclude 할경우 @ToString.exclude 지정


Lombok - @Constructor
Lombok - @EqualsAndHashCode
Lombok - @Data

@NoArgsConstructor = > Default Constructor
-> 필드가 final로 설정되어 있는 경우 필드 초기화를 할수 없기때문에 생성자를 만들수없고 에러발생 문제점
-> force=true라는 옵션을 이용해 final 필드 강제 초기화를 시켜 생성자를 만들수있음
-> @NonNull과 같이 필드에 제약조건이 설정되어있는 경우, 추후 초기화를 진행하기전까지 생성자내 null-check 로직이 생성되지 않음

Nullness annotation = @NonNull : null을 허용하지 않는경우, @Nullable : null을 허용할경우

@AllArgsConstructor = > 모든 Field 에 대한 Constructor
@RequiredArgsConstructor => @NonNull이나 final인 Field만으로 이루어진 Constructor 생성
-> 두 개의 같은 타입 인스턴스 변수를 선언 후 선언된 변수의 순서를 바꾸게 되면
lombok이 파라미터 순서를 필드 선언 순서로 변경하게 되고 입력이 변경된 상태로 들어가게 되는 문제점.

HashCode = 같은 객체 , Equals = 같은 값
객체값이 같을경우 동일하다고 판단해주어야하고
HashCode 는 객체 생성시 마다 다른 HashCode를 가지게 되므로
DB에서 동일한 Key를 사용하기 위해서 
HashCode 와 Equals 를 Overide 해줄필요있음.
=> 직접구현시 실수 발생가능 => @EqualsAndHashCode 사용
-> 객체를 Set에 저장후 필드 값을 변경시 hashCode가 변경되어 이전에 저장한 객체를 찾을수 없는 문제점.

@Data = > @Getter, @Setter, @RequiredArgsConstructor, @ToString, @EqualsandHashCode 제공
Lombok 을 통한 가독성 높은 코드작성가능
-> RequiredArgsConstructor , EqualsandHashCode가 가지는 문제점을 포함함

@Builder
-> 파라미터 순서가 아닌 이름으로 값을 설정, 리팩토링에 유연하게 대응 및 필드순서가 변경되어도 상관 없음.
-> 객체 생성이 명확해짐
