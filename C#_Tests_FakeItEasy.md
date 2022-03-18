# FakeItEasy
````c#
//Create a fakeObject
var myFake = A.Fake<IMyInterface>();

//Replace the method behavior

// to return value
A.CallTo(() => myFake.myMethod1(A<Type1>._))
	.Returns(newReturn);

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
