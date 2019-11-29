- Const: normal const


- $ dollor sign: ${}


- Let x
    - Can not use it before it is declared
    - Block-scope variable, while var is function-scope
    - At the top level, let, unlike var, does not create a property on the global object:
var foo = "Foo";  // globally scoped
let bar = "Bar"; // globally scoped

console.log(window.foo); // Foo
console.log(window.bar); // undefined


- For string
    - Let string
    - ${string} 
    - Using back-ticks ( ` ` ) instead of the quotation marks
    - console.log(`This is ${firstName} ${lastName}
    - Methods
        - String.startWith(‘k’);
        - String.endWith(‘k’);
        - String.includes(‘oh’);
        - String.repeat(5);
            - // String String String String String


- Arrow function
    - You can NOT using ’this’ in addEvenListener()
    - => this method share the lexical ’this’ keyword from its surrounding！！！
    - Obj内的方程，再嵌套方程，里面的this指向的就是global variable了



- Destructuring
        const {firstName, lastName} = obj;
        console.log(firstName);    
        console.log(lastName);
    
        const {firstName: a, lastName: b} = obj;
        console.log('a:' + a);
        console.log('b:' + b);



- Array in ES6/ES2015
    - Array.from(boxes);      //转换list到array
        - var boxesArray6 = Array.from(boxes);
    - for (const cur of boxesArray6) {
                        If (cur.className === “”){
                        }
                     }
    - The findIndex() method returns the index of the first element in the array that satisfies the provided testing function. Otherwise, it returns -1, indicating that no element passed the test.
        - Temp = Array.findIndex(cur => cur < 18);
        - Temp = Array.find(cur => cur < 18);


- Call( ), apply( ), bind( )
    - In Call, apply function, the first argument would replace the origin ’this’
        - In other word, change the ’this’ pointer in the original function
    - Bind( ), could return a new function


- Spread operator
    - all = [h, ...boxes]
        - All 是array
        - Boxes 是 nodelist
        - 不需要用 Array.from(all) 去转化为array

- Rest parameters
    - No input: there is a input arguments [array]
    - One input, the rest parameters are arguments[array]



- array
    - Array.prototype.splice( 5, 2, ‘bob')
        - Which means replace 2 elements at index 5, with ‘bob'
    - Array.from( )
    - Array.findIndex( )
    - Array.find( )
    - for (const cur of Array){ }
    - Array.forEach(function(cur, index, array){ })
    - `Array.slice(a,b)`
        - Index a -> b became a new array for itself [a, b)
    - Array.map(el => el.numTree)
        - Return a array that [树1的数量，树2的数量…..]


- Array.reduce，你可以把它变成calc的方程，超赞！

function calc(arr) {
    const sum = arr.reduce((prev, cur, index) => prev + cur, 0);
    return [sum, sum / arr.length];
}




- array
    - forEach() — executes a provided function once for each array element.
    - map() — creates a new array with the results of calling a provided function on every element in the calling array.
        - Map( ) is faster than forEach( )









