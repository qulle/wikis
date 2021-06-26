# C++ language feature
A living document with useful C++ tips and tricks.

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
