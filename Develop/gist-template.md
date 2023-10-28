# Title (replace with your title)

Introductory paragraph (replace this with your text)

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components
- A regex is considered a literal, so must be wrapped in slash characters. 
- Two ways to create a regex object, first is literal notation (as above) and the second is to use a RegExp constructor, which use quotations instead. 
- Always case sensitive
### Anchors
- The characters ^ and $ are considered to be anchors. 
- ^ signifies a string that BEGINS with the characters that follow
    - EX: ^The would match "The" but not "the" 
- $ signifies a string that ENDS with the characters. 
### Quantifiers
- Set the limits of the string that your regex wishes to match. 
    - EX: ${3,16} will look for a string that is 3-16 characters long. 
- Quantifiers are inherently GREEDY, which means they match as many occurances as possible. Adding a ? after will make it LAZY, matching as few occurances as possible. 
- * matches the pattern zero or more times.
- + matches one or more times
- ? matches zero or one time
- {} provide three different ways to set limits
    - { n } will match pattern n number of times
    - { n, } will match the pattern at least n number of times
    - { n, x } will match pettern to a minimum of n, and maximum of x 
### Grouping Constructs
    - Using () within a regex will break up each part of the expression into a subexpression. 
        -EX: (abc):(xyz) 
            - Note the colon between subexpressions
            - Subexpressions look for an exact match unless told otherwise. 
            - Two categories, CAPTURING and NONCAPTURING - research more
                - Capturing will capture the matched character sequence for possible re-use
### Bracket Expressions
- Square Brackets represent a range of characters that we want to match 
    - EX: [abc] would match "aaa", "bin", "court", "bca"
- When using a hyphen between alphanumeric characters, it will represent a range of thsoe characters. 
    - EX: [a-c] and [abc] are functionally the same. 
- [a-z0-9_-] will want a string that includes a letter between a to z, a number between 0-9, and a underscore or hyphen. THey can be in any order. For this example, it's important to note that the string is not required to meet ALL of these requirements, but ANY of them. 
- Bracket Expressions can be turned into a NEGATIVE character group by adding ^ to the begining of the expression isinde the bracket. 
    - EX: [^aeiouAEIOU] would find a string that does not include a lowercase or uppercase vowel.
### Character Classes

### The OR Operator
- Or operator is | 
- While bracket expressions do not require the string to meet all requirements. To include this logic outside of a bracket expression, espcially in grouping constructs, use the OR operator. 
    - [abc] could be written as [a|b|c]
    - EX: (abc):(xyz) to (a|b|c):(x|y|z) makes "a;z" match, but "xyz:abc" would not
### Flags

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
