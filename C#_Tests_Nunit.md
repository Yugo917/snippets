# Nunit	and FluentAssertion
```c#
[Category("unit")]
public class MyClassTest
{
	// ----- Synchrone

	[Test]
	public void MyMethodToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		//Act
		//Assert
	}

	[Test]
	public void MyMethodToTest_TestCase_ShouldThrowException()
	{
		//Arrange
		//Act
		var action = () =>
		{			
		};
		//Assert
		action.Should().Throw<Exception>().Where(e=>e.Message == "The expected error");;
	}

	[TestCase("value1")]
	[TestCase("value2")]
	public void MyMethodToTest_MultipleTestCases_ShouldSucceed(string variable)
	{
		//Arrange
		//Act
		//Assert
	}

	public static IEnumerable<object[]> GenerateDataTests()
	{
		var data = new List<object[]>()
		{
			new object[] {"MyValue1",  1},
			new object[] {"MyValue2",  2}
		};
		return data;
	}

	[TestCaseSource(nameof(GenerateDataTests))]
	public void MyMethodToTest_MultipleTestCases2_ShouldSucceed(string value, int expectedResult)
	{
		//Arrange
		//Act
		//Assert
	}

	[TestCase(Ignore = "ignore cause description")]	
	public async Task MyMethodToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		//Act
		//Assert
	}

	// A UnityTest behaves like a coroutine in Play Mode. In Edit Mode you can use
	// `yield return null;` to skip a frame.
	[UnityTest]
	public IEnumerator Repository_TestWithEnumeratorPasses()
	{
		// Use the Assert class to test conditions.
		// Use yield to skip a frame.
		yield return null;
	}

	// ----- ASynchrone

	[Test]
	public async Task MyMethodAsyncToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		//Act
		//Assert
	}
	
	[Test]
	public async Task MyMethodAsyncToTest_UseCase_ShouldThrowException()
	{
		//Arrange
		//Act		
		var action = async () =>
		{
			var _ = await myApi.myMethod1();
		};
		//Assert
		(await action.Should().ThrowAsync<Exception>())
			.Where(e => e.Message.Contains("The expected error"));
	}
	
	
	[Test]
	public async Task MyAsyncWorkFlowToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		var waitTimeout = TimeSpan.FromSeconds(5);
		var mre = new ManualResetEvent(false);
		var messageToSnipe
		bus.subscribe((message)=>{
			messageToSnipe = message;
			mre.set()
		});
		//Act
		bus.sendMessage("MyMessage");
		//Assert
		mre.WaitOne(waitTimeout).Should().BeTrue();
	}	
}
```		 
