# **the Dimensium Coding Standard**

`Team rules.` Everyone who contributes to our reositories and projects should follow this coding standard, in order to unify the coding style. Clean codes improves maintainbility, don't it?

This file is full of code examples, and contains many languages and many rules, please read'em all, and then you can feel free to code.

## Basics

### Philosophies for everyone

#### 1. Write open source code

Dimensium is an open-source community, so please write open source code as a Dimensium collabrator.

#### 2. Feel free to ask

There's no differences between dimensium collabrators. You always has the right to ask anybody if there's something troubles you.

#### 3. **`Team rules`**

`Team rules.` obey the standard and rules, including coding style and requirements of clean code.

#### 4. Accept contributions and collabrations

This principal is simple, no need to explain it.

#### 5. A real artist will sign on their works

Feel free to write your name on things you did and collabrated in Dimensium.

### Coding

#### 1. Which language to use

Use English to express anything in code. And use English to discuss with other Dimensium coders as much as possible.

There's no limit of specific programming language for Dimensium coders. But main programming language we use is C/C++ and languages in C Programming Language Family:

- C
  - C++ / Cpp2 / Carbon
  - Objective-C / Objective-C++
  - Java / J#
    - Kotlin
  - C#
  - Rust
  - ECMAScript
    - Typescript
  - Perl
  - PHP
  - ...

#### 2. Express intent

Absolutely.

#### 3. Write stable programs

Absolutely.

#### 4. Crash early

Absolutely.

#### **5. Program behaviors**

<!-- TODO -->

#### **6. Coding Style**

The coding style written in `clang-format` is also put in the directory. download it and run it in `clang-format-15`.

We use C++ examples most, but this style is also available to other programming languages.

##### 6.1 Basics

###### 6.1.1 Length of each line

Keep the length of source lines to 19 characters or less for the readability.

###### 6.1.2 Curly brackets and indentations

Every curly brackets that opens a block should put in the 1st column of a line.

```cpp
class X
{// NOTICE THIS
    private:
        void greatPrivateFunc(void)
        {// NOTICE THIS
        }
    public:
        X(void) = default;
        X(X const&) = default;
        X &operator=(X const&) = default;

        void greatPublicFunc(void)
        {// NOTICE THIS
        }
};
```

When initing variables (especially arrays) using curly brackets (e.g. uniform initialization syntax `Type var_name {value}`), if value is too long (e.g. too many values to init an array), the curly brackets should put on next line.

```cpp
int array_contains_a_lot_of_items /*NO = HERE*/
    {// NOTICE THIS, USING UNIFORM INITIALIZATION SYNTAX
        1,2,3,4,5,6,7,8,
        1,2,3,4,5,6,7,8,
        1,2,3,4,5,6,7,8,
        1,2,3,4,5,6,7,8,
    };
int array_contains_a_lot_of_items_using_c_style_init = 
    {// NOTICE THIS
        1,2,3,4,5,6,7,8,
        1,2,3,4,5,6,7,8,
        1,2,3,4,5,6,7,8,
        1,2,3,4,5,6,7,8,
    };
```


For classes which has a long initializaion list, we put the colon the same line after the space after the right bracket. the initialization put on the next line after another indentation.

```cpp
class X
{
    private:
        int data_member_01;
        int data_member_02;
        int data_member_03;
        int data_member_04;
        int data_member_05;
        int data_member_06;
        int data_member_07;
        int data_member_08;
        int data_member_09;
    public:
        X(
            int init_01, 
            int init_02, 
            int init_03, 
            int init_04, 
            int init_05,
            int init_06,
            int init_07,
            int init_08,
            int init_09) :
            data_member_01 {init_01},
            data_member_02 {init_02},
            data_member_03 {init_03},
            data_member_04 {init_04},
            data_member_05 {init_05},
            data_member_06 {init_06},
            data_member_07 {init_07},
            data_member_08 {init_08},
            data_member_09 {init_09}
        { }

        X(X const&) = default;
        X &operator=(X const&) = default;
};
```

For all operators, we put spaces reasonably. For example:

```java
public class Main
{
    public static int main(String[] args)
    {
        int a = 0;
//           ^ ^
        a = 1 + 3*2 + 5*6;
//       ^ ^    ^~~   ^~~
    }
}
```

