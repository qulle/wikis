# C++ language feature
A living document with useful C++ tips and tricks.

## Table of Contents
### Misc
- [Type Checking](#type-checking)
- [Generate random numbers](#generate-random-numbers)
- [Check if palindrom](#check-if-palindrom)

### STL
- [STL read and write from std](#stl-read-and-write-from-std)

### Templates
- [Templates filter based on argument type](#templates-filter-based-on-argument-type)
- [Variadic templates](#variadic-templates)

## Type Checking
```cpp
// Exakt match, raw pointer
bool Pizza_Lover::prefer(Food const* food) const
{
    return typeid(*food) == typeid(Pizza);
}

// Exakt match, smart pointer
bool Pizza_Lover::prefer(std::shared_ptr<Food> const& food) const
{
    return typeid(*food.get()) == typeid(Pizza);
}

// Not exakt, raw pointer
bool Salad_Lover::prefer(Food const* food) const
{
    return dynamic_cast<Salad const*>(food);
}

// Not exakt, smart pointer
bool Salad_Lover::prefer(std::shared_ptr<Food> const& food) const
{
    return dynamic_cast<Salad*>(food.get());
}
```

## Generate random numbers
```cpp
#include <random>

std::random_device eng{};
std::uniform_int_distribution<int> dist{0, 20};

for(int i{}; i < 20; ++i)
{
    std::cout << dist(eng) << std::endl;
}
```

## Check if palindrom
```cpp
bool is_palindrome(std::string const& str)
{
    long unsigned length{str.length()};
    for(unsigned i{}; i < length; ++i)
    {
        if(str[i] != str[length - 1 - i])
        {
            return false;
        }
    }

    return true;
}
```

## STL read and write from std
```cpp
#include <algorithm>
#include <numeric>
#include <iterator>

// Get input
std::vector<int> v {
    std::istream_iterator<int>{std::cin},
    std::istream_iterator<int>{}
};

// Write output
std::vector<int> v {1, 2, 3, 4};
std::copy(
    std::begin(v),
    std::end(v),
    std::ostream_iterator<int>{std::cout, " "}
);
```

## Templates filter based on argument type
### Compile
```
cl /EHsc /std:c++17 print-test.cc
```

### print-test.cc
```cpp
#include <ostream>
#include <iterator>
#include <utility>
#include <iostream>
#include <vector>
#include <map>
#include <tuple>
#include <array>
#include <string>

#include "print.h"

/* Expected output:
5
{1, 2, 3}
{(1 1), (2 2), (3 3)}
(5 3.14)
{hello, world}
{{ab, c}, {def, g, hi}}
SFINAE
string literal
*/

int main()
{
    print(std::cout, 5);
    std::cout << std::endl;
  
    std::vector<int> v {1, 2, 3};
    print(std::cout, v);
    std::cout << std::endl;

    std::map<int, int> m { {1, 1}, {2, 2}, {3, 3} };
    print(std::cout, m);
    std::cout << std::endl;

    std::tuple<int, double> t { 5, 3.14 };
    print(std::cout, t);
    std::cout << std::endl;

    std::string s[] { "hello", "world" };
    print(std::cout, s);
    std::cout << std::endl;
  
    std::array<std::vector<std::string>, 2> a {
        std::vector<std::string>{ "ab", "c" },
        std::vector<std::string>{"def", "g", "hi"}
    };
  
    print(std::cout, a);
    std::cout << std::endl;

    char const* str {"SFINAE"};
    print(std::cout, str);
    std::cout << std::endl;

    print(std::cout, "string literal");
    std::cout << std::endl;
}
```

### print.h
```cpp
#ifndef PRINT_H
#define PRINT_H

#include <ostream>
#include <utility> // std::get
#include <string>
#include <cstddef> // std::size_t
#include <tuple>
#include <array>

// Normal printable stuff
template <typename T>
auto print(std::ostream& os, T const& obj) -> decltype(os << obj, os);

// Containers, if has iterator
template <typename T>
auto print(std::ostream& os, T const& obj) -> decltype(obj.begin(), obj.end(), os);

// If has std::get<T> (std::tuple, std::pair)
template <typename T>
auto print(std::ostream& os, T const& obj) -> decltype(std::get<0>(obj), os);

// If array []
template <typename T, std::size_t N>
std::ostream& print(std::ostream& os, T (&obj)[N]);

// If std::array<T>
template <typename T, std::size_t N>
std::ostream& print(std::ostream& os, std::array<T, N>& obj);

// Function overload std::string
std::ostream& print(std::ostream& os, std::string const& str);

// Function overload const char*
std::ostream& print(std::ostream& os, const char* str);

// Helpfunctions
template <typename T>
void print_help(std::ostream& os, T const& obj);

#include "print.tcc"

#endif
```
### print.tcc
```cpp
// Normal printable stuff
template <typename T>
auto print(std::ostream& os, T const& obj) -> decltype(os << obj, os)
{
    os << obj;

    return os;
}

// Containers, if has iterator
template <typename T>
auto print(std::ostream& os, T const& obj) -> decltype(obj.begin(), obj.end(), os)
{
    print_help(os, obj);

    return os;
}

// If has std::get<T> (std::tuple, std::pair)
template <typename T>
auto print(std::ostream& os, T const& obj) -> decltype(std::get<0>(obj), os)
{
    os << '(' << std::get<0>(obj) << ' '  << std::get<1>(obj) << ')';

    return os;
}

// If array []
template <typename T, std::size_t N>
std::ostream& print(std::ostream& os, T (&obj)[N])
{
    print_help(os, obj);

    return os;
}

template <typename T, std::size_t N>
std::ostream& print(std::ostream& os, std::array<T, N>& obj)
{
    print_help(os, obj);

    return os;
} 

// Function overload std::string
std::ostream& print(std::ostream& os, std::string const& str)
{
    os << str;

    return os;
}

// Function overload const char*
std::ostream& print(std::ostream& os, const char* str)
{
    os << str;

    return os;
}

// Helpfunctions
template <typename T>
void print_help(std::ostream& os, T const& obj)
{
    os << '{';
    
    bool first = true;
    for(auto&& v : obj)
    {
        if(!first) { os << ", "; }

        print(os, v);
        first = false;
    }

    os << '}';
}
```

## Variadic templates
### Compile
```
cl /EHsc /std:c++17 print-test.cc
```

```cpp
#include <iostream>

// Base case
void foo();

// Unpacking
template<typename T, typename... Ts>
void foo(T first, Ts... rest);

// Unpacking
template<typename T, typename... Ts>
void foo(T first, Ts... rest)
{
    std::cout << "Un-packing : " << first << std::endl;
    
    foo(rest...);
}

// Base case
void foo()
{
    std::cout << "Base-case" << std::endl;
}

int main()
{
    foo(1, 2, 3.0f, 4);
}
```
