# funmath227

## Problem statement

[URL link](https://www.linkedin.com/feed/update/urn:li:activity:7206853346815623169)

```text
Fun Math #227

Bellamy went to a store and bought an electronic gadget which cost $90.05.
She paid with a $100 bill and received the change in coins.

Since the store was in Canada, the denominations of the coins could be 5 cents, 10 cents, 25 cents, a dollar, or two dollars, as shown in the picture below.

What were the minimum and maximum number of coins that she could receive?
```
<p><img src="https://github.com/my-LinkedIn/funmath227/blob/main/assets/cad-coins.jpeg"><p>

When it comes to `Discrete Optimisation` problems my way to go is [MiniZinc](https://github.com/my-LinkedIn/funmath227/blob/main/README.md#references)... I strongly recommend it!

## Source code

### Model

```minizinc
include "globals.mzn";

% Define Coin denominations in cents
int: five_cents = 5;
int: ten_cents = 10;
int: twentyfive_cents = 25;
int: one_dollar = 100;
int: two_dollars = 200;

% Total change in cents
int: total_change = 995;

% Decision variables
var 0..total_change div five_cents: num_five_cents;
var 0..total_change div ten_cents: num_ten_cents;
var 0..total_change div twentyfive_cents: num_twentyfive_cents;
var 0..total_change div one_dollar: num_one_dollar;
var 0..total_change div two_dollars: num_two_dollars;

% Constraints
constraint
    num_five_cents * five_cents +
    num_ten_cents * ten_cents +
    num_twentyfive_cents * twentyfive_cents +
    num_one_dollar * one_dollar +
    num_two_dollars * two_dollars == total_change;
```

### Minimization Objective

```minizinc
solve minimize
    num_five_cents +
    num_ten_cents +
    num_twentyfive_cents +
    num_one_dollar +
    num_two_dollars;

output ["Min number of coins: \(num_five_cents + num_ten_cents + num_twentyfive_cents + num_one_dollar + num_two_dollars)\n"];
```

### Maximisation Objective

```minizinc
solve maximize
    num_five_cents +
    num_ten_cents +
    num_twentyfive_cents +
    num_one_dollar +
    num_two_dollars;

output ["Max number of coins: \(num_five_cents + num_ten_cents + num_twentyfive_cents + num_one_dollar + num_two_dollars)\n"];
```

## Output

Nota: MiniZinc can only consider one Objective at a time, so you have to solve 2 distinct problems but using a common Model.

### Minimisation
```text
...
Min number of coins: 10
----------
==========
Finished in 549msec.
```
### Maximisation
```text
...
Max number of coins: 199
----------
==========
Finished in 443msec.
```

## References

  - [MiniZinc](https://www.minizinc.org/)
  - [Discrete optimization](https://en.wikipedia.org/wiki/Discrete_optimization)
