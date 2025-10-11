# Algorithm Performance
- Algorithm may use time and memory(space) to execute algorithm.
- The more algorithm use resource less, the better. 
- So here is many way, to tracking algorithm resource consumption:
    - **Empirical Analysis**: Tracking time and memory space by using programming language's module like python `time`, C++ `chrono` and etc. But, this way is different result depending to hardware performance.
    - **Instruction Counting**: This way is to express operation counts as function that have `n`(input size) as input. If algorithm has once substitution operation and two loop, expression will be *2n+1*.
    - **Asymptotic Notation**: This way is to express algorithm's complexity when `n` increases infinitely. 
- Algorithm performance exist in 3 case: best, average and worst. We have to tracking all of these 3 cases.

## Asymptotic Notation
- Representative Asymptotic Notation technique is '**Big-O**', '**Big-Omega**' and '**Big-theta**'.

![https://knovhov.com/big-o-notation-fastest-to-slowest-time-complexity/](https://knovhov.com/wp-content/uploads/2020/12/asymptotic-analysis.jpg)

### Big-Omega(Best case)
- Big-Omega is way to express function that show lower bound of algorithm.
- Real algorithm complexity function is bigger than or same with Big-Omega function. 

### Big-O(Worst case)
- Big-O is way to express function that show upper bound of algorithm.
- Real algorithm complexity function is smaller than or same with Big-O function.

### Big-Theta(Average case)
- Big-O is way to express function that show middle bound of algorithm.
- Real algorithm complexity function is bigger than or smaller than Big-Theta function.
