# JavaScript

## JSON notation

```js
// a JavaScript object...:
var myObj = { "name":"John", "age":31, "city":"New York" };

// ...converted into JSON:
var myJSON = JSON.stringify(myObj);

// parsing JSON string to object
var obj = JSON.parse('{"firstName":"John", "lastName":"Doe"}'); 
```

Reference: https://www.w3schools.com/jsreF/jsref_obj_json.asp https://www.w3schools.com/jsreF/jsref_parse_json.asp

## Comparing strings

For equality:

```js
const str1 = '1st string';
const str2 = str1;
const str3 = '2nd string';

str1 === str2; // true
str1 === str3; // false
```

More on https://masteringjs.io/tutorials/fundamentals/string-compare
