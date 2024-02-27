# Title (replace with your title)

Introductory paragraph (replace this with your text)

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.

The following was copied from the MDN webdocs website URL https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions 
```
"Using regular expressions in JavaScript
Regular expressions are used with the RegExp methods test() and exec() and with the String methods match(), matchAll(), replace(), replaceAll(), search(), and split().

Method	Description
exec()	Executes a search for a match in a string. It returns an array of information or null on a mismatch.
test()	Tests for a match in a string. It returns true or false.
match()	Returns an array containing all of the matches, including capturing groups, or null if no match is found.
matchAll()	Returns an iterator containing all of the matches, including capturing groups.
search()	Tests for a match in a string. It returns the index of the match, or -1 if the search fails.
replace()	Executes a search for a match in a string, and replaces the matched substring with a replacement substring.
replaceAll()	Executes a search for all matches in a string, and replaces the matched substrings with a replacement substring.
split()	Uses a regular expression or a fixed string to break a string into an array of substrings."
```
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

### Anchors
* '^' This is called a 'Caret'. It is used to define the start of a line. It ensures that the pattern following it must appear at the beginning of the line.

Example: 

'^John is cool' indicates that AT THE START OF A LINE - this exact sequence can be found. 

* '$' is called simply a 'Dollar Sign'. It is used like a carat but the opposite way. It marks the END OF A LINE. It ensures that the pattern preceding is must appear at the end of the line. 

Example:

'John is cool$' indicates that at the END OF A LINE - this exact sequence can be found.

* '\b' This is a 'Word Boundary'. It is used to define the start and finish of a word. It's useful for looking up specific words and they can not be part of a larger word where the letters appear in that same sequence.

Example:

 '\bthe\b' will work for 'the' and EXCLUDE something like 'thermal'.

* '\B' This is a 'Non-Word Boundary'. It is used to define a sequence of characters NOT LIMITED TO A WORD. Essentially the opposite of how '\b' 'Word Boundaries' work.

Example:

  '\Bthe\B' will work for a word like 'thermal' but will EXCLUDE the word 'the'. 

### Quantifiers
Quantifiers are used to quantify how many of an occurrence of characters or sequences we are looking for in the expression. 

* '*' is called an 'Asterisk'. This is used to match zero or more occurrences of the preceding character or group. IT ALLOWS FOR EMPTY STRING and UNLIMITED OCCURRENCES.
Example: '9*' is saying that is will match ' ', AND '9', '99', '9999999', and so on. 

* '+' is called a 'Plus Sign'. This quantifier matches one or more occurrences of the preceding character or group. The character being specified MUST BE PRESENT.
Example: 'b+' matches 'b', 'bb', 'bbb', and so forth. 

* '?' Is called a 'Question Mark'.  Matches zero or one occurrence of the preceding character or group. It allows empty string BUT UNLIKE '*' it DOES NOT MULTIPLE OCCURRENCES.
Example: 'cd?' is saying it will match 'cd' OR ' '.

* '{n}' is called 'Braces With A Number'. This is a quantifier that specifies how many of a character or sequence are you looking for. VERY USEFUL for looking up phone numbers and things like that with specific and unique formatting. 
Example: '\d{3}' will look up numbers or 'digits' appearing at minimum 3 in a sequence. 
Example 2: '\d{3}[-.]\d{3}[-.]\d{4}' is specifying 999-999-9999 OR 999.743-1234 OR 555.555.5555.

* '{n,} is called 'Braces with a Number and a Comma'. This quantifier matches 'n' OR MORE(unspecified) occurrences of the preceding character or group.
Example: 'a{2,}' means it will look for things that have 'aa' OR MORE to an unspecified amount. 'aa', 'aaa', 'aaaaaaaaaaaaaa'.

* '{n,m} is called 'Braces with Two Numbers and a Comma'. This quantifier matches specifically 'n' or the amount of matches BETWEEN AND UP TO 'm' stated in the {}. 
Example: 'za{2,5}' means it will look for matches that have 'zaza', 'zazaza', 'zazazaza', OR 'zazazazaza'.   
BASICALLY anything that matches 'za' 2 to 5 times in sequence. 

### Grouping Constructs
Grouping constructs are used to create subexpressions WITHIN a larger expression. These subexpressions can be treated as a single unit, allowing for quantifiers (as seen above) or alternation to be applied to the entire group.

* '()' These are called 'Parentheses'. Creates a capturing group. It allows you to select MULTIPLE CHARACTERS as a single unit.
Example: 
  - (ab)+ matches 'ab', 'abab', 'ababab', and so on. The parentheses group 'ab' as a unit, and the + quantifier applies to the entire group.

  - (x|y) matches either 'x' or 'y'. The parentheses group the alternation construct, and the | (OR operator) applies to the entire group.

* '(?<name>...)' is a 'Named Capturing Group'.It creates a named capturing group, allowing you to refer to the matched content by a specified name. Basically allowing you to put IDs on to specific groups or sequences of characters. 
Example:
  - (?<day>\d{2})-(?<month>\d{2})-(?<year>\d{4}) creating a sequence of 02-05-1995.
  - Here is a snippet of javascript to further illustrate this concept:

