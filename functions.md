# Functions

Functions can be defined inline or using the `function` keyword, e.g.:

`f(x,y) = 2x+y`

```
function f(x)
  x+2
end
```


## Arguments

Arguments are normally specified by position, while arguments given after a semicolon are instead specified by name.  
The call of the function must respect this distinction, calling positional argument by position and keyword arguments by name (e.g., it is not possible to call positional arguments by name).  
The last argument(s) can be specified together with a default value.

`myfunction(a,b;c=1) = (a+b)*3c`
 
All keyword arguments need a default value, but the opposite is not true (positional arguments can also have default argument).


## Return value

Return value using the keyword `return` is optional: by default it is returned the last computed value.  
The return value can also be a tuple (so returning effectively multiple values):

```
myfunction(a,b) = a*2,b+2
x,y = myfunction(1,2)
```

## Multiple-dispatch (aka polymorphism)

The same function can be defined with different number and type of parameters (this is useful when the same kind of logical operation must be performed on different types).  
When calling such functions, Julia will pick up the correct one depending from the parameters in the call (by default the stricter version).  
These different versions are named "methods" in Julia and, if the function is type-safe, dispatch is implemented at compile time.

## Templates (type parametrisation)

Functions can be further specified regarding on which types they works with, using templates:

`myfunction{T<:Number,T2}(x::T,y::T2,z::T2) = 5x + 5y + 5z`

The above function first defines two types, T (a subset of Number) and T2, and then specify each parameter of which of these two types must be.

## Functions as objects

Functions themselves are objects and can be assigned to new variables, returned, or nested. E.g.:

```
f(x) = 2x # define a function f inline
a = f(2)  # call f and assign the return value to a
a = f     # bind f to a new variable name (it's not a deep copy)
a(5)      # call again the (same) function
```

## Call by reference / call by value

Parameters given to functions are normally passed by reference.  
Functions that do change their arguments have their name, BY CONVENTION, postponed by a `!`, e.g.:

`myfunction!(ref_par, other_pars)` (the parameter that will be changed is by convention the first one)
