# Programming-Languages-Notes
## Grammer
'<'expression'>' ::= '<'variable'>'
## Variables
- Name : 'x', 'Fred'
- Value: 
- Type:
- Scope:
- Lifetime:

### Lifetime
Variables that always exist:
- math.pi
- math.e

Program header

### Scope
Global: available everywhere 

Global Scope:

Static Scope (local):
- Allocated at compile time

Dynamic Scope (local):
- Allocated at run time (recursion)

### Binding
Implementing an attribute to a variable.

This can be done with a dictionary of variables. Bless Python and its data structures.

### Syntax
- Function Parameter
- Test their values
- Assignment
- Create them - implicit/autmoatic
- Get the value of the variable

('<'set'>' '<'name'>' '<'expression'>')

Set is now a reserved word.

'<'name'>' ::= contiguous sequence of characters or numbers but must include a non-numeric character. It can't be a reserved word.

The lexical analyzer(tokenizer) and the parser will impose the grammer rules above for variables.

Below is some of the necessary code. Mostly for the evaluator; we need to upgrade the parser and tokenizer to check the variables and see if they are valid names and such. Assume at the time of evaluation that the variables are valid. So any validation should occur before evaluation.

### Semantics

    # mapping names to values
    Bindings = {}
    .
    .
    .
    evalL(parseTree):
        if parseTree[0] == "set":
            # create the variable
            # bind it to its value
            Bindings[parseTree[1]] = evalL(parseTree[2])

### More Semantics

    (set x (+ 5 7))
    .
    .
    .
    (set y (+ 5 x)) # what do we do here?

    # in the evaluator
    # bindings is a potential name fr the dictionary
    if parseTree in Bindings:
        return Bindings[parseTree]

## Function Definitions
(def '<'name'>' '<'argumentList'>' '<'body'>')

def is a keyword.

    evalL(parseTree):
        if parseTree[0] == 'def':
            Bindings[parseTree[1]] = parseTree[2:] # use the same dictionary as the variables
        .
        .
        .
        # how to execute the function
        if parseTree[0] in Bindings:
            for i in range(0, len(parseTree[2])):
                Bindings[Bindings[2,i]] = evalL(parseTree[2,i])
            return evalL(parseTree[3])


## Scoping - 2/13/20
Only allow the function to access certain variables
Scopes are always concentric in a program.
That is, inner scopes inherit all variables in the outer scopes.
You can repeat this forever. i.e. define an inner scope inside the inner scope

Dynamic Scoping - Try to find the variable in the dictionary for the scope you are currently in (inner scope), then try to go up a level and search for the variable in that dictionary. 

An example of denoting scoping in C++ is 
{-denotes beginning of scope 
}- denotes close of scope

For our language every function call creates a new scope.  In the scope is:
- All input parameters are in the scope
- All assignments made in the scope

## Decision on how to Scope - 2/13/20

Possible Solution: Make a global array.
The first dictionary in the array will be the outermost scope.
as new scopes are defined we increment the location in the global array and place the new scope dictionary there.
When searching through scopes to find a variable just decrement the global variable and go through the scope dictionary's going up to the outermost scope.

## Continuation about eLInterpreter 2/18/20

Set and def will modify things

## Short Circuit Evaluation

An expression in which the result is determined without evaluating all of the operands and/or operators
In the and case - if anything evaluates to false, you can skip the rest of evaluations
In the or case - if anything evaluates to true, you can skip the rest of evaluations

### Homework - 2/18/20

Read Chapter 7 and 8 notes/slides.
eL Interpreter assign due Firday.

## Delayed Evaluation - 2/27/2020

- Templates

- Macros

- Lazy vs Eager Evaluation

Given a list return the length of the list

6 <- (length (quote (1 2 3 4 5 22)))

"On the way back"

    (def length (list)
    (if (atom list)
        0
        (+ (length (rest list)) 1))))

Alternate Version - "On the way down"

    (def length (list)
        (len list 0))
    (def len(list count)
        (if (atom list)
            count
            (len (rest list) (+ 1 count))))

### For Loop

First in Python:

    def len(list):
        i = 0
        for item in list:
            i += 1
        return i

Now in eL:

Cliffhanger...