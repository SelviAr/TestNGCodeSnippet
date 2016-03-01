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

### TestNG Methods
``` java

public class TestMethods {

	@Test(priority = 1 )
	public void Login() {
		System.out.println("@Test");
	}
	
	@Test(enabled = true)
	public void test2() {
		Assert.assertEquals(true, true);
	}

	@Test(enabled = false)
	public void test3() {
		Assert.assertEquals(true, true);
	}
	
	@Test(alwaysRun = true, description = “test method”)
	public void sss() {
		System.out.println("@Test");
	}
	
	@DataProvider
	public Object[][] UserDataProvider() {
		return new Object[][]{
			{ 'Selvi Arm', 'selvia', 'selvi@xyz.com' },
			{ 'Vik Pal', 'vikp', 'coolvik@xyz.com' },
			{ 'Aksha Pal', 'aksha', 'aksha@xyz.com' }
		};
	}
	
	// This test will run 3 times
	@Test(dataProvider = "UserDataProvider")
	public void CharToASCIITest(String FullName, String UserID, String EmailID) {
		   Assert.assertEquals(EmailID, 'aksha@xyz.com');
	}
	
	@Test (groups = { "UI", "Regression" })
	@Parameters({ "DBConfigString", "Browser" })
	public void createConnection(String DBConfigString, String Browser) {
	
	}
	
	@Test(dependsOnGroups = {"database","selenium-test"})
	public void runFinal() {
		System.out.println("runFinal");
	}

	@Test(dependsOmethods = "login")
	public void runFinal() {
		System.out.println("runFinal");
	}
	
	
	@Test(invocationCount = 7) 
	public void sss() {
		System.out.println("@Test");
	}
	
	@Test(invocationCount = 7, invocationTimeOut = 30 )
	public void sss() {
		System.out.println("@Test");
	}
	
	/*
	   * Example : Multiple expected exceptions
	   * Test is success if either of the exception is thrown
	   */
	@Test(expectedExceptions = ArithmeticException.class)
	public void divisionWithException() {
		int i = 1 / 0;
	}
	
	@Test(timeOut = 1000)
	public void testThisShouldFail() {
		while (true);
	}

}

```

### TestNG Listeners
``` java

```

Asserts
``` java

```

