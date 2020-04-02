# mock-LocalDate-now-java
How to mock the static LocalDate.now() call in java.

## Example code

```
@RunWith(PowerMockRunner.class)
@PrepareForTest({LocalDate.class,PublicationValidator.class})
public class PublicationValidatorTest {

    private Validator validator;

    @Before
    public void setUp(){
        LocalDate date = LocalDate.of(2000, 1, 1);
        PowerMockito.stub(PowerMockito.method(LocalDate.class,"now")).toReturn(date);
        validator = new Validator();
    }

    @Test
    public void exampleTest() {
        result = validator.callWithCallToLocalDate()
        assertThat(result).isTrue();
    }
}
```

## Explaination
```@RunWith(PowerMockRunner.class)``` Will enable powermock for this test class

```@PrepareForTest({LocalDate.class,Validator.class})``` Include both the class to mock and the class using the mock

```LocalDate date = LocalDate.of(2000, 1, 1);``` Decide which date should be used for the tests

```PowerMockito.stub(PowerMockito.method(LocalDate.class,"now")).toReturn(date);``` This line will mock specifically the call to LocalDate.now() (other methods remain unaffected)

It is also possible to mock all calls by using ```PowerMockito.mockStatic(LocalDate.class)``` with a when().thenReturn() statement after. 


## Extra information
Remember to add PowerMock and the powermock mockito api to your classpath.
Maven file:
```
<dependency>
    <groupId>org.powermock</groupId>
    <artifactId>powermock-module-junit4</artifactId>
    <version>2.0.4</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.powermock</groupId>
    <artifactId>powermock-api-mockito2</artifactId>
    <version>2.0.4</version>
    <scope>test</scope>
</dependency>
```
