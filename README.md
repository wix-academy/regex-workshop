# Regex Workshop

In this workshop we will learn how to write Regular Expressions to match many different patterns.

<img src="https://camo.githubusercontent.com/c5026835dcc420687befac8b349fb810c8cdfd4b7c9601d63b44b465561e55dc/687474703a2f2f696d67732e786b63642e636f6d2f636f6d6963732f726567756c61725f65787072657373696f6e732e706e67" alt="" width="300" />

## Setup

The Workshop can be done in either Javscript or Scala, the differences are very minor so pick what best suites you.

Choose one:
* [Javascript Setup](./javascript-setup.md)
* [Scala Setup](./scala-setup.md)

***After you finish and understand the setup we can begin.***

## Step 1 - Intro

A regular expression is a pattern used to check if a given text matches it.

Most languages have similar patterns for Regex.

In **Javascript** we write our Regex between two slashes `//` or by using the `RegExp` object, we will stick with the slash notation.

**Example:** `/w/` is a regular expression that matches all words containing the letter `w`

In **Scala** we write the pattern as a regular String and then run `.r` on the string (our test does that for us, so we just need to write a simple string)

**Example:** `"w"` is the pattern used for a regular expression that matches all words containing the letter `w`

**Step 1 Challenge: Write a Regular Expression that checks if the given text contains the letter `a`.**

> In the `Solution` file write your answer in the `answer1` variable.

### reminder
**Javascript:** In order to check that you are correct run `npm t 1` or `npm run test:watch 1` in the terminal in this project root.

**Scala:** run `Test.scala` and use `Program arguments` in order to filter for the current step, `"1"`.

## Step 2 - Anchors

In order to check that a given text starts with a specific pattern we can use the `^` character and in order to check if it ends with a specific pattern we can use the `$` character - these are called *Anchors*.

`\b` is another Anchor that can be used to check if the pattern is at the end of a word.

**Example:** `"ick$"` is a regular expression that only matches a given text if it has the letters `i` `c` `k` in that order and then the text immediately ends. So for the text `"Pickle Rick"` since it ends with `ick` it matched our Regex. For the text `"Rick and Morty"`, although it contains the pattern `ick`, it doesn't end with it, so it does not match the pattern.

**Step 2 Challenge: Write a Regular Expression that checks if the given text starts with the letter `m`.**

> In the `Solution` file write your answer in the `answer2` variable and run step 2 tests.

## Step 3 - Character Classes

In the world of Regular Expression there are **Character Classes** that can be used to match characters from specific sets.

* `\d` matches any of the 10 digits [`0`, `1`..., `9`]
* `\w` matches any of the letters of the english Alphabet uppercase & lowercase, digit or `_`
* `\s` matches any whitespace [' ', '\n', '\t'...]
* `.` matches any character except line breaks

[Read more about Character Classes here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes)

**Example:** `"\d\d"` is a regular expression that only matches a given text if it has two digits in a row. So for the text `"The answer is 42!"` since it contains two digits in a row (`4` and `2`) it matches our Regex. For the text `"1+1=2"`, although it contains two digits, since they are not in a row the regex doesn't match.

**Step 3 Challenge: Write a Regular Expression that checks if the given text ends with any digit.**

> In the `Solution` file write your answer in the `answer3` variable and run step 3 tests.

## Step 4 - Quantifiers

Sometimes we want to check if a pattern is repeating a cretain amount of times or between a min and max amount of times, for that we use the `{min,max}` pattern also known as **Quantifiers**. So, `{2,4}` would check that the preceding pattern is at least of length 2 (inclusive) and at most length 4 (inclusive).

**Example:** `"a{3,6}"` is a regular expression that only matches a given text if it has 3-6 `a`'s in a row. So the text `"Blah Blah Blaaah!"` matches since it contains `"aaa"`. On the other hand `"Blah Blah Blah!"` doesn't match since it doesn't contain more than one `a` in a row .

If we only care about the min we can do so by removing the max (but leaving the comma), so `"a{7,}"` checks that there are 7 `a`'s in a row at least. If we want an exact number of occurrences we remove the comma to, so `"a{5}"` checks that there are 5 `a`'s in a row exactly.

* For `a{0,}` there is a shorthand using a `*` which means any amount of the preceding pattern.
* For `a{1,}` there is a shorthand using a `+` which means one or more of the preceding pattern.
* For `a{0,1}` there is a shorthand using a `?` which means zero or one of the preceding pattern.

**Example:** `"^a+c*b+$"` is a regular expression that only matches a given text if it begins with one or more `a`'s immediately followed by any number of `c`'s (including zero) and then immediately followed and ending by one or more `b`'s. Texts that match the pattern would be `"ab", "aaaaaaaaaccccbbb", "acccccccccccccbbb"...`. Text that don't match would be `"abc"` (`c`'s must come before `b`'s), `"ac"` (must have at least one `b`), `"cccccccbbbbbbb"` (must have at least one `a`).

