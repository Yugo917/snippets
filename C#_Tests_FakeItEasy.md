# FakeItEasy
````c#
//Create a fakeObject
var myFake = A.Fake<IMyInterface>();

//Replace the method behavior

// to return value
A.CallTo(() => myFake.myMethod1(A<Type1>._))
	.Returns(newReturn);

// to return async value
A.CallTo(() => myFake.myMethod1Async(A<Type1>._))
	.Returns(Task.FromResult(newReturn));

// to lazy return value
A.CallTo(() => myFake.myMethod1(A<Type1>._))
	.Returns(newReturn1);
A.CallTo(() => myFake.myMethod2(A<Type1>._))
	.ReturnsLazily((T inputIsnewReturn1)=>{newReturn2CoputedWIthnewReturn1});

// to throw exception			
A.CallTo(() => myFake.myMethod1(A<Type1>._))			
	.Throws(new Exception());

// to invoke an other method
A.CallTo(() => myFake.myMethod1(A<Type1>.That.Matches(s=>s.Id == "toto")))
	.Invokes(_ =>
	{
		other.Method2();
	});

// to capture the argument given to the method			
Type1 ObjToSnipe = null;
A.CallTo(() => myFake.myMethod1(A<Type1>.That.Matches(x => x.Id == "toto")))
	.Invokes(input =>
	{
		ObjToSnipe = (Type1)input.Arguments[0];
	});

// to simulate incremental behavior
A.CallTo(() => myFake.DoAction())
		.Throws<ArgumentException>().NumberOfTimes(1)
		.Then.Throws<TimeoutException>().NumberOfTimes(1)
		.Then.Throws<SystemException>().NumberOfTimes(1);

//Create a TestProxyObject
var myTestProxyObject = A.Fake<MyType>(x =>
	{
		x.WithArgumentsForConstructor(() => new MyType());
		x.CallsBaseMethods();
	});

A.CallTo(() => myTestProxyObject.myMethod1())
	.Invokes(input =>
	{
		other.Method2();
	})
	.CallsBaseMethod();

//Assert the method execution			
A.CallTo(() => myFake.myMethod1(A<Type1>._)).MustHaveHappenedOnceExactly();
A.CallTo(() => myFake.myMethod1(A<Type1>.That.Matches(x => x.Id == "toto"))).MustHaveHappenedOnceExactly();
```
