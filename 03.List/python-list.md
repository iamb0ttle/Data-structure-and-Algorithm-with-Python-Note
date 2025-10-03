# Python List
- Python List is representative List implementation by **Dynamic Array**.
- Python is implemented by C(Language). So, Python List is originally C Lang Array.
- But Python List can store various data type elements, because element is stored its memory location address(not a value) in Array.
- So, we can store both string and integer data in the same List. 

## Disadvantage
Python List has some disadvantages that cause by implementing List as Array.

1. **Array Copy**: When generated List for the first time, List's size is initialized. And when array is filled by some `append()` operation, to store new element, python generate new array with bigger size(commonly `12% ~ 50%`) and copy all of List element. So, some `append()` operation can takes long time.
2. **Insertion and Removal**: If new element is inserted or removed from List's middle(not `front` and `rear`), Python move all of List elements into next location.

Mainly Python List disadvantages are situations that can takes long time.

# Python Tips: what about Python variable?
- Also Python variable contains value memory address instead of real value. 
- So, it is possible situation that different data type values are contained in same variable.
- When happens variable copy(like `x = y`), python variable copy its memory address instead of making new memory space. 
    ```py
    x = 100
    y = x

    print(f"x value: {x}, x memory address: {id(x)}") # x value: 100, x memory address: 140722376852176
    print(f"y value: {y}, y memory address: {id(y)}") # y value: 100, y memory address: 140722376852176

    x = 200
    print("\n--- After assign 200 in 'x' ---")
    print(f"x value: {x}, x memory address: {id(x)}") # x value: 200, x memory address: 140722376855376
    print(f"y value: {y}, y memory address: {id(y)}") # y value: 100, y memory address: 140722376852176
    ```