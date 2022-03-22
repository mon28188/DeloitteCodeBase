# Tab styles/headers/comments/code blocks

---

#### Tab styles 
The indentation between different levels of code is one tab, or 4 characters

```
#!Apex

if (foo == 1) {
    bar = 3;
}
```

#### Headers
The comments in the header of each class file should appear as block comments.

```
#!Apex

/**
 * This is your class description. It shouldn't exceed 120 characters in width.
 * It should describe at a high level why the class exists and little about what
 * it does, but not how it does it.
 * 
 * @author      Your Name (you@deloitte.nl)
 * @created     September 2016
 */
 
```
The content of the comments should be as brief as possible, so there should not be extra information such as TODO's or version revisions. The character "*" should be aligned.
Note: There should be no blank lines between the comment and the class signature the comment belongs to.
 
#### Comments
##### Block comments
Block comments start and end with / and *, such as
```
#!Apex

/* comment */
```
Block comments should only be used for class header and method header. Block comments must be in the following format to allow code documentation to parse them correctly:
One line block comments are not to be used within the code base. Instead, use the above style where the block comment spans 3 lines.

##### Method header comments
The comments in the header of each method should appear as block comments.
```
#!Apex

/**
 * Describe what the method does and not how it does it. Developers will understand what
 * the code is doing, but need some extra information as to why it is here.
 *
 * @param  param1          Parameter 1 description
 * @param  param2          Parameter 1 description
 * @return Description on how the method returns the value.
 */
public String getName( String param1, String param2 ){
     return '';
}
```
The content of the comments should be as brief as possible, so there should not be extra information such as TODO's. The character "*" should be aligned.
Note: There should be no blank lines between the comment and the block of code the comment belongs to.

##### Inline comments

Inline comments are comments with only one line of content, such as:
```
#!Apex

// comment
```
Inline comments should be used inside block statements, such as methods. Multiple lines of inline comments within a method is allowed, such as:
```
#!Apex

// This
// is
// a
// comment
```
In this situation, the markers of each inline comments should line up, such as:
```
#!Apex

public String getName( String param1, String param2 ){
     return '';      // This is a comment
                     // which is lined up
                     // with the line above
}
```

##### Special inline comments
There are few types of special inline comments allowed:
```
#!Apex

// TODO: description on what needs doing US-1234
// FIX: Indicates that there is an issue and something needs to be fixed US-1234
```
* There should always be a space between the "//" marker and the content. * The action words should be in upper case, followed by a colon. * The reference to a user story number is required.

##### HTML tags in comments 
HTML tags are allowed to be used in the block comments. The coding conventions of HTML are also applied in this situation. HTML tags allowed in block comments: * ul * ol * li * b * i * p

##### Annotations in block comments
These annotations are mostly components for documenting tools, such as "param" or "return". The rule for comments is applied.

---

[Home](/wiki/Home.md) - [Coding conventions](/wiki/coding_conventions/coding_conventions.md) - Tab styles/headers/comments/code blocks