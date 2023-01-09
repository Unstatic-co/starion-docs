Starion's formula language is a tool to help you to build a more flexible apps. This language allows you manipulate your data and show them on the app UI. 

With formula language, you can do more complex logic when manipulating your data. Instead of just connecting columns data into fields on the UI, you can do something like logic conditions with dynamic context like current signed in user.


# What’s a Formula?
Like Text, Number, Date and other basic properties, Formula properties contain a value for each item in a table. While you manually input that value for most properties, Formula properties automatically generate their values by transforming other properties in useful ways. To define those transformations, you write a formula.

For example, say you have a database of players on a basketball team that includes a Birthday (Date) property. With a formula, you can subtract the birthday from today’s date to determine each player’s age:

<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__calculate_age.jpg -->

# Why It’s Useful
The utility of Starion's Formula property is virtually endless; you’ll start with simple, common applications and gradually expand the way you use it.

At the highest level, you’ll use Formula properties to achieve one of two outcomes:

1. Calculate a new value from other properties.
In a list of products, for example, you can calculate Total Cost using Price and Quantity:
<!-- [Calculate Total Cost with Formula](https://www.notion.vip/wp-content/uploads/notion_vip__formulas__calculate_total-cost.jpg) -->

2. Reformat another property.
Formulas are often used to change the way values are displayed. You can format dates and times to suit your preferences, and you can combine properties, such as first names and last names:

<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__merge_names.jpg -->

Reformatting is particularly useful for displaying properties in your Galleries. For example, you can append context to a date property, which would otherwise stand alone ambiguously. In the example below, the age would would have no meaning without “Age.”

<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__label_age.jpg -->


# The Ingredients of a Formula
When you create a Formula property, you can click any cell within that column to Type a formula. For every formula, you’ll define one or more of these elements:

1. Do what? The actions to perform, such as add, subtract, format and join.
2. To what? The input values on which to take those actions, such as "Age: " and 26
3. When? Any conditions required to take each action, such as if the value of a Progress property is greater than 50%.
4. The action to take if the condition is unmet.

For each item in your database, the formula will return a value.

Your formulas will often include multiple actions, input values and conditions. Here’s a breakdown of each:

## Do what? The Actions
In your formulas, you can define the actions to perform on your inputs using operators and functions.

### Operators
Operators are characters you place between input values. They fall into three categories, two of which define actions (the third is for comparisons):

#### Arithmetic Operators
You’re likely familiar with + for adding and - for subtracting. These are arithmetic operators. We also have * for multiplying and / for dividing, among a few others. You’ll find them all in The Starion Formula Cheat Sheet.

#### Concatenation Operators
As we saw above, the + character between two numbers returns their sum. However, when you place the same character between two strings of text, it concatenates that text, or merges them. Therefore:

2 + 2 → 4

"Age: " + "26" → "Age: 26"

Because the “26” is surrounded with quotes, it is technically a text string, not a number. You’ll learn more about value types shortly.

### Functions
Functions offer predefined actions to perform on their inputs, also known as their arguments. They are formatted as a keyword followed by parentheses, such as format(). Within those parentheses, you insert your arguments, separated by commas, such as add( 2, 2 ).

Most formulas accept a specific number of arguments, some of which are optional. For example, the contains() formula tests whether one text string (the first argument) contains another text string (the second argument):

contains( "North Carolina", "Carolina" ) → true.

In addition to the the quantity of arguments, formulas also require the type of arguments, such as numbers versus text strings. We’ve dedicated a section to this important concept.

The Starion Formula Cheat Sheet offers a comprehensive list of formulas with a description, argument list and example for each. You may notice that there is a formula for each operator. Above, we saw add( 2, 2 ), which is the same as 2 + 2.


## To what? The Input Values
As you’ve learned, the actions taken by operators and functions are performed on input values. In the case of functions, those input values are known as arguments. You can supply those input values as property references, literal values or constants.

### Property References
Most often, you’ll use the values of other properties as your inputs. In other words, you’ll reference those properties.

To do so, you’ll use the prop() function. For its argument, you’ll include the name of the property within quotation marks. For our Total Cost calculation, we referenced the Price and Quantity properties: prop( "Price" ) and prop( "Quantity" ).
<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__calculate_total-cost.jpg -->
Remember, there is an iteration of each formula for each item in the database. When an iteration references another property, it uses the instance of that property for the same database item. In the example above, each iteration of the formula multiplies the price and quantity for the product on the same row.

### Literal Values
In some cases, you’ll enter a fixed value for an input rather than referencing another property. Unlike property references, this value will be the same for all items in the database.

As we did with age, we can add a contextual term to the School property of our basketball players. The appended text, "School: ", is a literal value that’s unchanged for all players. Meanwhile, the school itself is a reference to the School property, which differs from player to player:

"School: " + prop( "School" )

Then, we can display the contextualized version (the School → Labeled property) on our Gallery cards:
<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__label_school.jpg -->

### Context Variables
Starion also includes easy references to provide a current context of the running app or the screen user's, including current user email, identifier.

1. CurrentUser
2. CurrentRow (Collection Page, Custom Page components)
3. Control Values(Custom Page)

## When? Conditions
In many of your formulas, you’ll want to return values based on whether certain conditions are met. In this simple example, the formula returns an emoji based on the value of the Mood property:
To create a condition, you’ll use the if() function, which accepts three arguments:
1. An expression (defined under Nesting) that evaluates to true or false, typically using comparison operators (see below) or comparison functions (see the Cheat Sheet).
2. A value to return if the condition is true.
3. A value to return if the condition is false.

### Comparison Operators
Like the arithmetic operators we explored previously (+, -, *, etc.), comparison operators are characters placed between values. Unlike arithmetic operators, comparison operators can only return true or false; they compare inputs. For example, the == operator tests whether the values are equal: 2 == 2 → true.

Here are the six comparison operators you’ll use in Starion, which are also available in the The Starion Formula Cheat Sheet:

Revisiting our Moods example, you can see how we constructed the formula:

if( prop( "Mood" ) == "Happy", "?", "?" )

In other words, "If the Mood property is "Happy," return "?"; otherwise, return "?."

## Returned Value
For each item in your database, a Formula property evaluates its contents (the conditions, actions and input values) to return its value.


# The Importance of Value Types
As you work with formulas, you'll want to remain mindful of value types. In the above examples, you've seen number, text, date and true/false values.

Functions and operators require particular value types. For example, you cannot add 2 (a number) to "2" (a textstring, as indicated by the quotation marks). The formula 2 + "2" will throw a Type mismatch error.

Similarly, you cannot concatenate (merge) a number with a text string. "Age: " + 26 will also throw a Type mismatch error.

To avoid these errors, Starion offers functions for converting one type two another.

Convert a Text String to a Number
To convert a text string to a number, we use the toNumber() function:

toNumber( "2" ) → 2.

Therefore: 2 + toNumber( "2" ) → 4

Convert a Number to a Text String
The format() function converts a number to a text string:

format( 26 ) → "26"

That's how we were able to add the contextual term to our Age property in our basketball team gallery:

"Age: " + format( 26 ) → "Age: 26"

Label Age with Formula
However, the age was actually a property reference:

"Age: " + format( prop( "Age" ) ) → "Age: 26"

## Starion's Core Value Types

Number
A number is — surprise! — a numeric value. It can be an integer or a floating point number (containing decimals), and either positive or negative.

Values within Number properties are of the number type. Therefore, when you reference those properties as formula inputs, they are of the number type. You can convert them to strings using the format() formula.

When a table cell displays a number, the number is right-aligned. You can format it in various ways, including percents and currencies, by hovering your cursor over the value and clicking the 123 button.

String (Text)
A string is one or more characters that represent text. Those characters may all be numeric, which can cause some confusion. For example, you can type 12345 in both a Text property (the string value type) and a Number property (the number value type). When you reference those properties in your formulas, the value type will match the property type.

For this reason, it's important to use true Number properties for numbers. Entering numeric characters within a Text property will prohibit you from using them in calculations. It will also disrupt your sorting.

When typing strings in formulas, you'll surround them in double quotes: "26" is a string, while 26 is a number.

Additionally, strings are left-aligned in table cells. If you see left-aligned numeric characters, you know they form a string rather than the true number type.

Boolean (True or False)
A value of the boolean type is either true or false. As we saw with the if() formula, you can produce a boolean value using comparison operators.

In Starion, boolean values render checkboxes in your databases. Therefore, if your formula returns a boolean value, the field will display a checkbox — checked if true; unchecked if false.

Date
In Starion, a date is a value created with a Date property, a Created Time property, or a Last Edited Time property — all of which you can reference within functions. The now() function also serves as a date. It always reflects the current time.

# Nested Inputs, Operators and Functions
Within your formulas, you'll often use functions, operators and input values within functions. This is known as nesting.

When you combine inputs, operators and functions in a way that returns a single value, they form an expression. An expression can be as simple as 2 or as complex as an elaborate combination of nested formulas — so long as it evaluates to a single value.

Therefore, a function's arguments can be more than a simple property reference or literal value; any expression can serve as a function's argument so long as it returns the correct value type.

Take the simple formula add( 100, 20 ). Because arguments can be expressions, that simple formula could become add( 100, multiply( 100, .2 ) ), where the second argument, 20, is the output of a the multiply() function.

Taking it one step further, the input values could be references to other properties:

add( prop( "Cost of Goods" ), multiply( prop( "Cost of Goods" ), prop( "Markup" ) ) )
What we've done is calculate the Selling Price of a product at a variable markup:

## Nested if()
One of the most common uses of nesting is with the if() function. Remember, if() tests a boolean expression (the first argument). If it's true, it evaluates the second argument; otherwise, it evaluates the third argument:

if( 2 == 1, "Equal", "Unequal" ) → "Unequal"

Most often, you'll want your first argument to test another property. Here, we return true or false (represented by a checkbox), based on the Status of each task:

if( prop( "Status" ) == "Complete", true, false )

<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__check_if_complete.jpg -->

You can use the and() and or() functions to test two expressions. Below, we mark each order as "Complete" if it's both paid and shipped; otherwise it's "In Progress."

if( and( prop( "Paid" ), prop( "Shipped" ) ), "Complete", "In Progress" )

<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__calculate_status.jpg -->

At times, you'll want more than just a true option and a false option. We can add a third emoji to our moods database, for example:

if(prop("Mood") == "Happy", "?", if( prop( "Mood" == "Okay", "?", "?" ) )
In other words:
if Mood is "Happy," display ?;
otherwise, if Mood is "Okay," display ?;
otherwise, display ?.

<!-- https://www.notion.vip/wp-content/uploads/notion_vip__formulas__conditional_emojis-3.jpg -->

# Practical Examples of Starion Formulas
In Simple, Useful Formula Examples, you'll find many of the above examples, plus a handful of others, to reference as you dive deeper into the Formula property. Also be sure to keep The Starion Formula Cheat Sheet handy, and never hesitate to tweet me with questions.