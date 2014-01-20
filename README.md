To aid in maintaining consistency across formatting, naming, logic structure, and internal documentation style, the following guidelines should be adhered to when contributing to or working on any AMX Australia and New Zealand NetLinx code.

## Layout and Formatting

### Tab Stops
Tab stops should be set at 4 characters. Tab stops should use the tab character. Do not use spaces.

### Column Width
Column width is to be set to 80 characters. As a guideline lines should not exceed this width unless there is a marked improvement to code readability.

### Indentation
Each level of indentation is to be the same width as a single TAB character. Although indentation does not affect logic structure within the NetLinx language, it is imperative that this is maintained for code readability.

### Spaces
Where possible, excess whitespace should be avoided. The exception to this is where it provides a logical separation between values.

A space never follows another space except in strings or comments.

No space follows an opening bracket, `(` or `[`, or precedes a closing bracket, `)` or `]`.

Each brace, `{` or `}`, whether delimiting a code block or the elements of an array, is preceded by a space; a space also follows an opening brace `{`.

Commas `,` and semicolons `;` are always followed by a space; no space precedes them. Colons `:` are not preceded by a space.

Assignments `=`, tests for equality/inequality (`==`, `>`, ...), binary operators (`+`, `&&`, ...) are all preceded and followed by a space.

Unary operators (`++`, `--`, `!`) are not separated from their operands.

No space precedes the opening bracket of an array index `[`, or the opening bracket `(` of a method argument argument list, either in declaration or invocation.

#### Examples

##### For Loops

	integer i;
	for (i = 0; i < 10; i++)
	{
	    fooBar(i * 10, 'abc');
	}

##### String Concatenation

	char[] x = "'foo', $20, 'bar'";

##### Functions

	define_function fooBar(integer i, char c[])
	{
	    ....
	}

and when calling

	fooBar(i * 10, 'abc');


### Brace Placement

All bacing is to follow the 'Allman' style. This style puts the brace associated with a control statement on the next line, indented to the same level as the control statement. Statements within the braces are indented to the next level.

If braces can be used, they should always be placed. For example, do *not* do the following:

	if (a > b)
	    fooBar(c);

instead opt for

	if (a > b)
	{
	    foobar(c);
	}

This style ensure that indented code is clearly set apart from the containing statement. Additionally, it assists in that commenting out the control statement, removing the control statement entirely, refactoring, or removing of the block of code is less likely to introduce syntax errors because of dangling or missing braces.

#### Examples

##### Functions

	define_function char fooBar (integer i, char c)
	{
	    ...
	}

##### Event Handlers

	button_event[device, 0]
	{
	
	    push:
	    {
	        ...
	    }
	    
	    release:
	    {
	        ...
	    }
	    
	}

##### Nestable Blocks

	if (a > b)
	{
	    ...
	}


### Line Breaks

#### Conditional Statements
Conditional statements should always split the condition and the action into separate lines. For example

	if (a == b)
	{
	    fooBar(c);
	}
	
should be used instead of

	if (a == b) fooBar(c);

#### Complex Conditionals
For complex conditionals which expand beyond the defined column width each condition is to be placed on a new line and the line indented by a TAB character further than the parent.

	define_function fooBar()
	{
	    ...
	    if (a > b &&
	        a <= c &&
	        a <> d)
	    {
	        ...
	    }
	    ...
	}

#### Argument Lists
If a function requires an extended argument list which causes the invocation to expand beyond the defined column width, arguments should wrap to the next line with one argument per line and be indented by two tab characters beyond the current level of indentation.

	uberFooBar(a,
	        b, 
	        c,
	        d,
	        e,
	        f);
	        
If the arguments can fit within the column width they invocation should be written as a single line.

	fooBar(a, b);

#### Array Assignment
As with argument lists and complex conditions if the length exceeds one line elements are to be wrapped, with one per line.

	char uberArray[] =
	{
	    'a',
	    'b',
	    'c',
	    'd',
	    'e',
	    'f'
	};

	char simpleArray[] = {'a', 'b', 'c'};


## Naming, Logic and Higher Techniques

### Function Names
Functions names should attempt to concisely describe its behaviour in such a way a user could infer its intent without consulting documentation. In many cases this may require the use of multiple, joined words. In these situations [CamelCase](http://en.wikipedia.org/wiki/CamelCase) is to be utilised.

For example:

	fooBar();
	getSomeValue();

### Variable Names
Do not use cute names like `thisVariableIsATemporaryCounter`.  Instead it should be called `tmp`, which is much easier to write, and remains easy to understand.

However, descriptive names for global variables are a must. If a global variable named something similar to `foo` is found anywhere in the repository the commit logs will be traced to find the original author of that line. This person will then be tracked down and slapped with a wet fish. Repeatedly.

Encoding the type of a variable into the name (so-called Hungarian notation) is brain damaged - the compiler knows the types and can check those. As with non-descriptive global variables public fish slapping will be held for all violations of this.

Local variable names should be short and to the point.  If you have a loop counter, it may be called `i`, or similar. Calling it `loopCounter` is non-productive, if there is no chance of it being misunderstood. Similarly, `tmp` can be just about any type of variable that is used to hold a temporary value.

### Constants
Constants are to be named using all caps with words separated by underscore characters. For example:

	THIS_IS_A_CONSTANT

### Function Parameter Names
Sticking with the 'lazy programmer approach' of using short names, functions in which the argument type is implied may use a condensed name. For functions requiring multiple arguments, or where the parameter may not be obvious, descriptive names (which adhere to the above variable naming guidelines) should be utilized.

### Line Termination
All statements are to be terminated with a semi-colon (`;`).

## Commenting
Comments are good, but there is also a danger of over-commenting.  Never try to explain *how* your code works in a comment, it is preferred to write the code so that the working is readable without further explanation.

Generally, you want your comments to tell *what* your code does, not *how*. Try to avoid putting comments inside a function body. If the function is so complex that you need to separately comment parts of it, you should consider splitting this into multiple utility functions.  You can make small comments to note or warn about something particularly clever (or ugly), but try to avoid excess.  Instead, put the comments at the head of the function, telling people *what* it does, and possibly *why* it does it.

The preferred style for long (multi-line) comments is:

	/*
	 * This is the preferred style for multi-line
	 * comments. Please use it consistently.
	 *
	 * It is made of a column of asterisks on the left side,
	 * with beginning and ending almost-blank lines.
	 */

To save space you can put a comment on one line:

	/* This comment takes up only one line. */
