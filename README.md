# Palindrome

Palindrome is a word, phrase, number or a group of characters that can be read from all directions, both backwards and forwards.

## Tests in this scripting problem will include

- Check is palindrome
Return true if given string is a palindrome otherwise return false(CHECK IF SPELLING IS SAME BOTH FORWARD AND BACKWARDS)
- Remove all non-alphanumeric characters
- Turning everything into lower case

### First test

- a simple function example to check if the string is a palindrome.

```js
    function palindrome(str) {
        Return true;
    }
    palindrome("eye")
```

### Second test

- Using REGEX or Regular Expressions to pass our second test
- A regular expression are patterns used to match character combinations in strings.
    `/[^A-Za-z0-9]/g` or `/[\W_]/g`.

### \W removes all non-alphanumeric characters

- \W matches any non-word character
- \W is equivalent to [^A-Za-z0-9]
- \W matches anything that is not enclosed in the brackets

```text
    [^A-Z] matches anything that is not enclosed between A and Z
    [^a-z] matches anything that is not enclosed between a and z 
    [^0-9] matches anything that is not enclosed between 0 and 9
    [^_] matches anything that does not enclose

```

- In our case, we require the palindrome `("0_0(:/-\:)0-0")` to return true.
  which means `_(:/-\:)-` has to be matched.

- We will add "_"
    that will make the expression `"\W_"`
- We also add the g flag for global search.
    So finally we will have something like this `/[\W_]/g`
    NOTE `/[\W_]/g`was used for demonstrative purposes only. For our case we will use the simplest regex version `/[^A-Za-z0-9]/g`

## JS Methods to be employed to this solution will include (using built-in functions)

- Returning the called string value converted to lowercase.

```js
    toLowerCase()
```

- Return a new string with some or all matches of a pattern replaced by a replacement. Using also our RegExp.

```js
    replace()
```

- To split a String object into an array of strings by separating the string into sub strings.

```js
    split()
```

- Reverse any array in place. Where the first array element becomes the last and the last becomes first.

```js
    reverse()
```

- Joining back all the elements in our array back to a string.

```js
    join()
```

```js
    function palindrome(str) {
        // Step 1. Lowercase the string and use the RegExp to remove unwanted characters from it
        var re = /[\W_]/g; // or var re = /[^A-Za-z0-9]/g;
        
        var lowRegStr = str.toLowerCase().replace(re, '');
        // str.toLowerCase() = "A man, a plan, a canal. Panama".toLowerCase() = "a man, a plan, a canal. panama"
        // str.replace(/[\W_]/g, '') = "a man, a plan, a canal. panama".replace(/[\W_]/g, '') = "amanaplanacanalpanama"
        // var lowRegStr = "amanaplanacanalpanama";
            
        // Step 2. Use the same chaining methods with built-in functions from the previous article 'Three Ways to Reverse a String in JavaScript'
        var reverseStr = lowRegStr.split('').reverse().join(''); 
        // lowRegStr.split('') = "amanaplanacanalpanama".split('') = ["a", "m", "a", "n", "a", "p", "l", "a", "n", "a", "c", "a", "n", "a", "l", "p", "a", "n", "a", "m", "a"]
        // ["a", "m", "a", "n", "a", "p", "l", "a", "n", "a", "c", "a", "n", "a", "l", "p", "a", "n", "a", "m", "a"].reverse() = ["a", "m", "a", "n", "a", "p", "l", "a", "n", "a", "c", "a", "n", "a", "l", "p", "a", "n", "a", "m", "a"]
        // ["a", "m", "a", "n", "a", "p", "l", "a", "n", "a", "c", "a", "n", "a", "l", "p", "a", "n", "a", "m", "a"].join('') = "amanaplanacanalpanama"
        // So, "amanaplanacanalpanama".split('').reverse().join('') = "amanaplanacanalpanama";
        // And, var reverseStr = "amanaplanacanalpanama";
        
        // Step 3. Check if reverseStr is strictly equals to lowRegStr and return a Boolean
        return reverseStr === lowRegStr; // "amanaplanacanalpanama" === "amanaplanacanalpanama"? => true
    }
 
    palindrome("A man, a plan, a canal. Panama");
```