```
const pattern = /(?<day>\d{2})-(?<month>\d{2})-(?<year>\d{4})/;
const text = '02-05-1995';

const match = pattern.exec(text);

if (match) {
  // Access the value of the 'month' named capturing group
  const monthValue = match.groups.month;
  console.log(`Month: ${monthValue}`);
}
```
* '(?:...)' is called a 'Non-Capturing Group'. It essentially searches for groups but allows for more 'wiggle-room' and is capable of gathering things with similar attributes.
Example:
  - \d{3}(?:-|\.)?\d{2} will match things with 3 digits and then 2 more after INCLUDING '-' OR '.' 
  - MEANING it could match things like 12345, 123-45, OR 123.45 

### Bracket Expressions
Bracket Expressions have been seen above in a few examples when explaining other regular expressions. They are essentially used to isolate something specific in a string of rejex query. Bracket Expressions can also be referred to as 'Character Expressions'. 

* '[ ]' This is a 'Bracket Expression'. It is used to specify what you're looking for OR to include some sort of rule in your rejex. I will cite the phone number example i had used above in an earlier example: 
  - Example: '\d{3}[-.]\d{3}[-.]\d{4}' is specifying 999-999-9999 OR 999.743-1234 OR 555.555.5555.
  - In this example, the section '[-,]' is being used to say that we will match digit sequences that have EITHER a '-' or a '.' 

  - Example 2: It can be used to search for specific sets like vowels or digits:
     - [aeiou] will search for any thing with 'a', 'e', 'i', 'o', 'u' 
     - [0-9] will search for anything with numbers 0 through 9. '1', '2', '3' etc. 

* '[^...]' is called a 'Negated Bracket Expression'. This is very similar to 'Bracket Expressions' BUT IS THE OPPOSITE. Instead of gathering things specified, it is going to gather things that don't match what's in the brackets - essentially excluding what is specified in the brackets. 
  - Example: 
     - [^aeiou] will search for all letters that ARE NOT vowels - i.e. consonants 
     - [^0-9] will search for characters that ARE NOT digits 

### Character Classes
Character classes are special shorthand codes that represent specific sets of characters. There are a lot of different character classes, I will be quickly summarizing them below:

* '\d' Represents any digit (0-9).
* '\D' Represents any non-digit character.
* '\w' Represents any word character (alphanumeric character plus underscore).
* '\W' Represents any non-word character.
* '\s' Represents any whitespace character (spaces, tabs, line breaks).
* '\S' Represents any non-whitespace character.
* '\t' Matches a horizontal tab.
* '\r' Matches a carriage return.
* '\n' Matches a linefeed.
* '\v' Matches a vertical tab.
* '\f' Matches a form-feed.
* '\0' Matches a NUL character. Do not follow this with another digit.
* '\' Indicates that the following character should be treated specially, or "escaped". It essentially isolates what follows it and allows things to become 'literal'. Example would be the '-' which can be 'a-z' but if you wanted 'a','-', and 'z' it would be '[a\-\z]'.
* '.' Can be used to match anything preceding a specific character. An example would be '.y' which will match things like 'hey', 'may', 'hockey' BUT WILL NOT MATCH 'yes' because there is nothing before the 'y'. 

### The OR Operator
* '|' Is called the 'OR operator'. It allows for the matching of multiple alternatives within a pattern. It functions as a logical OR, enabling the regex engine to match any of the alternatives specified. 

- The OR operator is used to provide alternatives for matching. For example, cat|dog will match either "cat" or "dog."

Example:

* grape|apple: Matches either "grape" or "apple."
* sun(day|set): Matches "sunday" or "sunset."
* Precedence: The OR operator has a lower precedence than grouping constructs. Parentheses ( ) can be used to control the scope of the OR operator.

### Flags
Flags in regular expressions are modifiers that control how the matching process behaves. They are added after the closing delimiter of the regular expression and affect various aspects of pattern matching. Here's a summary of common flags:

* 'd' is used to Generate indices for substring matches.
- Corresponding Property: hasIndices

* 'i' is called a 'Case-Insensitive Flag': Ignores the case of letters, making the pattern match regardless of letter case. 
- For example: /abc/i would match "ABC" or "aBc."
- Corresponding Property: ignoreCase

* 'g' is called a 'Global Flag': Performs a global search, finding all matches rather than stopping after the first match.
- Corresponding Property: 	global

* 'm' is called a 'Multiline Flag': Changes the behavior of ^ and $ anchors to match the start or end of each line within a multiline string.
- Corresponding Property:	multiline

* 's' is called a 'Dot-All Flag': Alters the behavior of the dot (.) to match any character, including newline characters.
- Corresponding Property: 	dotAll

* 'u' is called a 'Unicode Flag': Treats the pattern and input as Unicode, enabling the use of Unicode escapes and making quantifiers like \d work with Unicode characters.
- Corresponding Property:	unicode

* 'y' is called a 'Sticky Flag': Requires the match to start at the current position of the search string.
- Corresponding Property: 	sticky

* 'flags' are called 'Multiple Flags': Some regex engines allow combining multiple flags. 
- For example: /pattern/gi would enable both case-insensitive and global matching.


* '(?flag)' are called 'Inline Flags': Flags can also be applied inline within the pattern using (?flag) syntax. 
- For example, (?i)pattern makes the pattern case-insensitive.

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
