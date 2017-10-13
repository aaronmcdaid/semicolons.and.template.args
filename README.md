In C++, instead of having to type:

    std::get<1>(tup);
    
I would like to be able to type this instead:

    std::get(1; tup);
    
So that whenever a semicolon appears inside function-call parentheses, everything to the left of the semicolon would be treated as template args. This could be used with constructors also:

    auto v = vector<int>(5);   // current form
    auto v = vector(int; 5);   // new form

even with braces for initializer lists:

    auto v = vector<int>{2,3,5,7};   // current form
    auto v = vector{int; 2,3,5,7};   // new form

I don't think this introduces any ambiguity, as I don't think there's any other case where a semicolon can appear within parentheses or braces like this.

The initial motivation is simply to make some metaprogramming look more "function-like". `is_same<T, U>{}` could become `is_same(T, U;)`

As well as saving a few characters, it could simplify some ambiguities:

    this->         f<int>(); // Might fail at the moment, when written inside a template
    this->template f<int>(); // Current solution
    this->         f(int ;); // Proposed alternative solution, as the semicolon makes
                             // it obvious that 'f' is a template
    
([More info](https://stackoverflow.com/questions/610245/where-and-why-do-i-have-to-put-the-template-and-typename-keywords) on that last issue.)
  
