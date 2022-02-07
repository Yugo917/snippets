# JEST MOCK
```TS
//Create a mockedObject
const myMock = mock<IMyInterface>();

//Replace the method behavior

// to return value
myMock.myMethod1.mockReturnValue(newReturn);

// to throw exception	
myMock.myMethod1.mockImplementation(() => {
  throw new Error('MyError');
});

// to invoke an other method
myMock.myMethod1.mockImplementation(() => {
  other.Method2();
});

WIP
https://codewithhugo.com/jest-fn-spyon-stub-mock/
```

# Simple Fake
```TS
//Create a mockedObject
const fake: IMyInterface = {} as any;

//Replace the method behavior
fake.myMethod1 = () => { return newReturn }
fake.myMethod1 = async () => { return Promise.resolve(newReturn) }

// to throw exception		
fake.myMethod1 = () => { new Error('MyError') }

// to invoke an other method
fake.myMethod1 = () => { other.Method2() } 

```