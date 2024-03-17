# Learning C#

## FCC Lesson 1

### Console.WriteLine();

```cs
Console.WriteLine("Hello World!");
```

Common mistakes new programmers make:

- C# is case sensitive.

  Entering lower-case letters instead of capitalizing C in Console, or the letters W or L in WriteLine.

- C# differentiates between single and double quotes.

  Forgetting to use double-quotation marks, or using single-quotation marks to surround the phrase Hello World!.

- The semi-colon is not optional!

  Forgetting a semi-colon at the end of the command.

### Console.Write();

```cs
Console.Write("Congratulations!");
Console.Write(" ");
Console.Write("You wrote your first lines of code.");
```

### `Console.WriteLine();` Vs. `Console.Write();`

`Console.WriteLine();` prints output to the console and adds a 'line feed' at the end. `Console.Write()`, on the other hand, prints subsequent messages to the same line.

### Comments

Comments are made with two forward slashes in front like so...

```cs
// Console.WriteLine("Hello World!");
```

### Tid bits

- C# is a <i>compiled</i> language.
- Double quotes for a <b>string literal</b>
- The semicolon is called the <b>end of statement operator</b>

### Questions:

- C is compiled into binary... what is C# compiled into?

## FCC Lesson 2

### Types first

C# is strongly typed

We declare variables the same way is in C. That is, data type first, var name, then assignment operator, then value. For example:

```cs
string firstName = "Bob";
```

### Implicitly typed local variables

An implicitly typed local variable is created by using the `var` keyword followed by a variable initialization. For example:

```cs
var message = "Hello world!";
```

Note that variables using the `var` keyword must be initialized when declared.

### Data types

C# has a lot of different data types

- **String**
  ```cs
  string myText = "Hello, World!";
  ```
  - Strings use double quotes
- **Char**
  ```cs
  char myChar = 'A';
  ```
  - Chars use single quotes, as in C
- **Decimal**

  ```cs
  decimal decimalNumber = 3.141592653589793238m;
  ```

  - 128-bit
  - 28-29 significant digits precision
  - Provides greater accuracy when dealing with decimal fractions, making it ideal for applications involving currency, taxation, and scientific calculations where round-off errors must be minimized.
  - Generally, slower performance compared to float and double due to its higher precision and larger size.

- **Double**

  ```cs
  double doubleNumber = 3.14159;
  ```

  - 64-bit
  - ~15-17 significant digits precision
  - Offers a good balance between precision and performance, making it the default choice for most general-purpose numeric calculations in C#.

- **Float**

  ```cs
   float floatNumber = 3.14f;
  ```

  - 32-bit
  - ~6-9 significant digits precision
  - Typically used in applications where memory usage and performance are more important than precision, such as graphics processing, scientific simulations, and real-time systems.

- **Boolean**

  ```cs
  bool isTrue = true;
  ```

- **Integer data types**

  ```cs
  // Integer data types
  int integerNumber = 10;          // 32-bit signed integer
  long longNumber = 123456789L;    // 64-bit signed integer
  short shortNumber = 100;         // 16-bit signed integer
  byte byteNumber = 200;           // 8-bit unsigned integer
  ```

- **Some other data types**
  ```cs
  DateTime currentDate = DateTime.Now;  // Date and time
  TimeSpan timeDifference = TimeSpan.FromHours(2);  // Represents a time interval
  ```

## Variable Names Rules

- Use camelCase
- Save initial underscore for special occassions
- Use an initial alphabetic character
- Variable names can contain alphanumeric characters and \_
- Special characters such as # or $ are not allowed
- Can't begin with a number
- Are case sensitive
- Can't use reserved words

  ```cs
  // Some examples of variable names
  char userOption;

  int gameScore;

  decimal particlesPerMillion;

  bool processedCustomer;
  ```

## FCC Lesson 3

### Escape sequences

| Sequence | Effect                                                          |
| -------- | --------------------------------------------------------------- |
| \n       | new line                                                        |
| \t       | tab                                                             |
| \\       | double backslash to escape the backslash as an escape character |
| \u       | Unicode escape character                                        |

