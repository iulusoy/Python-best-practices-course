# Pitfalls: Common ways to introduce bugs in your Python code

## Shallow and deep copies

When copying lists and other mutable variable types like dictionarys, using an `=` sign only points the new variable to the same position in memory as the initial one. Changing one then automatically changes the other.

[*Example*](https://github.com/ssciwr/Python-best-practices-course/blob/main/Material_Part4_Pitfalls/copy_list.py)

**Solution**: Use `copy` or `deepcopy` instead to create copies of objects.

## Instantiation of mutable default keyword arguments in function calls

Default arguments are only evaluated once: At the time the function is created. If you provide a mutable default keyword argument and then change it in the function, the next time the function is called without that keyword, the default will point to the same address as in the first call; but the argument will have already changed, so the default in the first call and the default in the second call are different. 

[*Example*](https://github.com/ssciwr/Python-best-practices-course/blob/main/Material_Part4_Pitfalls/mutable_default.py)

**Solution**: Only provide non-mutable default arguments..

## Naming the module

A source of errors can be naming a module the same as another module that is imported, in this example the module is named `math.py` but also imports math from the standard Python library; and function calls using methods from the math module will fail, as Python will look for those in the `math.py` file. 

[*Example*](https://github.com/ssciwr/Python-best-practices-course/blob/main/Material_Part4_Pitfalls/math.py)

**Solution**: Name your module file different than the modules that you are importing.

## Exhausting iterators

Iterators and generators can be exhausted, meaning you can only use them once. 

[*Example*](https://github.com/ssciwr/Python-best-practices-course/blob/main/Material_Part4_Pitfalls/exhaust_iterators.py)

**Solution**: If you create an iterator or a generator and you need it more than once you need to save it first. As in the example provided, the iterator is created using `zip`, and can be saved in a `list`.

## Variable assignment in different scopes

Assigning a variable within a function shadows any assignment that may have happened in an outer scope. 

[*Example*](https://github.com/ssciwr/Python-best-practices-course/blob/main/Material_Part4_Pitfalls/assignment.py)

**Solution**: Pass the variable as an argument into the inner scope or use the return value of a new assignment.

## Closure variable binding

Python uses late binding, resulting that in closures variables are only looked up once the inner function is called. 

[*Example*](https://github.com/ssciwr/Python-best-practices-course/blob/main/Material_Part4_Pitfalls/closure.py).


**Solution**: Make sure the referenced variables are either passed to the inner function or are set correctly in the surrounding scope.

**Task 1: Experiment with the different modules in this section and reproduce the error and the solution.**
