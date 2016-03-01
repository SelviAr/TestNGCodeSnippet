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
	
	@DataProvider
	 public Object[][] UserCredentials(){
	  Object[][] Credentials = new Object[3][2];
	  
	  Credentials[0][0] = "UserID1";
	  Credentials[0][1] = "Password1";
	  
	  Credentials[1][0] = "UserID2";
	  Credentials[1][1] = "Password2";
	  
	  Credentials[2][0] = "UserID3";
	  Credentials[2][1] = "Password3";

	  return Credentials;
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
	
	@Test 
	@Parameters({ "OptionalValue"  })
	public void Test1(@Optional("OptionalValue" ) DBConfigString, String value) {
	
	}
	
	@Test(dataProvider = "data-provider", dataProviderClass=DataProviderClass.class)
	public void testMethod(String data) {
			System.out.println("Data is: " + data);
	}
}

public class DataProviderClass {
	@DataProvider(name="data-provider")
	public static Object[][] dataProviderMethod(){
		return new Object[][] { { "data one" }, { "data two" } };
	}
}


```

### TestNG DataProvider
``` java

/*
DataProviderTest Class
*/

public class DataProviderTest {
	//------------------
	//value injecting using TestNG XML Parameter 
	//<parameter name="username" value="selvi2"></parameter>
	//<parameter name="password" value="password123"></parameter>
	@Parameters({"username", "password"})
	@Test	
	public void LoginUsingXMLParameter(String username, String password) {
		System.out.println("Data taken from the xml file is " + username + " " + password);
	}
	
	//------------------
	//DataProvider
	@DataProvider
	public Object[][] getUserCredentialData() {
		return new Object[][]{
			{"selvi2", "password123"}, 
			{"selvi2", "password123"}
		};
	}
	
	@Test(dataProvider="getUserCredentialData")
	public void instanceDbProvider(String username, String password) {
		System.out.println("Data taken from class Instance  is " + username + " " + password);
	}	
	
	//------------------
	//Static DataProvider
	@Test(dataProvider="productionKey", dataProviderClass=DataProviderSource.class)
	public void client1Test(Integer p) {
		System.out.println("Client1 testing: Data(" + p + ")");
	}  

	@Test(dataProvider="QAKey", dataProviderClass=DataProviderSource.class)
	public void client2Test(Integer p) {
		System.out.println("Client2 testing: Data(" + p + ")");
	} 
	
	//------------------
	//Data based on the Method name
	@Test(dataProvider="DataBasedOnMethodName", dataProviderClass=DataProviderSource.class)
	public void TestCase01(String data) {
		System.out.println("Scenario testing: Data(" + data + ")");
	}

	@Test(dataProvider="DataBasedOnMethodName", dataProviderClass=DataProviderSource.class)
	public void TestCase02(String data) {
		System.out.println("Scenario testing: Data(" + data + ")");
	}

	@Test(dataProvider="DataBasedOnMethodName", dataProviderClass=DataProviderSource.class)
	public void commonScenarios(String data) {
		System.out.println("Common Scenarios testing: Data(" + data + ")");
	}

	//------------------
	//Data based on the test name given in the testng.xml
	//<test name="Unit"> or <test name="Acceptance"> or <test name="Integration">

	@Test(dataProvider="TestType", dataProviderClass=DataProviderSource.class)
	public void acceptanceTest(String data) {
		System.out.println("Acceptance testing: Data(" + data + ")");
	}

	@Test(dataProvider="TestType", dataProviderClass=DataProviderSource.class)
	public void integrationTest(String data) {
		System.out.println("Integration testing: Data(" + data + ")");
	}	

	//------------------
	//Get the strongly typed data
	@Test(dataProvider="userData")
	public void empTest(UserData user) {
		System.out.println("Username : (" + user.username + ")");
		System.out.println("Password : (" + user.password + ")");
	}	
	
	@DataProvider(name="userData") 
	public Object[][] getUserData() {
		return new Object[][]{{new UserData("Selvi2", "password123")}, {new UserData("Selvi1", "password123")}};
	}
	
