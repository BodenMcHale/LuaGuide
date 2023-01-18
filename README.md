# LuaGuide

This is a WIP and not yet finished. I'm finishing up the last few sections.

[Lua Crash Course by PohkaDev](https://www.youtube.com/watch?v=kgiEF1frHQ8)

[Lua Math](http://lua-users.org/wiki/MathLibraryTutorial)

[Lua Official Documentation](https://www.lua.org/docs.html)

[Lua Reference Guide by Pohka](https://github.com/pohka/Lua-Beginners-Guide)

[Tic80 Learn](https://tic80.com/learn)

[Tic80 Wiki](https://github.com/nesbox/TIC-80/wiki)

A mostly reasonable approach to Lua curated around Tic80.

Contributors are welcome.

## Table of Contents
  1. [Values and Types](#values-and-types)
  1. [Keywords](#keywords)
  1. [Variables](#variables)
  1. [Functions](#functions)
  1. [Comments](#comments)
  1. [Semicolons](#semicolons)
  1. [Naming Convention](#naming-convention)
  1. [Scope](#scope)
  1. [Loops](#loops)
  1. [Tables](#tables)
  1. [Math](#math)
  1. [License](#license)

## Values and Types
**Primitives**

There are six primitive types in Lua: `nil`, `boolean`, `number`, `string`. 

 + `nil`
 + `boolean`
 + `number`
 + `string`

```lua
local a = nil -- non-value
local b = true -- true boolean
local c = false -- false boolean
local d = "HelloWorld" -- string

print(a) -- nil
print(b) -- "true"
print(c) -- "false"
print(d) -- "HelloWorld"
```

The type `nil` has one single value, `nil`, whose main property is to be different from any other value; it often represents the absence of a useful value. 

```lua
local a = nil -- non-value

print(a) -- nil
```

The type `boolean` has two values, `true` and `false`. Both `nil` and `false` make a condition `false`; they are collectively called `false` values. Any other value makes a condition true. 

Despite its name, `false` is frequently used as an alternative to `nil`, with the key difference that `false` behaves like a regular value in a `table`, while a `nil` in a `table` represents an absent key. 

```lua
local a = true -- true boolean
local b = false -- false boolean

print(a) -- "true"
print(b) -- "false"
```

The type `string` should be surrounded in double quotes `""`.

The string concatenation operator in Lua is denoted by two dots `..`. 

If both operands are strings or numbers, then the numbers are converted to strings in a non-specified format.

 ```lua
local a = "StringOne"
local b = "StringTwo"
local c = 2

local d = a .. b
local e = "A: " .. a
local f = "Number of strings: " .. c

print(d) -- "StringOneStringTwo"
print(e) -- "A: StringOne"
print(f) -- "Number of strings: 2"
 ```

**Complex**

There are two complex types in Lua: `table` and `function`

 + `table`
 + `function`

 See [Functions](#functions) for more examples on `functions`.

 ```lua
local tableA = {"Item1", "Item2", "Item3"} -- table

print(tableA[1]) -- "Item1"

for i,v in pairs(tableA) do
    print(tableA[i]) -- prints each item on a new line
    -- "Item1"
    -- "Item2"
    -- "Item3"
end

-- declaring a new function
local function snake_case()
  local a = "This is a function" -- string

  print(a) -- "This is a function"
end
```

**[Return to the Table of Contents](#table-of-contents)**

## Keywords
Names (also called identifiers) in Lua can be any string of Latin letters, Arabic-Indic digits, and underscores, not beginning with a digit and not being a reserved word. 

Identifiers are used to name variables, table fields, and labels.

The following keywords are reserved and cannot be used as names:
+ `and`
+ `break`
+ `do`
+ `else`
+ `elseif`
+ `end`
+ `false`
+ `for`
+ `function`
+ `goto`
+ `if`
+ `in`
+ `local`
+ `nil`
+ `not`
+ `or`
+ `repeat`
+ `return`
+ `then`
+ `true`
+ `until`
+ `while`

Lua is a case-sensitive language: `and` is a reserved word, but And and AND are two different, valid names. As a convention, programs should avoid creating names that start with an underscore followed by one or more uppercase letters.

**[Return to the Table of Contents](#table-of-contents)**

## Variables

**Arithmetic Operators**
Lua supports the following arithmetic operators:
- \+ addition
- \- subtraction
- \* multiplication
- / float division
- // floor division
- % modulo
- ^ exponentiation

With the exception of exponentiation `^` and float division `/`, the arithmetic operators work as follows: If both operands are integers, the operation is performed over integers and the result is an integer. Otherwise, if both operands are `numbers`, then they are converted to floats, the operation is performed following the machine's rules for floating-point arithmetic and the result is a float.

Exponentiation `^` and float division `/` always convert their operands to floats and the result is always a float. Exponentiation `^` uses the ISO C function pow, so that it works for non-integer exponents too.

Floor division `//` is a division that rounds the quotient towards minus infinity, resulting in the floor of the division of its operands.

Modulo `%` is defined as the remainder of a division that rounds the quotient towards minus infinity, similiar to floor division `//`.

```lua
local a  =  1
local b  =  0.5
local c = 3.2

local d  =  a + c -- addition
print(d) -- 4.2

local e  =  c - a -- subtraction
print(e) -- 2.2

local f  =   a * b-- multiplication
print(f) -- 0.5

local g = c / b -- float division
print(g) -- 6.4

local h = c // b -- floor division
print(h) -- 6

local i = c % b -- modulo
print(i) -- 0.2

local j = b ^ c -- exponentiation
print(j) -- 0.10881882041202

local k  =  (1 + 3) * 2 -- addition and multiplication
print(k) -- 8

print(1 + 1) -- 2
print(-a) -- -1
```

**Relational Operators**

Lua supports the following relational operators:
- == equality
- ~= inequality
- < less than
- \> greater than
- <= less or equal
- \>= greater or equal

These operators always result in `true` or `false`. 

Equality `==` first compares the type of its operands. If the types are different, then the result is `false`. Otherwise, the values of the operands are compared. `Strings` are equal if they have the same byte content. `Numbers` are equal if they denote the same mathematical value.

`Tables` are compared by reference: two `tables` are considered equal only if they are the same `table`. Every time you create a new `table`, this new `table` is different from any previously existing `table`. 

A function is always equal to itself. Functions with any detectable difference (different behavior, different definition) are always different. Functions created at different times but with no detectable differences may be classified as equal or not (depending on internal caching details).

Equality comparisons do not convert `strings` to `numbers` or vice versa. Thus, "0"==0 evaluates to `false`, and t[0] and t["0"] denote different entries in a `table`.

The operator `~=` is exactly the negation of equality `==`

The order operators work as follows. If both arguments are `numbers`, then they are compared according to their mathematical values, regardless of their subtypes. Otherwise, if both arguments are `strings`, then their values are compared according to the current locale.

**Logical Operators**

The logical operators in Lua are `and`, `or`, and `not`. All logical operators consider both `false` and `nil` as `false` and anything else as `true`.

The negation operator not always returns `true` or `false`. The conjunction operator and returns its first argument if this value is `false` or `nil`; otherwise, and returns its second argument. The disjunction operator or returns its first argument if this value is different from `nil` and `false`; otherwise, or returns its second argument. 

Both `and` and `or` use short-circuit evaluation; that is, the second operand is evaluated only if necessary. 

Here are some examples:
- 10 or 20 = 10
- 10 or error() = 10
- nil or "a" = "a"
- nil and 10 = nil
- false and error() = false
- false and nil = false
- false or nil = nil
- 10 and 20 = 20

**[Return to the Table of Contents](#table-of-contents)**

## Comments - TODO: Add this section, explaination for the single and multi line comment and two seperate examples

Single line comments are created using `--`.

Multiline comments are created using `--[[]]--`.

```lua
-- this line of text will not run
--comment without a space

--[[ 
This is how
to write a
multi-line comment
print("HelloWorld")
]]--

print("HelloWorldd") -- same line comment
```

**[Return to the Table of Contents](#table-of-contents)**

## Functions - TODO: Add this section, explaination for the different functions and one example minimum for each

Passing an argument through the `function`.

```lua
function printTax(price)
  local tax  =  price * 0.10 -- 10% tax on items
  print("Tax: " .. tax)
end

printTax(100)
```

`Functions` can return values.

```lua
-- function that returns a value
function calculateTax(price)
  return price * 0.10 -- 10% tax on itmes
end

local a = 100

local taxIncludingPriceWithNumber = calculateTax(100)
local taxIncludingPriceWithVariable = calculateTax(a)

print(taxIncludingPriceWithNumber) -- $110
print(taxIncludingPriceWithVariable) -- $110
```

```lua
-- multiple parameters
function displayInfo(name, age, country)
  print(name .. " is " .. age .. " years old and is from " .. country)
end
displayInfo("Billy", 12, "Jupiter")
```
```lua
-- declaring a new function
local function snake_case()
  local a = "This is a function" -- string

  print(a) -- "This is a function"
end

local function passing_number(200)
  local a = "This is a function" -- string

  print(a) -- "This is a function"
end

-- calling the function
snake_case()
 ```

## Semicolons - TODO: Explain more

Semi-colons in Lua are generally only required when writing multiple statements on a line.

```lua
local a,b=1,2; print(a+b)
```

Alternatively

```lua
local a,b=1,2
print(a+b)
```

**[Return to the Table of Contents](#table-of-contents)**

## Naming Convention TODO: Add this section, explaination and two examples

**[Return to the Table of Contents](#table-of-contents)**

## Scope TODO: Add this section, explaination and two examples
Variables have different scopes. Once the end of the scope is reached the values in that scope are no longer accessable
```lua
function foo()
  local a  =  10
end
print(a) -- nil
```

```lua
local isAlive  =  true
if isAlive then
  local a  =  10
end
print(a) -- nil
```

**Global Variable**
```lua
local _G.myValue  =  69
-- doing this can sometimes be bad practice
```

**[Return to the Table of Contents](#table-of-contents)**

## Loops TODO: Add this section, explaination and two examples
There is a few different ways you can do a loop in lua
```lua
-- while loop
local i  =  0
local count  =  0
while i < =  10 do
  count  =  count + 1
end
print("count is " .. count) -- count is 7
-- for loop
count  =  0
for i = 1, 5 do
  count  =  count + 1
end
print("count is " .. count)
```

**Infinite Loops**
```lua
-- infinite loop will never end
local i  =  0
while i > =  0 do
 i  =  i + 1
 print(i)
end
```

**Nested Loops**
```lua
local count  =  0
for a = 1, 10 do
  for b = 1, 10 do
    count  =  count + 1
  end
end
print(count) --  100
```

**[Return to the Table of Contents](#table-of-contents)**

## Tables TODO: Add this section, explaination and two examples
```lua
-- basic table
local colors  =  { "red", "green", "blue" }
print(colors[1]) -- red
print(colors[2]) -- green
print(colors[3]) -- blue
-- using a loop to iterate though your table
for i = 1, #colors do
  print(colors[i])
end
```

**Table Manipulation**
```lua
-- insert
local colors  =  { "red", "green", "blue" }
table.insert(colors, "orange")
local index  =  #colors -- 4 (this is the last index in the table)
print(colors[index]) -- orange
```

```lua
-- insert at index
local colors  =  { "red", "green", "blue" }
table.insert(colors, 2, "pink")
for i = 1, #colors do
  print(colors[i])
end
-- red, pink, green, blue
```

```lua
-- remove 
local colors  =  { "red", "green", "blue" }
table.remove(colors, 1)
for i = 1, #colors do
  print(colors[i])
end
--  "green", "blue"
```

**2 Dimensional Table**
```lua
-- tables within tables
local data  =  {
  { "billy", 12 },
  { "john", 20 },
  { "andy", 65 }
}
for a = 1, #data do
  print(data[a][1] .. " is " .. data[a][2] .. " years old")
end
```

**Key Tables**

2 dimensional tables are not suited to data with different types, instead uses keys for tables
```lua
local teams  =  {
    ["teamA"]  =  12,
    ["teamB"]  =  15
}
print(teams["teamA"]) --  12
for key,value in pairs(teams) do
  print(key .. ":" .. value)
end
```

```lua
-- insert into key table
teams["teamC"]  =  1
```

```lua
-- remove key from table
teams["teamA"]  =  nil
```

**Returning a Table from a Function**

This can be used to return multiple values from a functions
```lua
function getTeamScores()
  local scores  =  {
    ["teamA"]  =  12,
    ["teamB"]  =  15
  }
  return scores
end
local scores  =  getTeamScores()
local total  =  0
for key, val in pairs(scores) do
  total + =  val
end
print("Total score of all teams:" .. total)
```

**[Return to the Table of Contents](#table-of-contents)**

## Math TODO: Add this section, explaination and two examples
The `math` class has a number of `functions` for dealing with numbers. There are plenty more but these are some of the more useful ones.

* abs (absolute value)
  ```lua
  local x  =  -10
  print(math.abs(x)) -- result: 10
  local a  =  10
  print(math.abs(a)) -- result: 10
  ```
* ceil (round up decimal value)
  ```lua
  local x  =  1.2
  print(math.ceil(x)) -- result: 2
  ```
* deg (Convert value from radians to degrees)
  ```lua
  print(math.deg(math.pi)) --  result: 180
  ```
* floor (round down decimal value)
  ```lua
  local x  =  1.2
  print(math.floor(x)) -- result: 1
  ```
* pi (constant value of pi)
  ```lua
  print(math.pi) -- 3.1415926535898
  3.1415926535898
  ```
* rad (Convert value from degrees to radians)
  ```lua
  print(math.rad(180)) -- result: 3.1415926535898
  ```
* random (random number generation)
  ```lua
  -- random value between 0 tand 1
  print(math.random()) -- result: 0.0012512588885159
  -- random integer value from 1 to 100 (both inclusive)
  print(math.random(100)) -- result: 20
  -- random integer value from 20 to 100 (both inclusive)
  print(math.random(20, 100)) -- result: 54
  ```
* sqrt (Square root of a number)
  ```lua
  print(math.sqrt(100)) -- result: 10
  ```

**[Return to the Table of Contents](#table-of-contents)**

## License

MIT License

Copyright (c) 2023 Boden McHale

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

**[Return to the Table of Contents](#table-of-contents)**

**[Return to LuaGuide](#luaguide)**Guide for Lua programming based around the Tic80 fantasy console.
