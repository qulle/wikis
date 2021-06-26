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

// Not Exakt, raw pointer
bool Salad_Lover::prefer(Food const* food) const
{
    return dynamic_cast<Salad const*>(food);
}

// Not Exakt, smart pointer
bool Salad_Lover::prefer(std::shared_ptr<Food> const& food) const
{
    return dynamic_cast<Salad*>(food.get());
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
