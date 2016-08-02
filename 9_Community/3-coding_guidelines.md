#Coding guidelines
These is a set of coding guidelines which are mandatory to follow when contributing to ARToolKit. The guidelines main objective is source code formatting consistence and to optimize code readability. To this end, source code files should always be treated as a formal document.

##Indentation
ARToolKit uses 4 spaces for indentation, not tabs.

_2-space indentation is too little for the casual observer to correctly infer level of nesting; it leads quickly to errors of logic in complex nested sections. 8-space indentation is overkill and leads to much horizontal scrolling. We use spaces rather than tabs because it leads to consistent code across editors, and it’s the default for most modern IDEs._

##Braces
ARToolKit uses the “one true brace” variant of K&R braces for both C and C++. (see [https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS](https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS) for details)

It simply means write your curly bracket source code like this:
```
if (x < 0) {
    puts("Negative");
    negative(x);
} else {
    puts("Non-negative");
    nonnegative(x);
}
```
And always used brackets even if the statement contains only one line of code:
```
if (x < 0) {
    negative(x);
} else {
    nonnegative(x);
}
```
_Unlike Stroustrup or Allman style, 1TBS groups the logical start and end of control blocks with the actual logic statements that produce the control inflection. Also, it’s more compact._

##Spacing
Use a space after (most) keywords. 
The notable exceptions are sizeof, typeof, alignof, and __attribute__, which look somewhat like functions.

Use a space after these keywords:

> if | switch | case | for | do | while

but not with:

> sizeof | typeof | alignof | \__attribute__

Example:
```
s = sizeof(struct file);
```
###Parenthesized expressions
Do not add spaces around parenthesized expressions.
```
s = sizeof( struct file ); // DON’T
```
If editing legacy ARToolKit code which violates this, feel free to update it. For example this line:
```
if( flag ) {
```
should be updated to:
```
if (flag) {
```
###Pointer declaration using C
When declaring pointer data or a function that returns a pointer type, the preferred use of '*' is adjacent to the data name or function name and not adjacent to the type name. 
Examples:
```
char *message;
unsigned long long memparse(char *ptr, char **retptr);
char *match_strdup(substring_t *s);
```
###Pointer declaration using C++
For **C++** code however, generally the ‘*’ groups to the left:
```
std::string* s;
```

###Unary, binary and ternary operators
Use one space **on each side of** most binary and ternary operators, such as any of these:

> = + - < > * / % | & ^ <= >= == != ? :

(If it improves readability, you can remove the spaces on either side of * and / operators.)

But no space after unary operators:

> ++ \-\- & * + - ~ ! sizeof typeof alignof \__attribute__ defined

Example:

 - Increment: `++x, x++` 
 - Decrement: `−−x, x−−` 
 - Address: `&x`
 - Indirection: `*x` 
 - Positive: `+x` 
 - Negative: `−x` 
 - Ones' complement: `~x` 
 - Logical negation: `!x` 
 - Sizeof: `sizeof x, sizeof(type-name)`
 - Cast: `(type-name) cast-expression`

###Structure member operators
No space around the '.' and "->" structure member operators.

##Comments
For block comments, pick either // or /* */ and stick with it in that file. For trailing comments, use //.

Finish comments with a full stop/period.

_Especially when a comment extends off the right-edge of the visible area, a full stop/period helps the reader know whether they’ve seen the whole comment._

##Functions
Functions are not just for readability; they represent a logically distinct unit of execution. If a function consists of a long series of operations that must be performed together, and in a defined order, then there is no reason to break up that function into smaller units, unless those smaller units would also be reusable in some other context outside of the parent function.

##Other C++ style
Refer to the very well thought-out [Google C++ style guide](https://google.github.io/styleguide/cppguide.html) except where it conflicts with the above guidance.

##Other Java style
Refer to the Android [Code Style for Contributors](http://source.android.com/source/code-style.html) except where it conflicts with the above guidance.

    
