# PureHelpers
Importable pure ES helper methods

Importable methods. Note: all methods are pure.

--
`randomString (prefix = "", minRandomNumberValue = 10000, maxRandomNumberValue = 10000000)`

=> It creates a random (hex) number string, possibly preceded with a prefix

   Returns string

--
`repeatString (string2Repeat, n2Repeat)`

=> It returns a string where [string2Repeat] is repeated [n2Repeat] times

-- 
`checkPostcode (postcodeStringCandidate)`

=> It checks a dutch postal code to be valid

   Returns boolean

-- 
`truncateString (string2Truncate, truncateAtPosition, truncateOnWholeWordsOnly)`

=> It truncates [string2Truncate] @ position [truncateAtPosition]

   if [truncateOnWholeWordsOnly] is true, string2Truncate will be truncated right after the last word in the truncated string

   Returns string

-- 
`numberBetween (number, min, max)` 

=> It determines if [number] falls between [min] and [max]
   
   Returns boolean

-- 
`padLeft (number, base = 10, char = "0")`

=> It left-pads a [number] with [base] - [number].length [char]
   
   Example:
   
   ```javascript
    > padLeft(15, 1000, "-");
    > "0015"
   ```
   
   Returns string

-- 
`interpolate (string2Interpolate, tokens)`

=> It is a string templating method, using {[someproperty]} in string and a token object to replace [someproperty]
   
   Example:
   
   ```javascript
    > interpolate("Hello {world}", {world: "folks"});
    > "Hello folks"
    ```
   
   Example:
   
   ```javascript
   > interpolate("Hello {world}\n", [{world: "folks"}, {world: "Pete"}]);
   > "Hello folks\nHello Pete"
   ```
    
   You can use it to extend String.prototype:
   
   ```javascript
   > String.prototype.interpolate = function (tokens) { return interpolate(this, tokens); };
   ```
    
   Example usage:
   
   ```javascript
   > "Hello {world}\n".interpolate([{world: "folks"}, {world: "Pete"}]);
   > "Hello folks\nHello Pete"
   ```
   
   Returns string

-- 
`tryParseDate (dateStringCandidateValue, format = "dmy")`

=> It tries to parse string [dateStringCandidateValue] into a Date instance using [format]
   
   [format] "dmy" = [d]ate, [m]onth, [y]ear
   
   Example: 
   
   ```javascript
   > tryParseDate("07/02/2015", "mdy")
   > (Date)2015-07-01
   ```
   
   Returns a Date instance or [null] if parsing fails

-- 
(this module) `import (methods2Import, intoNamespace = {})` 

=> It imports [methods2Import] (array or object) from [methods] (this lib)
   into namespace [intoNamespace]
   
   [methods2Import] May be an array of strings, e.g.  ["methoda", "methodb"],
   or an object with method names as keys, e.g. {methoda: 1, methodb: 2}
   
   Example: 
   
   ```javascript
   > const importedMethods = [lib].import({numberBetween: 1, truncateString: 1}, {});
   > importedMethods.numberBetween(15, 5, 20);
   > true
   ```
   
   If you want to import methods in the *current* namespace directly, use
   
   ```javascript
   > [lib].import({numberBetween: 1, truncateString: 1}, function() { return this; }());
   ```
   
   Now within your library file you can call
   
   ```javascript
    > numberBetween(15, 5, 20);
    > true
   ```
   
   Note: a non existing method will translate to a method returning an error string
   
   Returns [intoNamespace]