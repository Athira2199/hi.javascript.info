# The "switch" statement (स्विच स्टेटमेंट)


एक `स्विच` बयान एक से ज्यादा `इफ` जाँच प्रतिस्थापित कर सकता है


यह कई वेरिएंट के साथ एक मूल्य की तुलना करने के लिए अधिक वर्णनात्मक तरीका देता है।

## वाक्य रचना

एक `स्विच` एक या एक से अधिक है `केस`  ब्लॉक और एक वैकल्पिक डिफ़ॉल्ट।


यह इस तरह दिखता है:

```js no-beautify
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

- `X` के मान को पहले `केस` (यानी `value1`) से दूसरे (यानी `value2`)और इसी तरह सारे `केस` मान के लिए एक सख्त समानता के लिए जाँच की जाती है।
- यदि समानता पाई जाती है, तो `स्विच` संबंधित` केस` से शुरू होने वाले कोड को निष्पादित करना शुरू कर देता है, जब तक कि निकटतम `ब्रेक` (या` स्विच` के अंत तक)।
- यदि कोई मामला मेल नहीं खाता है, तो `डिफ़ॉल्ट` कोड निष्पादित किया जाता है (यदि यह मौजूद है)।

## An example

`स्विच` (निष्पादित कोड हाइलाइट किया गया है) का एक उदाहरण:

```js run
let a = 2 + 2;

switch (a) {
  case 3:
    alert( 'Too small' );
    break;
*!*
  case 4:
    alert( 'Exactly!' );
    break;
*/!*
  case 5:
    alert( 'Too large' );
    break;
  default:
    alert( "I don't know such values" );
}
```

यहाँ `स्विच` पहले `केस` वेरिएंट `3` से `a` की तुलना करना शुरू करता है । मैच फेल।


फिर `4`। यह एक मैच है, इसलिए निष्पादन `केस 4` से शुरू होता है जब तक कि निकटतम` ब्रेक` नहीं।

**यदि कोई `ब्रेक` नहीं है, तो निष्पादन बिना किसी जाँच के अगले` केस` के साथ जारी है।**


`ब्रेक` के बिना एक उदाहरण:

```js run
let a = 2 + 2;

switch (a) {
  case 3:
    alert( 'Too small' );
*!*
  case 4:
    alert( 'Exactly!' );
  case 5:
    alert( 'Too big' );
  default:
    alert( "I don't know such values" );
*/!*
}
```
ऊपर के उदाहरण में हम तीन `alert`s का अनुक्रमिक निष्पादन देखेंगे।

```js
alert( 'Exactly!' );
alert( 'Too big' );
alert( "I don't know such values" );
```

````smart header="Any expression can be a `switch/case` argument"
Both `switch` and `case` allow arbitrary expressions.

उदाहरण के लिए:

```js run
let a = "1";
let b = 0;

switch (+a) {
*!*
  case b + 1:
    alert("this runs, because +a is 1, exactly equals b+1");
    break;
*/!*

  default:
    alert("this doesn't run");
}
```
Here `+a` gives `1`, that's compared with `b + 1` in `case`, and the corresponding code is executed.
````

## Grouping of "case"

Several variants of `case` which share the same code can be grouped.

For example, if we want the same code to run for `case 3` and `case 5`:

```js run no-beautify
let a = 3;

switch (a) {
  case 4:
    alert('Right!');
    break;

*!*
  case 3: // (*) grouped two cases
  case 5:
    alert('Wrong!');
    alert("Why don't you take a math class?");
    break;
*/!*

  default:
    alert('The result is strange. Really.');
}
```

अब दोनों `3` और` 5` एक ही संदेश दिखाते हैं।

"समूह" मामलों की क्षमता एक साइड-इफेक्ट है कि `स्विच / केस` बिना` ब्रेक` के कैसे काम करता है। यहाँ `केस 3` का निष्पादन लाइन` (*) से शुरू होता है और `केस 5` से गुजरता है, क्योंकि वहाँ` ब्रेक` नहीं है।

## प्रकार मायने रखता है

आइए जोर देते हैं कि समानता की जांच हमेशा सख्त होती है। मान मिलान करने के लिए एक ही प्रकार के होने चाहिए।

उदाहरण के लिए, आइए कोड पर विचार करें:

```js run
let arg = prompt("Enter a value?");
switch (arg) {
  case '0':
  case '1':
    alert( 'One or zero' );
    break;

  case '2':
    alert( 'Two' );
    break;

  case 3:
    alert( 'Never executes!' );
    break;
  default:
    alert( 'An unknown value' );
}
```

1. For `0`, `1`, the first `alert` runs.
2. For `2` the second `alert` runs.
3. But for `3`, the result of the `prompt` is a string `"3"`, which is not strictly equal `===` to the number `3`. So we've got a dead code in `case 3`! The `default` variant will execute.
