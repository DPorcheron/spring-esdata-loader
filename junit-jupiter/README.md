# spring-esdata-loader-junit-jupiter

**JUnit Jupiter** implementation of the library.

The sub-module is all that is needed to start using the library with the brand new **JUnit Jupiter**. 
It defines an `Extension` named `LoadEsDataExtention` that can be used to insert data into Elasticsearch,
before all tests are run (class level), or just before a specific test is run (method level).

Here is an example:

```java
import com.github.spring.esdata.loader.core.LoadEsData;
import com.github.spring.esdata.loader.junit.jupiter.LoadEsDataConfig;
import org.junit.jupiter.api.Test;

//@SpringBootTest or any @ContextConfiguration(..) to initialize the Spring context that contains the ElasticsearchTemplate

@LoadEsDataConfig({ // @LoadEsDataConfig is a meta annotation that is itself annotated with @ExtendWith(LoadEsDataExtension.class)
    @LoadEsData(esEntityClass=MyEsEntity1.class, location="/path/to/data1.json"),
    @LoadEsData(esEntityClass=MyEsEntity2.class, location="/path/to/data2.json")
})
public class MyJunitJupiterTestClass{

    public void testThatUsesEsDataLoadedAtClassLevel()
    {
        // make your assertions here
    }

    @LoadEsData(esEntityClass=MyEsEntity3.class, location="/path/to/data3.json")
    public void testThatUsesEsDataLoadedAtClassLevelAndAtThisMethodLevel()
    {
        // make your assertions here
    }
}
```

A full example can be seen in demo project:
*  [LoadEsDataExtensionTest.java](/demo/src/test/java/com/github/spring/esdata/loader/demo/junit/jupiter/LoadEsDataExtensionTest.java)
