# Regular Expressions Tutorial
## Regular expressions allows us to use rules to search for patterns of text 

## Summary
## The piece of Regular Expressions I'd like to break down is this 
const emailRegex = 	/^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$/; 
let testString = "Some_Email@ABC123.org";
let result = emailRegex.test(testString); // TRUE

### The first line is an expression that would check for a valid email address
### The second line is our test string  
### The final line is taking our regex which was stored in variable emailRegex and compared our string to the rules using the test method to see if our string is valid, in this case it returns TRUE



## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

# Regex Components
### Anchors <a name="anchors"></a>
### Anchors in regex can be thought up as characters that don't belong to the actual string, but rather allow one to match a position before or after a character in the string. 

### ^ - The caret anchor matches the beginning of the text 
#### For example, in our expression ```/^([a-zA-Z0-9_\-\.]+)``` we are indicating that our string should start with either ```A-z```, a number ```0-9```, an underscore ```"_"```, a hyphen ```"-"```, or a period ```"."```
#### ```regexTest = /^(a-z)/```


## $ - The dollarsign anchor states that it must end with the characters that preceded it 

### Quantifiers

### OR Operator
### With regex we can use an or operator by using the pipe key (|) not to be confused with (I). Using | allows multiple matches to exist if one is looking for an exact match or variation
#### Ex. 

### Character Classes

### Flags

### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
