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