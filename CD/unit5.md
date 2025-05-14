## Code Optimization 
is the process of improving the intermediate code so that faster-running and/or less memory-consuming machine code is generated without changing the program's output.

- The optimization must be correct, it must not, in any way, change the meaning of the program.
- Optimization should increase the speed and performance of the program.
- The compilation time must be kept reasonable.
- The optimization process should not delay the overall compiling process.

### Types 
1. Machine Dependent : Performed with machine-specific instructions/constraints.
    1. Register Allocation 
### 2. Peephole Optimiation : Local improvements in small code sequences - RFD
The small set of instructions or small part of code on which peephole optimization is performed is known as peephole or window.
- It basically works on the theory of replacement in which a part of code is replaced by shorter and faster code without a change in output. The peephole is machine-dependent optimization.

1. Redundant load and store elimination : In this technique, redundancy is eliminated.
- Initial code:
y = x + 5;
i = y;
z = i;
w = z * 3;

- Optimized code:
y = x + 5;
w = y * 3; //* there is no i now 
//* We've removed two redundant variables i & z whose value were just being copied from one another.

2. Flow control optimixzadtions :
    1. Avoid jumps on jumps:
    example:
- Initial code:
    L1 : jump l2
    l2: jump l3
    l3: jump l4
    l4: 
- Optimized code:
    L1 : jump `l4`
    l2: jump l3
    l3: jump l4
    l4 : 

3. Deadcode Elimination:-
Dead code refers to portions of the program that are never executed or do not affect the program’s observable behavior. Eliminating dead code helps improve the efficiency and performance of the compiled program by reducing unnecessary computations and memory usage.
- extra calculations which arent used .
- always false loops.

- Initial Code:-
int Dead(void)
{
    int a=10;
    int z=50;
    int c;
    c=z*5;
    printf(c);
    a=20; 
    a=a*10; //No need of These Two Lines 
    return 0;
    }
- Optimized Code:-
int Dead(void)
{
    int a=10;
    int z=50;
    int c;
    c=z*5;
    printf(c);
    return 0;
    }   


2. Machine Independent : At IR level; not specific to target architecture.

- 4 loop optis : FFUJ.
- 4 rest :       SSAF.

### 1. Loop Optimization: Focuses on reducing time complexity inside loops  - 
    1. To apply loop opti we first must detect loops.
    2. we use `Control flow analysis` using `program flow graph` to detect loops.
    3. to find PFG we use Basic Blocks .
    4. loops are cycles in PFG.

 - To find Basic Blocks :
 1. we find leaders .
 2. basic block is from 1 leader to (next leader-1);
> entry and exit if no of nodes and edges are needed to find .

- how to find leaders?
    1. first TAC is a leader.
    2. target of any cond or unconditional jump is a leader.
    3. immediate follow of above is a leader.
#### types :
1. Frequency reduction or Code Motion :
- In frequency reduction, the amount of code in the loop is decreased. A statement or expression, which can be moved outside the loop body without affecting the semantics of the program, is moved outside the loop. 
Example:
- Before optimization:
```c
while(i<100)
{
 a = Sin(x)/Cos(x) + i;
 i++;
}

- After optimization:

t = Sin(x)/Cos(x);
while(i<100)
{
 a = t + i;
 i++;
} 
```
2. Loop Unrolling
Loop unrolling is a loop transformation technique that helps to optimize the execution time of a program. We basically remove or reduce iterations. Loop unrolling increases the program’s speed by eliminating loop control instruction and loop test instructions. 
- Example :
```c
- Before optimization:

for (int i=0; i<10; i++)
    printf("Pankaj\n");

After optimization:

for (int i=0; i<10; i+=2)
    printf("Pankaj\n");
    printf("Pankaj\n"); 

```
3. Loop Jamming
Loop jamming is combining two or more loops in a single loop. It reduces the time taken to compile the many loops. 
Example:
```c
- Before optimization:

for(int i=0; i<5; i++)
    a = i + 5;
for(int i=0; i<5; i++)
    b = i + 10;

- After optimization:

for(int i=0; i<5; i++){
 a = i + 5;
 b = i + 10;
} 
```

4. constant folding :
eg 2*3.14 = 6.28 at compiling time .

5. Common Subexpression elimination :
```c
//Code snippet in three address code format
t1=x*z;
t2=a+b;
t3=p%t2;
t4=x*z;     //t4 and t1 is same expression 
            //but evaluated twice by compiler.
t5=a-z;

// after Optimization
t1=x*z;
t2=a+b;
t3=p%t2;
t5=a-z;
```
6. Strength Reduction :
It suggests replacing a costly operation like multiplication with a cheaper one. 
```c
Example:
a*4 

after reduction
a<<2
```
 7.  Algebraic expression simplification :
A program might contain some trivial algebraic expressions that do not result in any useful computation or change of value. Such lines of code can be eliminated so the compiler doesn’t waste time evaluating it. For example,
A=A+0;
x=x*1;

## Dominatrs
A node d of a flow graph dominates a node n if `every path` from the initial node of the flow graph to n goes through d.
– Denoted as “d dom n”
• The entry node of a loop dominates all nodes in the loop
• Every node dominates itself.


## heuristic nod listing
list all interiors nodes till 
{
    leftmost has all parents listed 
}

order for TAC calac = reverse 

## cost 
1. MOV R1, R0 => cost = 1
2. MOV a, r1 => 2
3. MOV a, b => 3

> Only 2 registers .

### simple code gen cost
more 
1. Register is to be freed and moved cost 2 more.

#### haeuristic 
1. less bcz sequential .