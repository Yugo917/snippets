# Nunit	and FluentAssertion
## Tests
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
		throw new NotImplementedException();
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
		action.Should().Throw<Exception>().Where(e=>e.Message == "The expected error");
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
		throw new NotImplementedException();
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
			.Where(e => e.Message.Contains("The expected error"));
	}

	[Fact]
	public async Task MyMethodAsyncToTest_UseCase_ShouldThrowHttpException()
	{
		//Arrange
		//Act		
		var action = async () =>
		{
			var _ = await myApi.myMethod1();
		};
		//Assert
		(await action.Should().ThrowAsync<ApiException>()).Where(x => x.StatusCode == HttpStatusCode.BadRequest)
                                                       .And.Content.Should()
                                                       .Contain("the Date must not be a default value")
                                                       .And.Contain("The Prop1 field is required.")
                                                       .And.Contain("The Prop2 field is required.");
	}
	
	
	[Fact]
	public async Task MyAsyncWorkFlowToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		var waitTimeout = TimeSpan.FromSeconds(1);
		var mre = new ManualResetEvent(false);
		var messageToSnipe;
		bus.subscribe((message)=>{
			messageToSnipe = message;
			mre.set()
		});
		//Act
		bus.sendMessage("MyMessage");
		//Assert
		mre.WaitOne(waitTimeout).Should().BeTrue();
	}	

	[Fact]
	public async Task MyAsyncWorkFlowToTest2_UseCase_ShouldSucceed()
	{
		//Arrange
		var waitTimeout = TimeSpan.FromSeconds(1);
		var countEvent = new CountdownEvent(2);
		bus.subscribe((message)=>{
			mre.Signal();
		});
		//Act
		bus.sendMessage("MyMessage1");
		bus.sendMessage("MyMessage2");
		//Assert
		countEvent.Wait(WaitTimeout);
        countEvent.IsSet.Should().BeTrue();
	}
}
```		 
## Fixture
```c#
public class MyFixture
{
	public string MyProp1 { get; }

	public MyFixture
	{

	}
}

[CollectionDefinition(nameof(MyFixtureTestCollection))]
public class MyFixtureTestCollection : ICollectionFixture<MyFixture>
{
    // This class has no code, and is never created. Its purpose is simply
    // to be the place to apply [CollectionDefinition] and all the
    // ICollectionFixture<> interfaces.
}

[Trait("Category", "Unit")]
[Collection(nameof(MyFixtureTestCollection))]
public class MyClassTest
{

	private readonly MyFixture fixture;

    public MyClassTest(MyFixture fixture)
    {
        this.fixture = fixture;
    }


	[Fact]
	public void MyMethodToTest_UseCase_ShouldSucceed()
	{
		//Arrange
		//Act
		//Assert
	}
}

```	