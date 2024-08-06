# Regex Tutorial

a tutorial that explains how a specific regex functions by breaking down each part of the expression and describing what it does.


## Summary

Regex, or regular expression for short, is a sequence of characters that defines a specific search pattern. When included in code or search algorithms, regex can be used to find certain patterns of characters within a string, or to find and replace a character or sequence of characters within a string. They are also frequently used to validate input.

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

## Regex Components

### Anchors
- Anchors are special characters used to match positions in a string rather than specific characters. They help you control where in the string a pattern should match.

 Example: const text = "Hello, world! Welcome to regex testing.";

- /^Hello/: This regex matches "Hello" only if it is at the start of the string. In this example, text.match(patternStart) finds "Hello" at the beginning of the text.

```// ^ (Caret) - Matches the start of the string
const patternStart = /^Hello/;
const matchStart = text.match(patternStart);
console.log(`Start match: ${matchStart ? matchStart[0] : 'No match'}`);
```
- /testing/.$/: This regex matches "testing." only if it is at the end of the string (with the period included). The $ ensures that it matches only if "testing." is the very last part of the text.

```// $ (Dollar Sign) - Matches the end of the string
const patternEnd = /testing/.$/;
const matchEnd = text.match(patternEnd);
console.log(`End match: ${matchEnd ? matchEnd[0] : 'No match'}`);
```
- \bworld\b: This regex matches "world" as a whole word. \b ensures that "world" is a separate word, not part of another word.

```// \b (Word Boundary) - Matches whole words
const patternWordBoundary = /\bworld\b/;
const matchWordBoundary = text.match(patternWordBoundary);
console.log(`Word boundary match: ${matchWordBoundary ? matchWordBoundary[0] : 'No match'}`);
```
- \Bworld\B: This regex matches "world" only if it is inside another word. In this example, it won't match because "world" is a whole word in the text, not part of another word.

```// \B (Non-Word Boundary) - Matches positions inside words
const patternNonWordBoundary = /\Bworld\B/;
const matchNonWordBoundary = text.match(patternNonWordBoundary);
console.log(`Non-word boundary match: ${matchNonWordBoundary ? matchNonWordBoundary[0] : 'No match'}`);
```

### Quantifiers
- Quantifiers specify how many times an element should be matched

Example: const text = "aaa aa a aaaa";

- /a*/g: This regex matches 0 or more occurrences of "a". The g flag (global) allows matching all occurrences in the text. It matches "", "a", "aa", "aaa", etc.

```// * (Asterisk) - Matches 0 or more occurrences
const patternAsterisk = /a*/g;
console.log("Matches for 'a*':", text.match(patternAsterisk));
```
- /a+/g: This regex matches 1 or more occurrences of "a". It finds sequences like "aaa", "aa", "a".

```// + (Plus) - Matches 1 or more occurrences
const patternPlus = /a+/g;
console.log("Matches for 'a+':", text.match(patternPlus));
```
- /a?/g: This regex matches 0 or 1 occurrence of "a". It finds "", "a", and is included between other matches.

```// ? (Question Mark) - Matches 0 or 1 occurrence
const patternQuestion = /a?/g;
console.log("Matches for 'a?':", text.match(patternQuestion));
```
- /a{3}/g: This regex matches exactly 3 occurrences of "a". It finds "aaa".


```// {n} (Exact Number) - Matches exactly 'n' occurrences
const patternExact = /a{3}/g;
console.log("Matches for 'a{3}':", text.match(patternExact));
```
- /a{2,}/g: This regex matches 2 or more occurrences of "a". It finds "aa", "aaa", "aaaa", etc.

```// {n,} (At Least 'n') - Matches 'n' or more occurrences
const patternAtLeast = /a{2,}/g;
console.log("Matches for 'a{2,}':", text.match(patternAtLeast));
```
- /a{2,4}/g: This regex matches between 2 and 4 occurrences of "a". It finds "aa", "aaa", and "aaaa".

```// {n,m} (Between 'n' and 'm') - Matches between 'n' and 'm' occurrences
const patternBetween = /a{2,4}/g;
console.log("Matches for 'a{2,4}':", text.match(patternBetween));
```

### OR Operator
- OR operator ( | ) is used to match one pattern or another. It allows you to specify multiple alternative patterns, where the regex will match if any one of them is found.

Example text: const text = "I have a cat and a dog.";

- /cat|dog/g: This regex matches either "cat" or "dog". The g flag (global) ensures all occurrences in the text are matched. In the example, it finds "cat" and "dog" in the text "I have a cat and a dog."

```// cat|dog - Matches either "cat" or "dog"
const patternOr = /cat|dog/g;
const matchesOr = text.match(patternOr);
console.log("Matches for 'cat|dog':", matchesOr);
```
- /apple|orange|banana/g: This regex matches "apple", "orange", or "banana". It finds all three fruits in the text "I like apple, orange, and banana." 

