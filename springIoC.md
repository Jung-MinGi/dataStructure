<h2>스프링의IoC 전략</h2>

스프링 애플리케이션에서는 오브젝트의 생성관 관계설정,사용,제거 등의 작업을 애플리케이션 코드 대신 독립된 컨테이너가 담당한다.<br>
컨테이너가 코드 대신 오브젝트에 대한 제어권을 갖고 있다고해서 **IoC**라고 부른다.<br>
스프링에선 IoC를 담당하는 컨테이너를 (=빈 팩토리 or ApplicationContext)라고 부르기도 한다.<br>

* 빈 팩토리(bean factory) vs ApplicationContext
```
컨테이너를 오브젝트를 다루는 기능만으로 보면 빈팩토리에 가깝고
더 넓게 보면 ApplicationContext라고 보면 된다.
```

스프링 애플리케이션을 만들기 위해선 **POJO클래스**와 **설정 메타 정보**를 필요로 한다<br>
POJO클래스는 일반적인 애플리케이션 코드를 의미하고<br>
설정 메타정보는 POJO클래스들을 어떤식으로 애플리케이션에 사용할지 적어논 정보인데<br>
이를 토대로 컨테이너가 빈을 제어한다.

* 설정 메타정보<br>
IoC컨테이너가 오브젝트를 제어할 수 있도록 적절한 메타정보를 제공해주어야 한다.<br>
IoC컨테이너가 필요한 설정 메타정보는 빈을 어떻게 만들고 어떻게 동작하게 할 것인가에 관한 정보를 내가 제공해주어야 한다.<br>

```
어떤 빈 정보가 있음 --> 빈 정보를 읽어 BeanDefinition정보로 변환해주는 기능을 가진 오브젝트는 BeanDefinitionReader라고 부른다
외부리소스(어떤 빈 정보)에 따라 해당되는 여러 리더기가 존재함
```

* IoC컨테이너 종류와 사용법<br>
  * GenericApplicationContext
    XML파일과 같은 외부의 리소스에 있는 빈 설정 메타정보를 리더를 통해 읽어들여서 메타정보로 전환해서 사용한다.<br>
    XML포맷에 사용되는 리더기는 XmlBeanDefinitionReader이다.<br>
    이 리더기를 통해 xml로 작성된 빈 정보를 읽어 이를 BeanDefinition정보로 변환해주는 것이다.

🧐@Configuration

스프링이 빈 팩토리(or applicationContext)를 위한 오브젝트 설정을 담당하는 클래스라고 인식할 수 있다
🧐의존관계 주입(DI)

런타임시점에 애플리케이션 코드 외부에서 제 3자(스프링)가 오브젝트간의 관계를 설정해주는 모습을 보고 의존관계 주입이라고 부른다

🧐 스프링 IoC전략(오브젝트의 설계와 생성,관계, 사용에 관한 전략)

개발시에는 인터페이스를 이용하여 클래스간의 관계를 느슨하게 유지하다가  런타임 시 클래스의 오브젝트간의 관계를 정의한다

 ![image](https://github.com/Jung-MinGi/SpringStudy/assets/118701129/b4d259d0-c64a-48b0-883d-346dfd8b5834)


만약 ConnectionMakerImpl1 구현체에서 ConnectionMakerImpl2 구현체로 변경하고 싶으면 애플리케이션 쪽 코드는 건드리지 않고 간단한게 설정정보에서 구현체만 수정해주면 된다

그래서 IoC의 대표적인 기능이 의존관계 주입이라서 DI컨테이너라고도 부른다.