	@DataProvider
     public Object[][] UserCredentials(){
      Object[][] Credentials = new Object[3][2];

      Credentials[0][0] = "UserID1";
      Credentials[0][1] = "Password1";

      Credentials[1][0] = "UserID2";
      Credentials[1][1] = "Password2";

      Credentials[2][0] = "UserID3";
      Credentials[2][1] = "Password3";

      return Credentials;
     }
	
}

/*
DataProviderSource Class
*/
public class DataProviderSource {

	@DataProvider(name="productionKey")
	public static Object[][] getClient1Data() {
		return new Object[][]{{17755}};		
	}
	
	@DataProvider(name="QAKey")
	public static Object[][] getClient2Data() {
		return new Object[][]{{334442}};		
	}
	
	@DataProvider(name="DataBasedOnMethodName")
	public static Object[][] getScenarioData(Method method) {		
		String testCase = method.getName();
		if ("TestCase01".equals(testCase)) {
			return new Object[][]{{"data key 17755"}};
		} else if ("TestCase02".equals(testCase)) {
			return new Object[][]{{"data key 334442"}};
		} else {
			return new Object[][]{{"Common scenario data"}};
		}
	}	
	
	@DataProvider(name="TestType")
	public static Object[][] getTestTypeData(ITestContext context) {		
		String testName = context.getName();
		if ("Integration".equals(testName)) {
			return new Object[][]{{"Integration test data"}};
		} else if ("Acceptance".equals(testName)) {
			return new Object[][]{{"Acceptance test data"}};
		} else {
			return new Object[][]{{"Common test data"}};
		}
	}	
}

/*
UserData Class
*/

public class UserData {
	private String username;
	private String password;

	public Employee(String username, password) {
		this.username = username;
		this.password = password;
	}
}

```


### TestNG Listeners

``` xml
<listeners>
        <listener class-name="com.mytestng.MyTestNGListener" />