**Step 4 Challenge: Write a Regular Expression that checks if the given text contains a valid telephone number. A valid telephone number:**
1. **always starts with a zero**
2. **has dashes after the first three digits and the next three digits**
3. **has 10 digits altogether**

**an example of a valid telephone number is `052-123-1234`**.

> In the `Solution` file write your answer in the `answer4` variable and run step 4 tests.

## Step 5 - Alternations

If we have several patterns we want to match we can use the pipe `|` to match the different patterns, this is known as an **Alternation**.

**Example:** `"Mr Meseeks|Look at me"` will match any text that contains `Mr Meseeks` **or** contains `Look at me`.

In order to add an Alternation for only a small pattern within the regex we can use grouping (which we will elaborate on its awesome powers in the following steps) by wrapping our pattern in parentheses `()`.

**Example:** `"^b(o|ar)b$"` will match only two texts `"bob"` and `"barb"`, the beginning `b` and the ending `b` are not part of the Alternation since only the `o|ar` are in the group.

**Step 5 Challenge: Write a Regular Expression that checks if the given text contains a reference to guy varzager or guy segev, in order to shorten the regex you can use a group**

> In the `Solution` file write your answer in the `answer5` variable and run step 5 tests.

## Step 6 - Character Set

In order to match any of several different charcters we can use Alternations `a|b|c|d|e` but a better way to do this would be to use a **Character Set**. `[abcde]` matches any of the letters within the Set `a`, `b`, `c`, `d` or `e`.

* `[a-g]` is shorthand for writing all the letters between `a` and `g`.
* `[a-z]` is how we would match any lowercase character and `[A-Z]` any uppercase character.
* `[a-zA-Z0-9_]` is the equivalent of using the `\w` Character Class that we saw in step 3.

**Example:** `"[a-eA-E]"` will match any text that contains any of the letters between `a` and `e` uppercase or lowercase. So it would match `"A zoo"` (because of the `A`) but wouldn't match `"this zoo"` (since it has none of the letters between `a` and `e`).

**Step 6 Challenge: Write a Regular Expression that only matches a word (containing uppercase and lowercase letters only) of length of at least 3 and at most 10 or a valid number of length 3 (valid numbers have no leading zeros)** 

> In the `Solution` file write your answer in the `answer6` variable and run step 6 tests.

## Step 7 - Flags

Patterns can have **Flags** attached to them in order to alter the way the match is calculated.

In **Javascript** flags are appended after the last slash. Each flag is one letter added to the end of the regular expression, so to use the `m` flag we would write `/a|b/m`. We can also append several for example `/a|b/gms`

In **Scala** flags are appended to the start of the pattern. Each flag is one letter, so to use the `m` flag we would write `"(?m)a|b"`. We can also append several for example `"(?gms)a|b"`.

Some available flags:

* `i` - case-insensitive pattern matching
* `g` - greedy matching, will return all matches and not just the first
* `m` - multiline mode, changes `^` and `$` to match the beginning and ending of a line and not just of the entire text
* `s` - Makes the `.` Character Class match all characters including `\n`

