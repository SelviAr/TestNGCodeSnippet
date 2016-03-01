# TestNGCodeSnippet




### Hierarchy of TestNG Annotations


+ BeforeSuite
    + BeforeTest
        + BeforeClass
            + BeforeMethod
                + Test 
    	    + AfterMethod
    	+ AfterClass
    + AfterTest
+ AfterSuite


``` java

public class TestNGHierarchy {

	@BeforeSuite
	public void beforeSuite() {
		System.out.println("This method will execute before the Test Suite");
	}

	@AfterSuite
	public void afterSuite() {
		System.out.println("This method will execute after the Test Suite");
	}
	
	@BeforeTest
 	public void beforeTest() {
		System.out.println("This method will execute before the Test");
	}
 
	@AfterTest
	public void afterTest() {
			System.out.println("This method will execute after the Test");
	}
 
	@BeforeClass
	public void beforeClass() {
		System.out.println("This method will execute before the Test Class");
	}

	@AfterClass
	public void afterClass() {
		System.out.println("This method will execute after the Test Class");
	}
	
	@BeforeGroups("Regression")
	public void beforeGroups() {
		System.out.println("This method will execute before the Test group");
	}

	@AfterGroups("Regression")
	public void afterGroups() {
		System.out.println("This method will execute after the Test group");
	}

	@BeforeMethod
	public void beforeMethod() {
		System.out.println("This method will execute before the Test case method");
	}

	@AfterMethod
	public void afterMethod() {
		System.out.println("This method will execute after the Test case method");
	}
	
	@Test()
	public void sss() {
		System.out.println("@Test");
	}
}

```

### TestNG Listeners
``` java

```

### TestNG Listeners
``` java

```

Asserts
``` java

```