</listeners>
```

``` java
public class MyTestNGListener implements IExecutionListener, IAnnotationTransformer
		,ISuiteListener, ITestListener, IMethodInterceptor, IInvokedMethodListener, IHookable, IReporter    {
	private long startTime;

	//IExecutionListener
	@Override
	public void onExecutionStart() {
		startTime = System.currentTimeMillis();
		System.out.println("TestNG is going to start");	
		System.out.println("Notify by mail that TestNG is going to start");			
	}

	@Override
	public void onExecutionFinish() {
		System.out.println("Notify by mail, TestNG is finished");
		System.out.println("TestNG has finished, took around " + (System.currentTimeMillis() - startTime) + "ms");
	}
	
	//IAnnotationTransformer
	
	@Override
	public void transform(ITestAnnotation annotation, Class testClass, Constructor testConstructor, Method testMethod) {		
		if (testMethod.getName().equals("t1")) {
			System.out.println("set data provider for " + testMethod.getName()); 
			annotation.setDataProviderClass(DataProviderFactory.class);
			annotation.setDataProvider("getDp1");
		} else if (testMethod.getName().equals("t2")) {
			System.out.println("set data provider for " + testMethod.getName()); 
			annotation.setDataProviderClass(DataProviderFactory.class);
			annotation.setDataProvider("getDp2");
		} else if (testMethod.getName().equals("t3")) {
			System.out.println("Disable " + testMethod.getName()); 
			annotation.setEnabled(false);
		}
	}
	
	//ISuiteListener
	
	@Override
	public void onStart(ISuite suite) {
		System.out.println("Start suite " + suite.getName());
		XmlSuite xmlSuite = suite.getXmlSuite();
		if (!xmlSuite.getTests().isEmpty()) {
			Map parms = new HashMap();
			parms.put("ui", "web");
			System.out.println("Set ui param value");
			xmlSuite.setParameters(parms);
		}		
	}

	@Override
	public void onFinish(ISuite suite) {
		System.out.println("Finish suite " + suite.getName());
	}
	
	//ITestListener
	@Override
	public void onTestStart(ITestResult result) {
		System.out.println("on test method " +  getTestMethodName(result) + " start");
	}

	@Override
	public void onTestSuccess(ITestResult result) {
		System.out.println("on test method " + getTestMethodName(result) + " success");
	}

	@Override
	public void onTestFailure(ITestResult result) {
		System.out.println("on test method " + getTestMethodName(result) + " failure");
	}

	@Override
	public void onTestSkipped(ITestResult result) {
		System.out.println("test method " + getTestMethodName(result) + " skipped");
	}

	@Override
	public void onTestFailedButWithinSuccessPercentage(ITestResult result) {
		System.out.println("test failed but within success % " + getTestMethodName(result));
	}

	@Override
	public void onStart(ITestContext context) {
		System.out.println("on start of test " + context.getName());
	}

	@Override
	public void onFinish(ITestContext context) {
		System.out.println("on finish of test " + context.getName());
	}
	
	private static String getTestMethodName(ITestResult result) {
		return result.getMethod().getConstructorOrMethod().getName();
	}
	
	//IMethodInterceptor
	
	@Override
	public List intercept(List methods,
			ITestContext context) {
		List result = new ArrayList();
		for (IMethodInstance m : methods) {
			Test test = m.getMethod().getMethod().getAnnotation(Test.class);
			Set groups = new HashSet();
			for (String group : test.groups()) {
				groups.add(group);
			}
			if (groups.contains("perf")) {
				result.add(m);
			} else {
				String testMethod = m.getMethod().getMethod().getName();
				System.out.println(testMethod
						+ " not a performance test so remove it");
			}
		}
		return result;
	}
	
	//IInvokedMethodListener 
	@Override
    public void beforeInvocation(IInvokedMethod method, ITestResult testResult) {
        System.out.println("before invocation of " + method.getTestMethod().getMethodName());
    }

    @Override
    public void afterInvocation(IInvokedMethod method, ITestResult testResult) {
        System.out.println("after invocation " + method.getTestMethod().getMethodName());
    }
	
	//IHookable 
	@Override
	public void run(IHookCallBack callBack, ITestResult testResult) {
		Object[] parms = callBack.getParameters();
		if (parms[0].equals("perftest")) {
			System.out.println("Skip for method because it not perftest");			
		} else {
			callBack.runTestMethod(testResult);
		}
	}
	
	//IReporter 
	@Override
	public void generateReport(List xmlSuites, List suites, String outputDirectory) {
		System.out.println("*** Login Screen Report ***");
		
		ISuite suite = suites.get(0);
		Map<String, Collection> methodsByGroup = suite.getMethodsByGroups();
		Map<String, ISuiteResult> tests = suite.getResults();
		for (String key : tests.keySet()) {
			System.out.println("Key: " + key + ", Value: " + tests.get(key));
		}
		
		Collection suiteResults = tests.values();
		ISuiteResult suiteResult = suiteResults.iterator().next();
		ITestContext testContext = suiteResult.getTestContext();
		Collection perfMethods = methodsByGroup.get("perf");
		IResultMap failedTests = testContext.getFailedTests();
		for (ITestNGMethod perfMethod : perfMethods) {
			Set testResultSet = failedTests.getResults(perfMethod);
			for (ITestResult testResult : testResultSet) {
				System.out.println("Test " + testResult.getName() + " failed, error " + testResult.getThrowable());
			}
		}
		
		IResultMap passedTests = testContext.getPassedTests();
		for (ITestNGMethod perfMethod : perfMethods) {
			Set testResultSet = passedTests.getResults(perfMethod);
			for (ITestResult testResult : testResultSet) {
				System.out.println("Test " + testResult.getName() + " passed, time took " + 
			(testResult.getStartMillis() - testResult.getEndMillis()));
			}
		}
		System.out.println("*** End of Login Screen Report ***");
	}
	
}



public class MyTestNGListenerTestExample {
	
	//Test Method for IAnnotationTransformer test
	@Test
	public void t1(String param) {
		System.out.println("Method is t1, parameter is " + param);
	}
	
	//Test Method for IAnnotationTransformer test
	@Test
	public void t2(String param) {
		System.out.println("Method is t2, parameter is " + param);
	}
	
	//Test Method for IAnnotationTransformer test
	@Test
	public void t3() {
		System.out.println("Method is t3");
	}		
	