But unfortunately, code formatter doesn't care the operator hierarchy. It always formats like this:

```java
a = 1 + 3 * 2 + 5 * 6;
```

Put a space after semicolons in three statement in begin of `for` statement, put a space after:

- control statement keyword, e.g.:
  - `for`
  - `if`
  - `switch`
- `catch` 

```cpp
for (init; pred; inc)
// ^      ^     ^
{
    ...stmts...
}

if (pred)
//^
{
    ...stmts...
}

switch (value)
//    ^
{
    case some_case:
    {
        ...stmts...
        break;
    }
    case some_other_case:
    {
        ...stmts...
        break;
    }
    ...other_cases...:
        ...other_stmts...
}

try
{
    ...stmts...
}
catch (something)
//   ^
{
    ...handling...
}
catch (some_other_thing)
//   ^
{
    ...handling_other_thing...
}
catch (...)
{
    ...handling_all_other_thing...
}
```


But don't put space after:

- function declarations, including `constexpr` functions in C++
- declarations of macro with parameters
- function names in function-invoking expression statement.

See ex.:

```cpp
ReturnType functionName(ArgumentType parameter)
//                    ^~
{
    ...stmts...
}

constexpr int constexprFunctionName(
//                                ^~
    constexpr ConstexprArgumentType parameter)
{
    ...stmts...
}

#define macroName(parameter) ...
//              ^^

functionName(argument);
```

see this example C++ code for detail:

```cpp

#include <some_headers>

namespace dimensium_coding_standard
{
    template <typename T>
//          ^
    class Stack
    {
        private:
//  ^~~~         <---add an extra indentation before access modifiers
            struct Node;
            std::shared_ptr<Node> head;
            std::mutex head_mutex;
        public:
            Stack(void) = default;
//                     ^~~         <---add spaces
            Stack(Stack const&) = delete;
//                             ^~~
            Stack &operator=(Stack const&) = delete;
//                                        ^~~
            Stack(Stack &&);
            Stack &operator=(Stack &&);

            void push(T const&);
            std::shared_ptr<T> pop(void);

            std::size_t size(void);
//          reasonably add empty lines to separate different declarations.
    };

    template <typename T>
    struct Stack<T>::Node
    {
        T item;
        std::shared_ptr<T> down;
    };

    template 
}
```



###### 6.1.3 naming identifiers

We use traditional C-Style function declarations and only put return type after declaration when necessary. When identifiers are too long, put them on next line and add an indentation on the start of the new line. Whatever, see the ex.:

```cpp

void normalFunction(void)
{ }

int anotherNormalFunction(SomeType some_argument)
{ }

// NOTICE THIS
LooooooooooooooooongReeeeeeeetuuuuuuuurnnnnnnnTyyyyyypeeeee
    looooooooooooongFuuuuuuuunctiiiiiioooooon(
        LooooooooongAaaaaaaarguuuuuuumeeeeentTyyyypeeeee1
            aaaaaaaaaaaarguuuuuuumeeeeeeent_1,
        LooooooooongAaaaaaaarguuuuuuumeeeeentTyyyypeeeee2
            aaaaaaaaaaaarguuuuuuumeeeeeeent_2)
{ }

// ONLY NECESSARY, WE PUT RETURN TYPE AFTER DECLARATION
template <typename TLeft, typename TRight>
auto add(TLeft x, TRight y) -> decltype(x+y)
{
    return x + y;
}
```

Use camel case with lower case character at first to name a function and macro with arguments:

```cpp
void greatName1(void);  // GREAT
//   ^~~~~~~~~~
int greatName2(void);   // GREAT
//  ^~~~~~~~~~
#define greatName3(some_argument) (some_argument)       //GREAT
//      ^~~~~~~~~~
#define greatName4(some_argument, ...) {someFunction((some_argument), __VA_ARGS__)} //GREAT
//      ^~~~~~~~~~
// ...
```


Use camel case with upper case character at first to name a class, enum, struct, typedef, `using` in C++11, and other user defined **type**:

