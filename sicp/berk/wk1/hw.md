# CS 61A WK 1

[source](https://github.com/romanbird/sicp/blob/main/week1/hwsicp-1-2.pdf)

## Question 1

- Evaluating the modified `sqrt-iter` that uses `new-if` instead of `if` will result in infinite loop since `new-if` is a procedure and so all arguments are evaluated, leading to infinite loops
- `if` on the other hand is a special form where applicative order does not apply and so all args are not evaluated, thereby preventing infinite loops

## Question 2

```scm
;test input: (squares '(2 3 4 5))
;out: (4 9 16 25)

; requires simply-scheme's "every" function
(define (squares nums)
    (define (square x) (* x x))
    (every square nums)
)

; uses recursive function
(define (squares nums)
    (if (= (count nums) 0)
        '()
        (se (* (first nums) (first nums)) (squares (butfirst nums)))
    )
)
```

## Question 3

```scm
(define (switch sent beg)
    (cond
        ((= (count sent) 0)
            ""
        )

        ((= (count sent) 1)
            sent
        )

        ;if "you" & beginning of sentence, then replace with "I"
        ((= beg 0) 
            (if (equal? (first sent) "You") 
                (se 'I (switch (butfirst sent) 1))
                (se (first sent) (switch (butfirst sent) 1))
            )
        )

        ;if "you", then replace with me
        ((equal? (first sent) "you")
             (se 'me (switch (butfirst sent) 1))
        )

        ;if "I" or "me", then replace with "you"
        ((or (equal? (first sent) "I") (equal? (first sent) "me"))
            (se 'you (switch (butfirst sent) 1))
        )

        (else (se (first sent) (switch (butfirst sent) 1)))
    )
)

;input: (switch '(You told me that I should wake you up) 0)
;output: (i told you that you should wake me up)
```

## Question 4

```scm
(define (ordered nums)
    (if (= (count nums) 1)
        #t
        (and (< (first nums) (item 2 nums)) (ordered (butfirst nums)) )
    )
)

;input: (ordered '(2 3 4 5))
;output: #t
```

## Question 5

```scm
(define (ends-e sent)
    (if (= (count sent) 0)
        '()
        (if (equal? (last (first sent)) "e")
            (se (first sent) (ends-e (butfirst sent)))
            (se '() (ends-e (butfirst sent)))
        )
    )
)

;input: (ends-e '(please put the salami above the blue elephant))
;output: (please the above the blue)
```

## Question 6

skippppeeeeed!