	//Test Method for ISuiteListener test
	@Parameters("ui")
	@BeforeSuite
	public void beforeSuite(String parm) {
		System.out.println("before suite, ui value: " + parm);
	}
	
	@Test
	public void t() {
		System.out.println("test method");
	}
	
	@AfterSuite
	public void afterSuite() {
		System.out.println("after suite");
	}
	
	
	//IMethodInterceptor
	@Test(groups="perf")
	public void t1() {
		System.out.println("test method: t1");
	}
	
	@Test
	public void t2() {
		System.out.println("test method: t2");
	}
	
}

```

### Asserts
``` java

Assert.assertEquals
Assert.assertNotEquals
Assert.assertTrue
Assert.assertFalse
Assert.assertNull
Assert.assertNotNull
Assert.assertSame
Assert.assertNotSame
Assert.fail
Assert.assertThrows
Assert.assertEqualsNoOrder

Assert.assertEquals(Actualtext, "Selvi");
Assert.assertNotEquals(Actualtext, "Selvi", "Expected and actual is same");

Assert.assertTrue(chk1.isSelected());
Assert.assertFalse(chk2.isSelected());

Assert.assertNull(txt1.getAttribute("disabled"));  
Assert.assertNotNull(txt1.getAttribute("disabled")); 
 
 
 
  BigDecimal b1 = new BigDecimal("1.0");
  BigDecimal b2 = new BigDecimal("1.0");
  BigDecimal b3 = b1;
 
  int i1 = 10;
  int i2 = 10;
 
  @Test
  public void BigDecimaltest() throws Exception {
    // if(b1 == b2)
    assertSame(b1, b2);    // THIS TEST WILL FAIL
 
    // b1.equals(b2)
    assertEquals(b1, b2);  // should pass
 
    // (b1 == b3)
    assertSame(b1, b3);    // will pass
 
    //(b1.equals(b3))
    assertEquals(b1, b3);  // will pass
  }
 
  @Test
  public void intTest() throws Exception {
    // if(i1 == i2)
    assertSame(i1, i2);    // will pass
 
    // if(i1 == i2)
    assertEquals(i1, i2);  // will pass
  }



```

### testng.xml
``` xml

<suite name="Suite One" parallel="classes" thread-count="2" time-out="3000">
	<listeners>
		<listener class-name="mylogger.CustomerLogging"/>
		<listener class-name="mylogger.CustomerReporter"/>
	</listeners>
	
	<test name="Test One" >
	
		<parameter name="Browser" value="Firefox" />
	
		<classes>
			<class name="TestNGOnePack.ClassOne" />  
				<methods>
					 <include name="testmethodone" />
					 <exclude name="testmethodtwo" />
					 <exclude name=".*two.*"/>
				</methods>
				
			<class name="TestNGOnePack.ClassOne">
				<methods>
					<include name=".*two.*"/>
				</methods>
			</class>
		</classes>
	</test> 
	
	<test name="Test Two" >
		<classes>
			<class name="Testng_Pack.Test_Parallel"></class>
		</classes>
	</test> 

	<test name="Test One"  preserve-order="true" >
		<packages>
		
			<package name="TestNGTwoPack" />
			<package name="TestNGThreePack" />
			
			<package name="com.selvenium.*">
			   <include name="TestNGOnePack" />
			   <exclude name="TestNGThreePack" />
			</package> 
			
		</packages>
	</test> 
	
	<test name="Test One">
		<groups>
			<run>
				<include name="functionaltest" />
				<exclude name="UIDataValidation" />
			</run>
		</groups>
		
		<groups>
			<define name="group1">
				<include name="functionaltest" />
				<include name="UIDataValidation" />
			</define>
			<define name="group2">
				<include name="UIDataValidation" />
			</define>
			<run>
				<include name="group1" />
			</run>
		</groups>
		
		<groups>
			<dependencies>
				<group name="depedent-group" depends-on="test1  test2"/>
				<group name="depedent-group" depends-on="starts-with.*"/>
			</dependencies>
		</groups>
	</test>
</suite>


```