```// apple|orange|banana - Matches "apple", "orange", or "banana"
const text2 = "I like apple, orange, and banana.";
const patternMultipleOr = /apple|orange|banana/g;
const matchesMultipleOr = text2.match(patternMultipleOr);
console.log("Matches for 'apple|orange|banana':", matchesMultipleOr);
```
- /cat|dog|fish/g: This regex matches "cat", "dog", or "fish". It finds "cat", "dog", and "fish" in the text "My cat and dog are friends with a fish."

```// cat|dog|fish - Matches "cat", "dog", or "fish"
const text3 = "My cat and dog are friends with a fish.";
const patternThreeOptions = /cat|dog|fish/g;
const matchesThreeOptions = text3.match(patternThreeOptions);
console.log("Matches for 'cat|dog|fish':", matchesThreeOptions);
```
- /red|blue|green/g: This regex matches "red", "blue", or "green". It finds all these colors in the text "The color is red or blue or green."

```// The OR operator can also be used with other patterns
const text4 = "The color is red or blue or green.";
const patternColors = /red|blue|green/g;
const matchesColors = text4.match(patternColors);
console.log("Matches for 'red|blue|green':", matchesColors);
```

### Character Classes
- Character classes are used to define a set of characters that you want to match. They provide a way to specify a range or a collection of characters that a single character in the input text should match.

Example: const text = "Sample text: 123, a-z, A_B, !@#";

- /[abc]/g: This regex matches any one character that is either 'a', 'b', or 'c'. The g flag ensures all occurrences are matched.

```// [abc] - Matches any one of the characters 'a', 'b', or 'c'
const patternClass = /[abc]/g;
const matchesClass = text.match(patternClass);
console.log("Matches for '[abc]':", matchesClass);
```
- /[^abc]/g: This regex matches any character that is not 'a', 'b', or 'c'. The g flag allows matching all such characters in the text.

```// [^abc] - Matches any character except 'a', 'b', or 'c'
const patternNegatedClass = /[^abc]/g;
const matchesNegatedClass = text.match(patternNegatedClass);
console.log("Matches for '[^abc]':", matchesNegatedClass);
```
- /[a-z]/g: This regex matches any lowercase letter from 'a' to 'z'. It will find all lowercase letters in the text.

```// [a-z] - Matches any lowercase letter from 'a' to 'z'
const patternRange = /[a-z]/g;
const matchesRange = text.match(patternRange);
console.log("Matches for '[a-z]':", matchesRange);
```
- /\d/g: This regex matches any digit (0-9). It finds all digits in the text.

```// \d - Matches any digit
const patternDigit = /\d/g;
const matchesDigit = text.match(patternDigit);
console.log("Matches for '\\d':", matchesDigit);
```
- /\D/g: This regex matches any character that is not a digit. It will find all non-digit characters in the text.

```// \D - Matches any non-digit character
const patternNonDigit = /\D/g;
const matchesNonDigit = text.match(patternNonDigit);
console.log("Matches for '\\D':", matchesNonDigit);
```
- /\w/g: This regex matches any word character (alphanumeric characters plus underscore). It finds all word characters in the text.

```// \w - Matches any word character (alphanumeric plus underscore)
const patternWord = /\w/g;
const matchesWord = text.match(patternWord);
console.log("Matches for '\\w':", matchesWord);
```
- /\W/g: This regex matches any non-word character. It will find all characters that are not alphanumeric or underscore.

```// \W - Matches any non-word character
const patternNonWord = /\W/g;
const matchesNonWord = text.match(patternNonWord);
console.log("Matches for '\\W':", matchesNonWord);
```
- /\s/g: This regex matches any whitespace character (such as space, tab, newline). It finds all whitespace characters in the text.

```// \s - Matches any whitespace character
const patternWhitespace = /\s/g;
const matchesWhitespace = text.match(patternWhitespace);
console.log("Matches for '\\s':", matchesWhitespace);
```
- /\S/g: This regex matches any non-whitespace character. It will find all characters that are not spaces, tabs, or newlines.

```// \S - Matches any non-whitespace character
const patternNonWhitespace = /\S/g;
const matchesNonWhitespace = text.match(patternNonWhitespace);
console.log("Matches for '\\S':", matchesNonWhitespace);
```

### Flags
- Flags (or modifiers) are special characters that you can add to a regular expression to change its behavior. They help control aspects like case sensitivity, global matching, and more.

Example: const text = "Hello world!\nHello Universe!";

- /Hello/g: The g flag makes the regex match all occurrences of "Hello" in the text. Without the g flag, it would only find the first occurrence.

```// g (Global) - Matches all occurrences of the pattern
const patternGlobal = /Hello/g;
const matchesGlobal = text.match(patternGlobal);
console.log("Matches for 'Hello' with 'g' flag:", matchesGlobal);
```
- /hello/i: The i flag makes the regex match "hello" regardless of case. It finds "Hello" even though the case doesn't match exactly.