```cs
// Kon'nichiwa World
Console.WriteLine("\u3053\u3093\u306B\u3061\u306F World!");
```

> **Note:**
>
> There are several caveats here. First, some consoles like the Windows Command Prompt will not display all Unicode characters. It will replace those characters with question mark characters instead. Also, the examples used here are UTF-16. Some characters require UTF-32 and therefore require a different escape sequence. This is a complicated subject, and this module is only aiming at showing you what is possible. Depending on your need, you may need to spend quite a bit of time learning and working with Unicode characters in your applications.

### Verbatim string literal

A verbatim string literal will keep all whitespace and characters without the need to escape the backslash. To create a verbatim string, use the `@` directive before the literal string.

```cs
Console.WriteLine(@"    c:\source\repos
        (this is where your code goes)");
```

### String interpolation

Of course, one can do string concatenation. For example:

```cs
string firstName = "Jane";
string greeting = "Goodbye,";
Console.WriteLine(greeting + " " + firstName + "!");
```

However, string interpolation can be better.

```cs
string firstName = "Jane";
string greeting = "Goodbye,";
string message = $"{greeting} {firstName}!";
```

### Combine verbatim literals and string interpolation

```cs
string projectName = "First-Project";
Console.WriteLine($@"C:\Output\{projectName}\Data");
// Output will be...
// C:\Output\First-Project\Data
```

## FCC Lesson 4

### C# can do implicit type conversion

```cs
string firstName = "Bob";
int widgetsSold = 7;
Console.WriteLine(firstName + " sold " + widgetsSold + " widgets.");
```

### Int truncation

As with C, C# truncates int values in division where a decimal answer would be produced. So, for example:

```cs
int quotient = 5 / 2;
Console.WriteLine(quotient);
// 2 and not 2.5
```

We can use a type that supports decimals instead:

```cs
decimal decimalQuotient = 5.0m / 2;
Console.WriteLine($"Decimal quotient: {decimalQuotient}");
// Decimal quotient: 2.5
```

This also works:

```cs
decimal decimalQuotient = 7 / 5.0m;
decimal decimalQuotient = 7.0m / 5.0m;
```

But this doesn't:

```cs
int decimalQuotient = 7 / 5.0m;
int decimalQuotient = 7.0m / 5;
int decimalQuotient = 7.0m / 5.0m;
decimal decimalQuotient = 7 / 5;
```

### Type Casting

You can also temporarily type cast one or both of the ints to a decimal capable type. For example:

```cs
int first = 5;
int second = 2;
decimal quotient = (decimal)first / (decimal)second;
Console.WriteLine(quotient);
```

> Operators like +=, -=, \*=, ++, and -- are known as compound assignment operators because they compound some operation in addition to assigning the result to the variable. The += operator is specifically termed the addition assignment operator.

### A note on value++ vs. ++value incrementing

Both the increment and decrement operators have an interesting quality — depending on their position, they perform their operation before or after they retrieve their value. In other words, if you use the operator before the value as in ++value, then the increment will happen before the value is retrieved. Likewise, value++ will increment the value after the value has been retrieved.

```cs
int value = 2;
Console.WriteLine("First: " + value);       // First: 2
Console.WriteLine($"Second: {value++}");    // Second: 2
Console.WriteLine("Third: " + value);       // Third: 3
Console.WriteLine("Fourth: " + (++value));  // Fourth: 4
```

### Readability

> Since you'll write the code once but read it many times, you should prioritize readability!

### Convert Fahrenheit to Celsius

My solution (with rounding):

```cs
int fahrenheit = 94;
decimal celsius = (fahrenheit - 32m) * 5 / 9;
Console.WriteLine("The temperature is " + Decimal.Round(celsius, 1) + " Celsius.");
// The temperature is 34.4 Celsius.
```

Microsoft's solution:

```cs
int fahrenheit = 94;
decimal celsius = (fahrenheit - 32m) * (5m / 9m);
Console.WriteLine("The temperature is " + celsius + " Celsius.");
```

## FCC Lesson 5
