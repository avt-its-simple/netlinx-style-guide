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

Do *not* add spaces around (inside) parenthesized expressions. The following is a *bad* example

	fooBar( x )

Use one space around (on each side of) binary operators, such as any of these:

	=  +  -  <  >  *  /  %  |  &  ^  <=  >=  ==  !=
	
but no space before the postfix increment & decrement unary operators:

	++  --

When calling functions, no space should be inserted between the function name and opening parenthesis of the argument list, however arguments should be separated by a comma followed by a single space.

String concatenation should follow the same spacing form as function argument lists described above.

#### Examples

##### For Loops

	integer i;
	for (i = 0; i < 10; i++) {
	    fooBar(i * 10, 'abc');
	}
	
is preferable to

	integer i;
	for ( i = 0 ; i < 10 ; i++ ) {
	    fooBar ( i * 10, 'abc' );
	}

or

	integer i;
	for(i=0;i<10;i++){
	    fooBar(i*10,'abc');
	}

##### String Concatenation

	char[] x = "'foo', $20, 'bar'";

is preferred to

	char[] x="'foo',$20,'bar'";

##### Functions

	fooBar(i * 10, 'abc');

is preferable to

	fooBar ( i * 10 , 'abc');

or

	fooBar(i*10,'abc');

### Line Breaks

#### Conditional Statements
Conditional statements should always split the condition and the action into separate lines. For example

	if (x == y) {
	    fooBar(z);
	}
	
should be used instead of

	if (x == y) fooBar(z);

#### Complex Conditionals
For complex conditionals which expand beyond the defined column width each condition is to be placed on a new line and the line indented by a TAB character further than the parent.

	define_function fooBar() {
	    ...
	    if (x > y &&
	        x <= z &&
	        w <> x) {
	        // Do something
	    }
	    ...
	}

#### Argument Lists
If a function requires an extended argument list which causes the invocation to expand beyond the defined column width, arguments should wrap to the next line and be indented by two tab characters beyond the current level of indentation.

	uberFooBar(arg0, arg1, arg2, arg3,
	        arg4, arg5);
	        
If the arguments can fit within the column width they invocation should be written as a single line.

	fooBar(arg0, arg1);

#### Array Assignment
When assigning a list a values to an array, each entry should appear on its own line:

	char tmp[] = {
	    'a',
	    'b',
	    'c'
	};

rather than

	char tmp[] = {'a', 'b', 'c'};

### Brace Placement
Opening braces are to always be the last character of the line which opens the code block. Closing braces are to exist on their own line, with the same indentation as the parent opening line.

#### Function Definitions
The first line of a function definition should include the required preamble, function name the parameter list and opening brace.

	define_function char fooBar (integer a, char b) {
	    // Do something
	}

#### Event Handlers
Netlinx event handlers are to be formatted in the same way as function blocks. That is, the opening brace is to sit on the same line as the event definition.

	button_event[device, 0] {
	
	    push: {
	        // Do push event guff
	    }
	
	    release: {
	        // Do release event
	    }
	
	}

#### Non-Function / Event Statement Blocks
All other statement block are to have the opening brace appear on the same line as the block's opening statement.

	if (x > y) {
	    // Do something
	}


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
