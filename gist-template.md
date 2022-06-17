# Regular Expressions Tutorial
## Regular expressions allows us to use rules to search for patterns of text 

## Summary
## The piece of Regular Expressions I'd like to break down is this 
```javascript
const emailRegex = /^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$/;
let testString = "Some_Email@ABC123.org";
let result = emailRegex.test(testString); // TRUE
```

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
## Anchors <a name="anchors"></a>
### Anchors in regex can be thought up as characters that don't belong to the actual string, but rather allow one to match a position before or after a character in the string. 

### ^ - The caret anchor matches the beginning of the text 
#### For example, in our expression<br> ```/^([a-zA-Z0-9_\-\.]+)```<br> we are indicating that our string should start with either "A-z", a number "0-9", an underscore "_", a hyphen "-", or a period "."
#### Another example <br>```regexTest = /^(a-z)/``` <br> if we ran <br>```regexTest.test("!hello everyone")```<br> it would return FALSE becuase the string does not begin with characters a-z.<br>If our expression read as <br>```regexTest = /^(!)/```<br> Then that would indicate that our string MUST begin with "!" for it to return true, then our original <br> ```regexTest.test("!hello everyone")```<br> would return true. 

### $ - The dollarsign anchor states that it must end with the characters that preceded it 
#### Our code <br>```([a-zA-Z]{2,5})$/```<br>signifies the string must end in with uppercase or lowercase characters, don't worry about the {2,5} we will cover that a little later.<br>Because this checks for email something like .com, .org, .co would all be valid entries. <br>If the string ended with .123 or .com! it would return false because anything besides a-z is not allowed. 

## Quantifiers <a name="quantifiiers"></a>
### With regex we can control how many times a pattern or character should appear. With our code <br>
```javascript
const emailRegex = /^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$/;
```
### we can spot the + symbol inside
```Javascript
//first half before the @
 /^([a-zA-Z0-9_\-\.]+)
 //second set after the @
 ([a-zA-Z0-9_\-\.]+)
 ```
 ### This indicates that the pattern of letters, numbers, underscore or dash can be repeated more than once. If my entry was "P@J" this would be valid as well as "ZZZZZZZZZ@1" The quantafier (+) indicates that we CAN repeat the preceding pattern 1 or more times
 
 ### The other quantifier is towards the end of our code enclosed by curly brackets {}
 ```Javascript
 ///this pattern is for the domain extension
 ([a-zA-Z]{2,5})$/;
 ```
 ### We see<br> ```{2,5}```<br> this indicates that our pattern must repeat a minimum of 2 times but no more than 5 times this is a little more close ended than our previous quantifier of "+". It wouldn't make much sense to have + as a domain extension because most are about 3 letter words such as .com or .org. Leaving the pattern with + would open us up to full words and likely fake extensions. 

## OR Operator <a name="or-operator"></a>
### The OR Operator is a denoted by the | character, usually used with grouping. Not used current example

## Character Classes <a name="character-classes"></a>
### Character classes match the specific set of characters requested
```Javascript
[a-zA-Z0-9_\-\.]
``` 
### here we have multiple character sets stating any character that matches these rules<br>a-zA-z represents any letter lowercase or uppercase, any digit.<br>The caracter also get into specific when we specifically name characters for example<br>
```Javascript
_\-\.]+)@
```
### in the preceding example we have specific characters being called "_", "-", ".", @. You'll notice that both the hyphen"-" or the "." both have a backslash \ before the character. This is an escape character as those characters without the escape have special meanings.<br> The "@" indicates that following that first group a @ character is needed there.<br>We could also replace our first group with the dot character class.
```Javascript
//works like /^([a-zA-Z0-9_\-\.]+)@
/^(.+)@/
```
### Using "." without a character escape matching any characters except for linebreaks. We would essentially be saying the same thing with this notation.<br>Notice that we have <br>```([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$```<br> here our character class is again called for specifically with<br>```\.```<br> stating we need a period in that possition and not any character. 
### There is more than one way to specify what characters to select.

## Flags <a name="flags"></a>
### Flags are located at the end of the closing "/" Our example does not use any flags an example of what this might look like is 
```javascript
([a-zA-Z]{2,5})$/i
```
### The i following the closing / indicates that the entire expression can ignore case, this would remove the need to indicate<br>```[a-zA-Z]```<br>

## Grouping and Capturing <a name="grouping-and-capturing"></a>
### Grouping is denoted by paranthesis () in our example we have created 3 groups to allow for the string to be broken up and follow specific rules depending on the section or the string<br>Our first group is 
```javascript
/^([a-zA-Z0-9_\-\.]+)
```
### This group is before our @ allows for the first half part of an email address. The next group or rules we need are the same but we have specified that this pattern must follow the @ 
```Javascript
/^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)
```
### this for example says email@somedomain<br>Lastly our final group is only characters and a quantifier with specific settings, this is to say that the last group can only be a letter of length n 
```javascript
/^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$/
```
### The final group or rules follows a period and only 2-5 characters in length. For example `Email@SomeDomain.ORG`

## Bracket Expressions <a name="bracket-expressions"></a>
### Bracket expressions are inside square brackets []. This kind of expression is used for ranges. We have a few in our expression 
```Javascript
// We have a set of ranges per each group, this is the last range in our example 
[a-zA-Z]
```
### Here we are saying any character between a-z works regardless of pattern. All of these examples would return true<br>```"apples", "hi", "sdsdsa", "bbbbbbbbbbbbb"```<br> In our example of bracket expression we are saying find any character or string regardless of length so long as its between a-z. The hyphen allows us to say anything between otherwise we would have to right something along the lines of <br>```[abcdef....]```<br>

### Greedy and Lazy Match <a name="greedy-and-lazy-match"></a>

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