### Without comments the solution will look like

```js
    function palindrome(str) {
        var re = /[\W_]/g;
        var lowRegStr = str.toLowerCase().replace(re, '');
        var reverseStr = lowRegStr.split('').reverse().join(''); 
        return reverseStr === lowRegStr;
    }
    palindrome("A man, a plan, a canal. Panama");
```

## Using a FOR loop statement to come up with a similar solution instead of built-in functions

- Using Half-Indexing (length/2) has benefits when we want to process large strings. We check the end from each part and divide the number of   iterations inside the FOR loop by two.

```js
    function palindrome(str) {
        // Step 1. The first part is the same as earlier
        var re = /[^A-Za-z0-9]/g; // or var re = /[\W_]/g;
        str = str.toLowerCase().replace(re, '');

        // Step 2. Create the FOR loop
        var len = str.length; // var len = "A man, a plan, a canal. Panama".length = 30
        
        for (var i = 0; i < len/2; i++) {
        if (str[i] !== str[len - 1 - i]) { // As long as the characters from each part match, the FOR loop will go on
            return false; // When the characters don't match anymore, false is returned and we exit the FOR loop
        }
        /* Here len/2 = 15
            For each iteration: i = ?    i < len/2    i++    if(str[i] !== str[len - 1 - i])?
            1st iteration:        0        yes         1     if(str[0] !== str[15 - 1 - 0])? => if("a"  !==  "a")? // false
            2nd iteration:        1        yes         2     if(str[1] !== str[15 - 1 - 1])? => if("m"  !==  "m")? // false      
            3rd iteration:        2        yes         3     if(str[2] !== str[15 - 1 - 2])? => if("a"  !==  "a")? // false  
            4th iteration:        3        yes         4     if(str[3] !== str[15 - 1 - 3])? => if("n"  !==  "n")? // false  
            5th iteration:        4        yes         5     if(str[4] !== str[15 - 1 - 4])? => if("a"  !==  "a")? // false
            6th iteration:        5        yes         6     if(str[5] !== str[15 - 1 - 5])? => if("p"  !==  "p")? // false
            7th iteration:        6        yes         7     if(str[6] !== str[15 - 1 - 6])? => if("l"  !==  "l")? // false
            8th iteration:        7        yes         8     if(str[7] !== str[15 - 1 - 7])? => if("a"  !==  "a")? // false
            9th iteration:        8        yes         9     if(str[8] !== str[15 - 1 - 8])? => if("n"  !==  "n")? // false
            10th iteration:        9        yes        10     if(str[9] !== str[15 - 1 - 9])? => if("a"  !==  "a")? // false
            11th iteration:       10        yes        11    if(str[10] !== str[15 - 1 - 10])? => if("c" !==  "c")? // false
            12th iteration:       11        yes        12    if(str[11] !== str[15 - 1 - 11])? => if("a" !==  "a")? // false
            13th iteration:       12        yes        13    if(str[12] !== str[15 - 1 - 12])? => if("n" !==  "n")? // false
            14th iteration:       13        yes        14    if(str[13] !== str[15 - 1 - 13])? => if("a" !==  "a")? // false
            15th iteration:       14        yes        15    if(str[14] !== str[15 - 1 - 14])? => if("l" !==  "l")? // false
            16th iteration:       15        no               
            End of the FOR Loop*/
        }
        return true; // Both parts are strictly equal, it returns true => The string is a palindrome
    }

    palindrome("A man, a plan, a canal. Panama");
```

### Removing the comments

```js
    function palindrome(str) {
        var re = /[^A-Za-z0-9]/g;
        str = str.toLowerCase().replace(re, '');
        var len = str.length;
        for (var i = 0; i < len/2; i++) {
            if (str[i] !== str[len - 1 - i]) {
                return false;
            }
        }
        return true;
    }
    palindrome("A man, a plan, a canal. Panama");
```

