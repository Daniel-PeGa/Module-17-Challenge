# Matching a URL -- Regex

A regex, or regular expression, is a sequence of characters that define a specific search pattern. In the following text, you'll learn to understand regular expressions a little better, with the help of our example designed to match a URL.

## Summary

Regular expressions are used to find certain patterns of characters within a string, just like you would on certain input validations. In this case, we're going to be working with the regular expression used to match a URL, which will be used to find the required patterns for a string to be validated as a URL:

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

This is, admittedly, very particular-looking. However, upon further review of the concept of regular expressions, as well as the different components of this regex, you'll leave saying yeah! i know what a regex is and how to identify the patterns that conform a URL!

## Table of Contents
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)

## Regex Components

### Anchors

In our example, we can see two examples of anchors: ^ and $
* ^  --> Means that the string will begin with the characters that succeed it, which in this case is the entire string until the final backslash (/)

* $ --> The money sign is very much just saying that the character pattern that we're looking for in the string is over, so stop looking for more cos theres none :(


### Grouping and Capturing

The more complicated regular expressions get, the more tempting it is to check multiple parts of a string and ensure the search pattern is as accurate as can be, such that the desired result is found. Grouping and capturing are helpful with that and we can see that in our example:
* () --> Parentheses are the primary way of grouping a section of a regex. Each section within a parentheses is known as a subexpression. The way parentheses work is by matching the content within as is. LITERALLY.

(https?:\/\/)

In our example, we are looking for a string that follows the pattern of lowercase letters in the order of "https", referencing a Hypertext Transfer Protocol Secure. 
* ?: --> This one will switch the capturing nature of the parentheses to non-capturing, such that the part that follows (\/\/) will be matched, but not remembered

This will therefore mean that we are looking for a string that follows the pattern of https, followed by a non-capturing sequence of characters which are invalidated by the forward slash, but we will see those in [Character Escapes](#character-escapes).

### Character Escapes

In the first group of our regex, we've already seen the anchor, capturing and non-capturing group, and we will now see the character escape. In our example, we have the forward slash (/) is our escape.
* / --> In a regex, this forward slash escapes a character that would have otherwise be interpreted literally. It basically makes any special characters that preceed it loose their special significance.

### Character Classes

Character classes define a set of elements, any one of which can occur in an input string to fulfill a match. That is to say, a character class is some kind of filter the search is going to go through to see if it matches. It's probably still confusing, so let me explain with an example from our URL matching excercise:

```
([\da-z\.-]+)
```
This is our second capturing group of the regex, and looks kind of funky not going to lie, but It will make sense once I explan the character classes within and the work they're doing for us during the pattern seach.

* \d --> This character class will match with any Arabic, numerical digit (0-9)

* a-z --> This, as well as the previous expression, are captured inside bracket expressions. For now all you need to know is this expression will search for any letter on the alphabet from a-z, but I'll explain the rest in the [bracket expressions](#bracket-expressions) section.

In regular expressions, you can also set the pattern search such that special characters are being looked for, and it's simpler than it might seem after considering how awful it looks just for digit or alphabetical search. The curious reason we can add special characters in the regular expression to be searched for is that we place them inside the square brackets "[]" and once something is inside them they loose their special significance. In the previous expression we see [\\.-] which means the string being seen in this situation can have a forward slash (\\), a period (.), or a dash (-).

Just as the [\d] is a shorthand character class for (0-9), there's another one we can notice in our regular expression...

* \w --> This one is called the word character, and its pretty cool because it matches [A-Za-z0-9_], and that's so much less to write.

### Quantifiers

In our URL-matching expression we can see some quantifiers. Their purpose is to set the limits of the string being seen by the regex (or to an ndividual section of it). A detile worth pointing out about quantifiers is their greedy nature, since they will attempt a match with as many occurences of particular patterns. The ones in our expression are: 

* [+] --> This quantifier will match the pattern one or more times

* ? --> This one will match the pattern zero or one time, and the engine will make as many attempts as possible to match it. However, were the regex to fail by the previous token not being present, the engine will ignore the part the question mark is working for.

```
(https?:\/\/)?
```
In our regular expression designed to match an URL, we see at the very begining the question mark, meaning it will try to match a pattern of litterally http, and the s, which stands for securing the protocol, but not all Hypertext Transfer Protocols are seccured, so we make the s optional. Further, the entire groping is optional, because the user might type, for example, google.com instead of https://google.com.

Another quantifier that has not yet being mentioned is the curly braces "{}". Their wrok is to match the pattern in question a specific number of times, meaning the string being searched can have only certain amount of characters, or is within a certain range of characters. 

``` 
\.([a-z\.]{2,6}) 
```

In this part of the expression, we see there's a limit in the number of characters you can have following the period on the URL match search. This is no more than putting a limit on the number of characters that can be after the website's name. The .com, .net, .co, etc, have only so many characters, and we want the regex to be aware of it, so there can be only from 2 to 6 characters there.

Another quantifier seen in our regex is:

* [*] --> The asterisc!! It's function is to say that the previous token can happen more than once and can be followed by the same thing multiple times. What was that? Let's check our regex:

```
([\/\w \.-]*)*\/?$/
```

The first asterisc is saying that the string can contain forward slash (/), the word character (\w), and the two special characters (. and -), and can be repeated a number of times. The second one allows for the previous grouping to be repeated any number of times. 

### Bracket Expressions

Throughout our URL-matching regex we see the square brackets ([]) time and again, soooooooooo, what do they do?? Well, the square brackets represent a range of characters that we want to match in our search. We often see in the regular expressions' bracket expressions special characters, and the brackets do an amazing job at making it easy for us. The special significance of special characters is lost when inside the square brackets.

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
