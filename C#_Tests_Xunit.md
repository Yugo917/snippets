# Nunit	and FluentAssertion
```c#
[Trait("Category", "Unit")]
public class MyClassTest
{
	// ----- Synchrone

	[Fact]
	public void MyMethodToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		//Act
		//Assert
	}

	[Fact]
	public void MyMethodToTest_TestCase_ShouldThrowException()
	{
		//Arrange
		//Act
		var action = () =>
		{			
		};
		//Assert
		action.Should().Throw<Exception>().Where(e=>e.Message == "The excpeted error");
	}

	[Theory]
	[InlineData("value1")]
	[InlineData("value2")]
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

	[Theory]
    [MemberData(nameof(GenerateDataTests))]
	public void MyMethodToTest_MultipleTestCases2_ShouldSucceed(string value, int expectedResult)
	{
		//Arrange
		//Act
		//Assert
	}

	[Fact(Skip = "ignore cause description")]
	public async Task MyMethodToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		//Act
		//Assert
	}

	// ----- ASynchrone

	[Fact]
	public async Task MyMethodAsyncToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		//Act
		//Assert
	}
	
	[Fact]
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
			.Where(e => e.Message.Contains("The excpeted error"));
	}
	
	
	[Fact]
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
