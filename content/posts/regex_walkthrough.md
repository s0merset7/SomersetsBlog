---
title: "Making Regex Rules in Semgrep"
description: ""
date: 2021-07-12T07:18:20-07:00
lastmod: 2020-07-12T07:18:20-07:00
cover: ""
coverAlt: ""
toc: false
tags: ["Semgrep"]
draft: false
---
<style>
	main {
    margin: 90px auto;
    padding: 0 15px;
    max-width: 70%;
	}
</style>

One feature of Semgrep is the ability to use regular expressions (regex) in your rule making. In the [previous post](/posts/semgrep_intro/semgrepnotes/) we discussed what Semgrep is and how to use it, here we will be focusing specifically on how to use Semgrep in conjunction with regex as it can get complicated

## Setup
Make sure you have a good understanding of how to use Semgrep, especially with creating your own custom YAML rules
### Helpful Resources
While creating your regex rules, it is helpful to have an area to test and experiment with different patterns. To do so, you can check out either:
- [Semgrep Playground](https://semgrep.dev/editor) - where you can test custom Semgrep YAML rules agaisnt custom code
- [Regex Playground](https://regex101.com/) - where you can test specific regex patterns against custom datasets, in the upper right hand side it will even provide an explanation as to why it is matching certian cases
    - Please note that the compiler used on this site is not the same that Semgrep uses so there may be some small discrepencies between platforms

### Semgrep YAML Rule Template
The following is a template for a Semgrep YAML regex rule that you can use as a basis:
```
rules:
    - id: name-of-regex-rule
        patterns:
        - pattern-regex: regex_pattern_here
        message: Write your message here
        languages: [regex]
        severity: SEVERITYLEVEL
```
- Keep in mind that `pattern-regex` is only one of five different regex pattern options. To learn about the other four, [click here](/posts/semgrep_intro/semgrepnotes/#regex-patterns)


## Example Walkthrough
For the following example, we will be trying to create a regex pattern that will match all four of these secret keys:
- PASSWORD(secret_key0:"qwertyuiopas")
- PASSWORD(SECRET_KEY1:'qwert92iop674')
- PASSWORD(secretkey2:\`QweRt92iopD2Fr4`)
- PASSWORD(SECRETkey3:QweRt92iD2Fr4)

To do so, we will answer four different questions and by the end, have our pattern ready to throw into Semgrep
- The following examples will use the `#` chracter as a placeholder for a part of the pattern that has not been addressed yet

### 1. Is there any part that won't change between iterations?
If we look at each iteration of our secret keys, we can see that the begining `PASSWORD()` along with the middle `:` are present in the same location. While alphanumeric characters can be used exactly as they appear within your regex rules, special characters must be treated differently
#### Special characters are reserved characters in regex
There are many reserved characters in regex patternsm, so many that almost every special character is also a reserved character. Meaning that if you want to match a special character, you must preceed it with a forward slash `\`
- Example Pattern: `PASSWORD\(####\:####\)` - see it in action [here](https://regex101.com/r/I3kps1/1/)

### 2. Is there any part that is very similar between iterations?
Each iteration has the words "secret" and "key" in them, however they are both uppercase and lowercase, as well as sometimes separated with an underscore, and othertimes not. To get around these two types of variations, we need to introduce two new regex patterns:
#### Case variations
If we know our pattern will be the same but changing upper vs. lower case, we can preceed that part with `(?i)` to indicate we want to ignore the case
- Example Pattern: `PASSWORD\((?i)secret#(?i)key\:####\)` - see it in action [here](https://regex101.com/r/brTBsG/1)
#### Off by a few chracters
When the the presence of a character changes, we can follow that character with a `?` to indicate that this character may be here OR not
follow character by `?` to say it doesnt matter
- Example Pattern:`PASSWORD\((?i)secret_?(?i)key\:####\)` - see it in action [here](https://regex101.com/r/3JVdKV/1)

### 3. Is there something that is often different but in the same part?
Often times there will be a part of a pattern that will change, but have a limited number of variations it could be. In our case, at the beginning and the end of each key, there is either a `"`, `'`, `` ` ``, or none. To account for all of these variations we need to use an OR parameter
#### How to use OR
To use the OR parameter, simply separate your different variations with a `|` and surround them all with `[]` like this
- `[Char1|Char1|Char3]`
We can also add the `?` at the end to indicate it could be one of these options OR none
- Example Pattern: ``PASSWORD\((?i)secret_?(?i)key\:["|'|`]?####["|'|`]?\)`` - see it in action [here](https://regex101.com/r/jSO4Xq/1)

### 4. Is there a part that can include a range of potential characters?
Finally, we notice that in each iteration, there is something that is entirely different each time, the key number and the key value itself. Once we identify some key features about what these values can be (the key number is a one digit numeric value while the key value is a 12 to 15 character alphanumeric string) we can create patterns around them
- For common broad catagories, you can use the following
    - `\d` - digit character (0-9)
    - `\w` - word character (alphanumeric and underscores)
    - `\s` - whitespace chracters (tabs/linespaces)
    - `.` - any character
- to indicate a specific range of potential characters use `[]` with the specific characters
    - `0-9` for numbers
    - `a-z` for lowercase alphabet
    - `A-Z` for uppercase alphabet
    - can also use individual special characters
- to indicate a range of expected characters, append the pattern with a `{#,#}`
- Pattern Example: ``PASSWORD\((?i)secret_?(?i)key\d{1}\:["|'|`]?[0-9a-zA-Z]{12,15}["|'|`]?\)``

This brings us to our final YAML rule of: [(check it out in action here)](https://semgrep.dev/s/s0merset7:regex_pattern_matching)
```
rules:
  - id: detect-secret-keys
    languages:
      - regex
    message: Secret Key Detected
    pattern-regex: PASSWORD\((?i)secret_?(?i)key\d{1}\:["|'|`]?[0-9a-zA-Z]{12,15}["|'|`]?\)
    severity: ERROR
```

## Summary

1. Is there any part that won't change between iterations?
    <br><div style="padding-left: 2em;">[ ] You can copy the unchanged parts as is in your Semgrep pattern
    <br>[ ] Special characters must be preceded by `\` </div>

2. Is there any part that is very similar between iterations?
    <br><div style="padding-left: 2em;">[ ] Preceed a part with `(?i)` to ignore case
    <br>[ ] Follow a chracter with `?` when it may OR may not be present </div>
3. Is there something that is often different but in the same part?
    <br><div style="padding-left: 2em;">[ ] Put different possibilities of a part in an OR parameter `[Char1|Char1|Char3]` </div>
4. Is there a part that can include a range of potential characters?
    <br><div style="padding-left: 2em;">[ ] For common broad catagories, you can use the following
        <br><div style="padding-left: 2em;">[ ] `\d` - digit character (0-9)
        <br>[ ] `\w` - word character (alphanumeric and underscores)
        <br>[ ] `\s` - whitespace chracters (tabs/linespaces)
        <br>[ ] `.` - any character</div>
    <br>[ ] to indicate a specific range of potential characters use `[]` with the specific characters
        <br><div style="padding-left: 2em;">[ ] `0-9` for numbers
        <br>[ ] `a-z` for lowercase alphabet
        <br>[ ] `A-Z` for uppercase alphabet
        <br>[ ] can also use individual special characters</div>
    <br>[ ] to indicate a range of expected characters, append the pattern with a `{#,#}`</div>

    ## Sources
    - [Regex Tutorial by Jonny Fox](https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285)
    - [Regex Playground](https://regex101.com/)
    - [Semgrep Regex Documentation](https://semgrep.dev/docs/writing-rules/rule-syntax/#pattern-regex)