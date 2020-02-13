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