```cpp
class SomeClass;
//    ^~~~~~~~~         <------NOTICE
struct SomeStruct;
//     ^~~~~~~~~~ 
enum class SomeEnumeration
//         ^~~~~~~~~~~~~~~
{ };
typedef SomeType SomeTypedef;
//      ^~~~~~~~ ^~~~~~~~~~~
using SomeTypeAlias = SomeType;
//    ^~~~~~~~~~~~~   ^~~~~~~~
```


> We use `parameter` to refer the `formal parameter`, use `argument` to refer the `actual argument`.

Use snake style to name a variable, namespace, parameter, enumeration value, and this rule makes code easy to see if the identifier is variable or type because we use different naming methods, and also avoiding the use of `HN`.

```cpp
void someFunction(int some_argument);
//                ^~~~~~~~~~~~~~~~~         <------NOTICE

int some_variable;
//  ^~~~~~~~~~~~~ 

SomeType another_variable;
//       ^~~~~~~~~~~~~~~~

namespace some_namespace
//        ^~~~~~~~~~~~~~
{ }

enum class SomeEnumeration
{
    foo_bar, bar_baz, baz_qux, foo_baz, foo_qux,
//  ^~~~~~~  ^~~~~~~  ^~~~~~~  ^~~~~~~  ^~~~~~~
};
```

When there's abbreviations in camel case names, just put them upper case. See:

```cpp
    UUID getUUIDOfEntity(Entity const&);
//  ^~~~    ^~~~
```

When there's abbreviations in snake style names, just put them lower case and leave a dash around them. See:
```cpp
// Do:
CompilerABIInfo compiler_abi_info;
// Don't:
CompilerABIInfo compiler_a_b_i_info;
```

Here's also a ex. for python to show how wide the range it can be used. We use `this` instead of `self` for the 1st parameter of member functions:

```python
def someFunction():
#   ^~~~~~~~~~~~
    pass
class SomeClass(SomeBaseClass):
#     ^~~~~~~~~ ^~~~~~~~~~~~~
    def __init__(this):
#                ^~~~
        this.some_data_member = some_value
#       ^~~~ ^~~~~~~~~~~~~~~~   ^~~~~~~~~~
    def someMemberFunction(this, some_parameter):
#       ^~~~~~~~~~~~~~~~~~ ^~~~  ^~~~~~~~~~~~~~
        pass
```

Ex. for Javascript:

```javascript
class SomeClass
//    ^~~~~~~~~
{
    constructor(some_argument)
//              ^~~~~~~~~~~~~
    {
        this.some_value = some_argument;
//           ^~~~~~~~~~   ^~~~~~~~~~~~~
    }

    function someMemberFunction(some_argument)
//           ^~~~~~~~~~~~~~~~~~ ^~~~~~~~~~~~~
    {
        doSomethingWith(this.some_value, some_argument);
//      ^~~~~~~~~~~~~~~      ^~~~~~~~~~  ^~~~~~~~~~~~~
    }
};
```

###### 6.1.4 Express intent directly

The rule is quite simple but quite important. Naming an identifier properly may be difficult, when you have trouble for naming an identifier, make a `TODO` comment for it, express what the name should be, to let other coders think about a better name.

**Intent should be expressed anywhere.**

Example, bad

```cpp
for (int index = 0; index < sz; ++index)
    doSomethingWith(array[index]);
```

Example, better

```cpp
for (intent::Index index = 0; index < array.size(); ++index)
    doSomethingWith(array.at(index));
```

Example, great
```cpp
for (auto const&item : array)
    doSomethingWith(item);

// even changing "item" to x, the intent still very obvious and easy to read:

for (auto const&x : array)
    doSomethingWith(x);
```

Another example, bad

```cpp
class FncDat
{
    private:
        std::chrono::time_point<std::chrono::system_clock> gt;
        DatPak pak1, pak2;
    public:
        // snip

        std::chrono::time_point<std::chrono::system_clock> getYMDHMS(void) const;
        DatPak getData(void) const;
};
```

Another example, great

```cpp
class FinanceData
{
    private:
        std::chrono::time_point<std::chrono::system_clock> generation_timestamp;
        DataPackage internal_data, finance_data;
    public:
        // snip
        std::chrono::time_point<std::chrono::system_clock> getGenerationTimestamp(void) const;
        DataPackage getFinanceData(void);
};
```





[Dimensium]: https://github.com/dimensium
