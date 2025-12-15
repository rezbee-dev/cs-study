# CS 61A WK 1

[source](https://github.com/romanbird/sicp/blob/main/week1/hwsicp-1-2.pdf)

## Question 1

- Evaluating the modified `sqrt-iter` that uses `new-if` instead of `if` will result in infinite loop since `new-if` is a procedure and so all arguments are evaluated, leading to infinite loops
- `if` on the other hand is a special form where applicative order does not apply and so all args are not evaluated, thereby preventing infinite loops

## Question 2

```scm
(define (squares nums)
    (define (square x) (* x x))
    (every square nums)
)
```