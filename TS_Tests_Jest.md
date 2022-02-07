# Jest
# Snippets
```TS
describe("MyClassToTest", () => {

	// ----- Synchrone

	test("MyMethodToTest_UseCase_ShouldSucceed", () => {
		//Arrange
		//Act
		//Assert
	});

	test("MyMethodToTest_TestCase_ShouldThrowException", () => {
		//Arrange
		//Act
		const action = () =>
		{
			throw new Error("my error");
		};
		//Assert
		expect(() => {
			action()			
		}).toThrow("my error");
	});

	test("MyMethodToTest_MultipleTestCases_ShouldSucceed", () => {
		const testCases: [] = [
			{ prop1: "a", prop2: "1", expectedResult: "a1" }, 
			{ prop1: "b", prop2: '2', expectedResult: "b2" }, 
			{ prop1: "c", prop2: '3', expectedResult: "c3" } 
		];

		testCases.forEach(testCase => {
			//Arrange
			let input = testCase;
			//Act
			let res = input.prop1 + input.prop2;
			//Assert
			expect(res).toBe(input.expectedResult);
		});
	});

	// skip cause description
	test.skip("MyMethodToTest_UseCase_ShouldSucceed", () => {
		//Arrange
		//Act
		//Assert
	});

	// ----- ASynchrone

	test("MyAsyncMethodToTest_UseCase_ShouldSucceed", async () => {
		//Arrange
		//Act
		//Assert
	});

	test("MyAsyncMethodToTest_TestCase_ShouldThrowException", () => {
		//Arrange
		//Act
		const action = async () =>
		{
			throw new Error("my error");
		};
		//Assert
		expect(async () => {
			await action()			
		}).toThrow("my error");
	});

	test("MyAsyncMethodToTest_MultipleTestCases_ShouldSucceed", async () => {
		const testCases = [
			{
				input: "input",
				expectedResult: "expectedResult"
			}
		];
		await Promise.all(
			testCases.map(async test => {
				//arrange
				//act
				let res = await repo.myMethod(test.input);
				//assert
				expect(res).toBe(test.expectedResult);
			})
		);
	});	

}
```

```TS
// SmokeTs

describe("SmokeTs", () => {

	test("toBe", () => {
		expect(1 + 2).toBe(3);
	});

	test("toEqual", () => {
		let a = {
			firstName: "toto",
			lastName: "tata"
		};
		let b = {
			firstName: "toto",
			lastName: "tata"
		};
		expect(a).toEqual(b);
	});

	test("toMatchObject", () => {
		let a = {
			firstName: "toto",
			lastName: "tata"
		};
		let b = {
			firstName: "toto"
		};
		let c = {
			lastName: "tata",
			firstName: "toto"
		};
		expect(a).toMatchObject(b);
		expect(a).toMatchObject(c);
	});
	
});
```


