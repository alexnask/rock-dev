## Chapter 0: Coding style

While there is no official coding for rock, some conventions have been picked up over the years.  
This is an attempt to document them as accurately as possible.  

Note that many of these conventions do not apply to older parts of rock's codebase.  

### Whitespace

No tabs.  
No whitespace at the end of a line.  
Use '\n' newlines (not "\r\n").  

### Line length

There is no hard limit on the length of a line.  
However, it is strongly suggested to keep lines relatively small.  
If it cannot be refactored by splitting off smaller expressions, break up the line using '\\'.  

### Nesting

It is strongly suggested to keep your nesting level below five (5).  
Splitting off sections of code into local functions is encouraged if it can make your code less nested and easier to follow.

### Indentation

Use four (4) spaces per level (usually scope but includes closure code in function arguments).  

### Operators

Use no space between a unary operator and its expression.
Use one (1) space between a binary operator and its right and left hand side expressions.  

In comma separated lists, use no spaces between the left side element and the comma operator and one (1) space between the comma operator and the right side element.

### Control statements, bracing

If you can omit an empty pair of braces, for example in a function declaration with an empty body, it is encouraged to do so.  
Function declarations with a single expression body can be written in a single line.  

Use one (1) space between your control statement keyword and parenthesis enclosed expression.

Use K&R style braces: Opening brace at the end of first line, closing brace at the same indentation level as the statement.  

else/else if blocks are declared on the same line as the previous block closing brace.  

match statement cases may either be a single expression or define a block that increments the indentation level on the next line.

Brace control statements, even single statement ones.  

The only exceptions are loops or match statements that only happen when a condition is met.  
In that case, you may write your if and condition and, on the same line, start your loop statement.

Here are some examples:  

```ooc

Foo: class {
    // Empty body omitted
    init: func

    // Single expression function collapsed into one line
    giveMeSomeInt: func -> Int { 42 }

    // Regular function declaration
    action: func {
        a := match {
            // case is a single expression
            case true => 42
            // case is a block with its own indentation level
            case      =>
                x := fetch()
                process(x)
        }


        // Chaining if-else if-else statements
        if (false) {
        } else if (true) {
        } else {
        }

        // Single statement if still brace enclosed
        if (someBool) {
            return
        }

        // Conditional loop may omit if braces
        if (true) for (i in 0 .. 10) {
            "#{i}" println()
        }
    }
}

```

### Naming conventions

Use PascalCase for type names.  
Use camelCase for method and field names.  
Use a '_' prefix for private functions, methods and fields.  
Use a '?' suffix for Bool fields and methods, instead of the "isX" convention.

### Function declarations

Write function signatures in a single line.  
If the function defines generic parameters, the declaration list should be separated by one (1) space from the left side.
If the function takes no arguments, omit empty parentheses.  
If the function takes arguments, the argument list must be separated by one (1) space from the left side.  
If the function returns nothing, avoid "-> Void".  
If the function returns some non-void type, the return type arrow must be separated by one (1) space from each side.  

When the function returns some expression at the end of its body, omit "return".  
Use default arguments sparingly.  
Use automatically typed ('.') and automatically assigned ('=') arguments whenever possible.

Function signature examples:  

```ooc

// Generic parameters, no arguments, no return type
// Note: This function cannot be used in practise, T and V are always unresolved
f1: func <T, V>
// Generic parameters, arguments, no return type
f2: func <T> (t: T, al: ArrayList<T>)
// Generic parameters, arguments, return type
f3: func <Type> (hash: Int) -> Type
// No generic parameters, no arguments, no return type
f4: func
// No generic parameters, arguments, no return type
f5: func (a, b: Int)
// No generic parameters, arguments, return type
f6: func (a: Int) -> String
// No generic parameters, no arguments, return type
f7: func -> Int

```

### Variable type checking

When if a variable is an instance of some type, prefer the use of a match statement/expression over if statements and instanceOf? calls.

### Variable declarations

Use the assign-infer operator (":=") whenever your desired variable type will always match the type of the initial expression.  
Use typed variable declarations when initializing to a subtype of the desired variable type rather than using the assign-infer operator and a cast.

When a typed variable declaration is used, use no spaces between the variable name and the colon character, then one (1) space and finally its type.  

### Function calls

Use no spaces between the function name or expression and the function call argument list.  
Chained function calls that use the '.' operator should be separated by at least one (1) space on either side of the operator.  

The argument list may be broken into multiple lines ending with a comma (except the last line).  
Each line's first argument should line up with the previous line's first argument, in such a way that all first arguments from the first to the last line are lined up.  

### Types

Function types follow the same rules as function declaration signatures.  
Generic and template types should not be separated form their type argument instantiation list.  
Array, pointer and reference types should not have their respective symbols ("[]", '*', '@') separated from their base type.