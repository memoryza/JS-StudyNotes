# 生成一个length为m,数组向为n的数组，不适用for循环。

```js
 // 探索生成length为m，值为n的数组，不能使用for,因为不能使用for map、forEach、filter、find就都不是用了

        // 1.使用new Array().fill()
        let m = 10;
        // let n = { value: 1 };
        // let n = 1;
        let n = '2';
        const arr1 = new Array(m).fill(n);
        // console.log('arr1: ', arr1);

        // 2.使用字符串
        function createArr(m, n) {
            let strArr = JSON.stringify(n) + ',';
            strArr = strArr.repeat(m).split(",");
            // console.log('strArr: ', strArr);
            //strArr.padEnd(10,1);  or strArr='1';strArr.padStart(10) 
            // 会看到结果是 字符串数组 ["1", "1", "1", "1", "1", "1", "1", "1", "1", "1"]
            //若想要数组项为num、boolean、obj、arr等怎么办
            strArr.forEach((element, i) => {
                Object.defineProperty(strArr, `${i}`, {
                    get() {
                        return JSON.parse(element);
                    }
                })
            });
            return strArr;
        }
        const strArr = createArr(m, n);

        //3递归
        const createArr1 = function (m, n) {
            const arr = [];
            (function (m, n) {
                arr.push(n);
                if (arr.length != m) {
                    arguments.callee(m, n);
                }
            })(m, n);
            return arr;
        };
        const newArr1 = createArr1(m, n);
        console.log('newArr1: ', newArr1);

        const createArr2 = function () {
            const arr = [];
            return function (m, n) {
                arr.push(n);
                if (arr.length == m) {
                    return arr;
                }
                arguments.callee(m, n);
            }
        }();
        const newArr2 = createArr1(m, n);
        console.log('newArr2: ', newArr2);

        //4.while

        function whileCreateArr(m, n) {
            const arr = [];
            while (arr.length < m) {
                arr.push(n)
            }
            return arr;
        }
        const whileArr = whileCreateArr(m, n);
        console.log('whileArr: ', whileArr);

```