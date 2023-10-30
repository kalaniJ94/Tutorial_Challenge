# Regulars Expressions Explained & Dissected 

Regular expressions, often referred to as regex, are a powerful tool for pattern matching and text manipulation in programming and text processing. They provide a concise and flexible way to search for and manipulate text based on specific patterns. In this tutorial, we'll dive into the fundamentals of regex and explore how they work, enabling you to harness their capabilities to solve complex text-related tasks in your coding projects. I'll provide a real-life example of a commonly used regex for us to follow along with, and come out on the other side with a better understanding of how we can use regexes in our day to day coding journey.   

## Summary

Let's begin by taking a brief look at one of the most common uses of a regex: validating the creation of a "strong" password, using rules that we create. 

/^(?=[A-Za-z0-9]*[A-Z])(?=[A-Za-z0-9]*[a-z])(?=[A-Za-z0-9]*\d)(?=[A-Za-z0-9]*[^A-Za-z0-9])[\S]{8,16}$/

Does that look intimidating? Don't worry, We'll break this string down into easy to understand snippets. 

## Table of Contents

- [Introduction](#Introduction)
- [Regex Components](#regex-components)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Introduction
 So what exactly is a Regex? Spoken plainly, a regex (shorthand for "Regular Expression") is a sequence of characters that define a search pattern. This pattern is usually used to find or replace text within a given string or database. 

Let's start with a small example. Let's say we have a sting, like so: 

let string = "computer car fox cat mac"

 If we'd like to find every word that starts with the letter "c", we could use a regex: 
"/\bc\w+/g" would return computer, car, cat, but not mac or fox. This could be implemented like so: 

let string= "computer car fox cat mac";
let regex = /\bc\w+/g;
let matches = string.match(regex);
console.log(matches);

Basic syntax syntax is very simple, and follows a /pattern/modifiers template. That being, the pattern is the expression we want to match, and is wrapped in our defining slashes. It is followed by any modifiers we'd like to add, which are optional and can be used to specify how the regex will be implemented. 

## Regex Components

There are two ways to create a regex, the first being literal notation, as we are doing in our master example. The second is through the use of a RegExp constructor, such as: 
const pattern = new RegExp("apple);
This search would look for the word "apple within a string. 

Our code example, being a literal, works differently. Firstly, we wrap our code in a "/" character, which is a universal rule used to indicate to the computer the beginning and end of our expression. This is known as a Delimiter. 
    
It's also important to note at this stage of our tutorial, that a regex is always case sensitive. Thus, in our example code, we must include both a-z and A-Z in the search. We will expand on these parameters soon. 

### Anchors
Anchors(^ and $) are characters that define where exactly the pattern should begin and end its matching function in a given input string. 

The ^ (aka caret) defines a "beginning of the line" anchor. Thus, the $ character is the "end of the line" anchor. Together, they define that the rules of our strong password must remain true throughout the entire sting. without them, the regex would match part of the password, but possibly not all. By including them, we will ensure a strong password throughout the entire sting. 

Anchors can also be used to search for words that begin or end with a certain character. For example, /^J/ would return "Jupiter", while /$t/ would return "Javascript". 

### Quantifiers
Let's take a quick look at a particular section of our regex. 
[\S]{8,16} is found at the end of the pattern, and defines how many characters should be found in our password. [\S] is a character class which will match any non-whitespace character, while {8,16} defines how many of these characters there should be. For our purpose, they together create a rule that there should be bewtween 8 and 16 characters in the password. 

The curly bracket characters are used to define the quantifier, and can be used in three ways:
     - { n } will match pattern n number of times
    - { n, } will match the pattern at least n number of times
    - { n, x } will match pattern to a minimum of n, and maximum of x 

Another important note to make of quantifiers is that they are inherently "Greedy", which means they will match the pattern as many times as possible. This can be changed by adding the following characters:
- * matches the pattern zero or more times.
- + matches one or more times
- ? matches zero or one time

### Grouping Constructs
By rule, using the () characters within a regex will break that portion into a "subexpression", which will follow different rules. Our password regex makes use of these to create multiple "Positive Lookahead Assertions". These are grouping constructs that look ahead in the string without consuming characters, and check if certain conditions are met from the current position. 

In our example, "(?=[A-Za-z0-9]*[A-Z])" will enforce at least one uppercase letter in the string, without consuming any character. (?=) will assert a positive lookahead assertion. "[A-Za-z0-9]*" seeks to match zero or more alphanumeric characters. "[A-Z]" will match one uppercase letter. 

There are two categories of subexpressions, Capturing, and Non-Capturing. a "captured" expression will be stored for possible re-use later in the expression. Additionally, it is important to note that subexpressions will always look for an exact match, unless told to do so otherwise. 
### Bracket Expressions
Bracket Expressions are used within regexes to define a range of characters that we want to match, usually at a given position within the pattern. 

For example, a regex that is [abc] would match "aaa", "court" or "bca". This is because once definied within a bracket expression, it is required to meet ANY requirement, not all of them, and in any order. Furthermore, within square brackets, a hyphen can be used to represent a range of characters. This means that [a-c] and [abc] are functionally the same. Special characters within bracket expressions are treated as their literal characters, and not their special regex meanings. 

Lastly, by including a ^ at the beginning of a bracket expression, you can turn it into a negative search, which would return characters not in the defined set. For example, [^aeiouAEIOU] would return a sting that does not include a lowercase or uppercase vowel. We use this in our password regex to ensure the presence of one non-alphanumeric character within the password. 

### Character Classes
- A character class in a regex defines a set of characters, any one of which can occur in an inout string to fufill a match. Bracket Expressions, for example, are considered character classes
    - EX: . matches any character except the newline command (\n)
            \d matches any Arabic numeral. Equivalent to [0-9]
            \w Matches any alphanumeric character , including an underscore. Equivalent to [A-Za-z0-9_]
            \s Matches a single whitespace character, including tabs and line breaks
        - These examples can be made INVERSE by capitalizing the letter. 
            EX: \D matches a non-digit character

Character classes are a fundamental concept of regexes, which allow you to define sets of characters that can be matched at a specific position in a regex pattern. They are usually used in tandem with the square brackets, as covered above. There are a couple of shorthand commands that can be used within these patterns as well, such as: . matches any character except the newline command (\n)
    \d matches any Arabic numeral. Equivalent to [0-9]
    \w Matches any alphanumeric character , including an underscore. Equivalent to [A-Za-z0-9_]
    \s Matches a single whitespace character, including tabs and line breaks

At this point, our example regex to validate a strong password should make sense to us. It is composed of several grouping constructs that each work together to define the rules of our password. It must be between 8 and 16 characters, contain one uppercase and one lowercase letter, as well as one non-alphanumeric character. 

There are a couple of other concepts to cover to give you  abetter understanding of regexes, however. 

### The OR Operator
The OR operator is a powerful concept, broadly used across programming in general, but has a very literal meaning.  In the context of regexes, it can be used to define alternative strings. For example, 'cat|dog' would match either "cat" or "dog" within a given string. 

### Flags
Flags are modifiers that can be added to a regex pattern to effect it's behavior during matching. There are several common examples: 
        (i) will make a search case-insensitive. 
        (g) defines a search as global, and will allow a search to continue after finding the first match. THis is useful for when you are searching for multiple instances.
        (m) is used to indicate that the anchor characters (^ and $) should match along a string that is located along a multiline string.
        (s) will allow the . metacharacter to match any character, instead of the default that will ignore such a character. 
        (u) will allow the regex to use Unicode characters. 
        (y) is used for "sticky" matching, which will allow pattern matching from the last index where the previous matching occurred. This is particularly useful for incremental or sequential matching. 

For example, here are some flags in use: 
const pattern = /apple/gi; would look for case insensitive and global uses of "apple". 

### Character Escapes
    - The backslash (\) character is used to escape a character that would otherwise be interpreted literally. 
        - EX: { would be used to start a quantifier, but adding a \{ would mean you could look for the character instead. 
    - All characters, including \, lose their significance inside of bracket expressions. 

Character escapes (used by a backslash character \) are used to "escape" a character that would other be intrepreted litterally by the regex. For example, { would normally be used to start a quantifier, but by adding a \, we can instead search for the character instead. 
## Author

My name is Kalani Jones, and I hope you found this article enligtening and helpful. I'm currently a coding bootcamp student, but I've been a chef for nine years and have a passion for teaching and helping others understand topics. Thanks for reading! 