[read more about flags](https://www.codeguage.com/courses/regexp/flags)

**Example:** `/^m.m$/s` for Javascript or `"(?s)^m.m$"` for Scala matches `"mom", "mam", "mem", "m m", "m%m", "m\nm"`. notice that `^m.m$` (without the `s` flag) matches everything but `"m\nm"`.

**Step 7 Challenge: Write a Regular Expression that only matches text containing a line that begins with `x` or `X` and ends with `q` or `Q` and all other characters in the line are `c` or `C`**

> In the `Solution` file write your answer in the `answer7` variable and run step 7 tests.

## Step 8 - Negative Character Set

In order to not match a set of characters we can use a **Negative Character Set**. This can be done by adding a `^` in the beginning of a Character Set. `[^abc]` means any character that is not `a`, `b` or `c`.

**Example:** `"^a[^0-9]c$"` matches `"abc", "a+c", "a|c", "axc", "aac", "a{c"` but doesn't match `"a0c", "a1c"...`.

**Step 8 Challenge: (Moderate) Write a Regular Expression that only matches text that contain a sequence of `g`'s that has an even amount, but is not within a sequence of odd amount of `g`'s. Clarification Example: `"ggg"` although it contains `gg` which is an even amount of `g`'s it is contained within a three `g` sequence so shouldn't match**

> In the `Solution` file write your answer in the `answer8` variable and run step 8 tests.

## Step 9 - Capture Groups

We began discussing groups in Step 5 and here we will see one of its superpowers.

When wrapping a pattern in parentheses we are using what is called a **Capture Group**. A capture group allows us to reference text captured by the group pattern within the regex. In order to use a captured group we use the special syntax `\1`, `\2`... which is a backslash followed by the Capture Group number (they are numbered from left to right starting with 1).

**Example:** `"([0-9])\1"` matches any text that contains two of the same digit in a row. So it would match `"11", "I have to go to the 00", "i have 99 problems, but capturing groups ain't one"` but not `"1 1", "aa"`...

In addition, when using Capture Groups we can also use the captured text outside of the regex (in Javascript by using the `match` function), but this is out of our scope for this workshop. [You can read about this here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match).

If we want to not capture a group, we can use the **Non Capture Group** syntax `(?:a|b)`. This will match `a` or `b` but will not capture the group, so we can't use the `\1` since the group wasn't captured.

**Step 9 Challenge: Write a Regular Expression that only matches text that contain at least three of the same character**

> In the `Solution` file write your answer in the `answer9` variable and run step 9 tests.

## Step 10 - Positive Lookaround

When using patterns to match text we actually "use up" the characters that were matched, and so we can't use them again if we want to check more than one thing on specific characters.

**Example:** if we want to test if the given text matches `a.*0.*2.*b` but also matches `a.*1.*3.*b` we can't do this easily since we don't know where the `0` and `2` are compared to the `1` and `3`. So if we were to write `"a.*0.*2.*1.*3.*b"` we would miss out on texts like `"a0123b"`.

In the previous example, we could have alternated all the different permutations but that would be very long. Our main issue is that once we write `a.*0.*2.*b` we've used up our `a0123b` and can't match it on the second pattern we have.

Positive Lookahead allows you to pattern match without "using up" the characters. Wrapping a pattern with`(?=)` allows us to reuse the matched text in subsequent patterns.

**Example:** in order to match `a.*0.*2.*b` and also match `a.*1.*3.*b` we can do `"(?=a.*0.*2.*b)a.*1.*3.*b"`. This makes sure that the text contains text matching `a.*0.*2.*b` without "using it up" allowing the second match `a.*1.*3.*b` to also return true.

There is also a Positive Lookbehind that works similarly but looking back at characters we already "used up" `(?<=)`.

**Positive Lookaround** is the collective name of Positive Lookahead and Positive Lookbehind.

**Step 10 Challenge: Write a Regular Expression that only matches a number with only odd digits that has at least one 5 digit (this can be done also without Positive Lookahead but would result in a longer regex)**

> In the `Solution` file write your answer in the `answer10` variable and run step 10 tests.

## Step 11 - Negative Lookaround

Similar to Positive Lookahead, Negative Lookahead allows you to check that a pattern **does not** match but doesn't "use up" the characters. Wrapping a pattern with `(?!)` allows to reuse the matching text in subsequent patterns.

**Example:** `"^(?!a\d\dc)a..c$"` matches all text beginning with `a` and ending with `c` with two characters in the middle that the both can't be digits (but each can be separately. This would match `"abbc", "a%!c", "a1bc", "ab1c"..` but not match `"a00c", "a91c"...`.

There is also a Negative Lookbehind that works similarly but looking back at characters we already "used up" `(?<!)`.

**Negative Lookaround** is the collective name of Negative Lookahead and Negative Lookbehind.

[Read more about Positive and Negative Lookbehinds](https://www.regular-expressions.info/lookaround.html)

**Step 11 Challenge: (HARD) Write a Regular Expression that only matches a given text if it doesnt contain the same letter twice in a row**

> In the `Solution` file write your answer in the `answer11` variable and run step 11 tests.

## Step 12 - Password Challenge

Nothing left to teach you :)

**Step 12 Challenge: (Moderate) Write a Regular Expression that only Validates a Password with the following rules**
1. **Has at least one uppercase letter**
2. **Has at least one lowercase letter**
3. **Has at least one digit**
4. **Has at least one special character: @#$!**
4. **Is of length 8 - 16**

## Step 13 - Palindrome

**Step 13 Challenge: (Moderate) Write a Regular Expression that only matches [Palindromes](https://en.wikipedia.org/wiki/Palindrome#:~:text=A%20palindrome%20is%20a%20word,such%20as%20madam%20or%20racecar.) of length 4-5**

## Step 14 - Prime

**Step 14 Challenge: (Super Hard) Write a Regular Expression that checks if a given text contains a sequence of x's that is of length that is a prime number**

## Further Challenges

You are now a Regex Master! Congrats!

<img src="https://www.meziantou.net/assets/perl-problems.png?v=f5e3" alt="" />

If you want some more Regex challenges you can look in to the following links: 
* [Regex Golf](https://alf.nu/RegexGolf)
* [Regex Crossword](https://regexcrossword.com/)

Careful! it is addictive.

<img src="https://miro.medium.com/max/1400/1*o2JwtNB7w1nn63nj6z1N9Q.jpeg" alt="" width="400" />