```// i (Case Insensitive) - Matches 'hello' regardless of case
const patternCaseInsensitive = /hello/i;
const matchesCaseInsensitive = text.match(patternCaseInsensitive);
console.log("Matches for 'hello' with 'i' flag:", matchesCaseInsensitive);
```
- /^Hello/m: The m flag allows ^ to match "Hello" at the beginning of each line, not just the start of the whole string. In the text, "Hello" at the beginning of the second line is matched.

```// m (Multiline) - Changes behavior of ^ and $
const patternMultiline = /^Hello/m;
const matchesMultiline = text.match(patternMultiline);
console.log("Matches for '^Hello' with 'm' flag:", matchesMultiline);
```
- /Hello.world!/s: The s flag allows the . to match newline characters. So, this pattern matches "Hello" followed by any characters (including newlines) up to "world!".

```// s (Dot All) - Makes . match newline characters
const patternDotAll = /Hello.world!/s;
const matchesDotAll = text.match(patternDotAll);
console.log("Matches for 'Hello.world!' with 's' flag:", matchesDotAll);
```
- /\u{1F600}/u: The u flag allows matching Unicode characters beyond the basic multilingual plane. Here, it matches the 😀 emoji in the text.

```// u (Unicode) - Matches Unicode characters
const patternUnicode = /\u{1F600}/u; // Unicode for 😀
const textUnicode = "😀";
const matchesUnicode = textUnicode.match(patternUnicode);
console.log("Matches for Unicode character with 'u' flag:", matchesUnicode);
```
- /Hello/y: The y flag makes the regex match "Hello" only if it starts exactly at the current position (lastIndex). By setting lastIndex to 13, the regex matches "Hello" starting from the 14th character of the text.

```// y (Sticky) - Matches only from the current position
const patternSticky = /Hello/y;
const stickyRegex = new RegExp(patternSticky, 'y');
stickyRegex.lastIndex = 13; // Set the position in the string to start matching
const matchesSticky = stickyRegex.exec(text);
console.log("Matches for 'Hello' with 'y' flag:", matchesSticky);
```

### Grouping and Capturing
- Grouping and capturing are techniques used to extract parts of a matched string and to apply quantifiers to multiple characters at once.

Example: const text = "John Doe, Jane Smith, Bob Johnson";

- /(\w+)\s(\w+)/g:
    - (\w+): Captures one or more word characters (first name).
    - \s: Matches a whitespace character (space).
    - (\w+): Captures one or more word characters (surname).
    - match[0]: Full match (e.g., "John Doe").
    - match[1]: First capture group (e.g., "John").
    - match[2]: Second capture group (e.g., "Doe").

```// Grouping and Capturing
// (John|Jane|Bob) captures the name part and (\w+) captures the surname
const patternCapture = /(\w+)\s(\w+)/g;
let match;
console.log("Capturing groups:");
while ((match = patternCapture.exec(text)) !== null) {
    console.log(`Full match: ${match[0]}`);
    console.log(`First name (Group 1): ${match[1]}`);
    console.log(`Surname (Group 2): ${match[2]}`);
}
```
- /(?:John|Jane|Bob)\s(\w+)/g:
    - (?:John|Jane|Bob): Non-capturing group that matches one of the names.
    - \s(\w+): Captures the surname.
    - This pattern matches the names and surnames but only captures the surnames.

```// Non-Capturing Groups
// (?:John|Jane|Bob) matches names without capturing
const patternNonCapture = /(?:John|Jane|Bob)\s(\w+)/g;
const matchesNonCapture = text.match(patternNonCapture);
console.log("\nNon-Capturing groups:");
console.log("Matches:", matchesNonCapture);
```
- /(\w+)@(\w+)\.(\w+)|(\d{3})-(\d{4})/g:

    - (\w+)@(\w+)\.(\w+): Captures email parts:
        - (\w+): Username.
        - @(\w+): Domain.
        - \.(\w+): Top-level domain.
    - (\d{3})-(\d{4}): Captures phone number parts:
        - (\d{3}): Area code.
        - -(\d{4}): Number.
    - match2[0]: Full match (e.g., "user@example.com" or "555-1234").
    - match2[1], match2[2], match2[3]: Email parts.
    - match2[4], match2[5]: Phone number parts.

```// Example with multiple capture groups
const text2 = "My email is user@example.com and my phone number is 555-1234.";
const patternEmailPhone = /(\w+)@(\w+)\.(\w+)|(\d{3})-(\d{4})/g;
let match2;
console.log("\nMultiple Capture Groups:");
while ((match2 = patternEmailPhone.exec(text2)) !== null) {
    console.log(`Full match: ${match2[0]}`);
    console.log(`Email Username (Group 1): ${match2[1]}`);
    console.log(`Email Domain (Group 2): ${match2[2]}`);
    console.log(`Email Top-Level Domain (Group 3): ${match2[3]}`);
    console.log(`Phone Area Code (Group 4): ${match2[4]}`);
    console.log(`Phone Number (Group 5): ${match2[5]}`);
}
```

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)