# TS
# Destructuring

```TS
const obj1: any = {
      props1: "props1",
      props2: "props2",
      props3: "props3"
    };

    const {
      props1, props2, props3, props4
    } = obj1;
    console.log(props1); // "props1"
    console.log(props4); // undefined

    const obj2: any = {
      propsA: "propsA",
      propsB: "propsB",
      propsC: "propsC"
    };

    const {
      propsA, ...allPropsWithoutpropsA
    } = obj2;
    console.log(propsA); // "propsA"
    console.log(allPropsWithoutpropsA); // all obj2 props without propsA
```