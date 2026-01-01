# CH1 Exercise Solutions

## CH 1.1

<details><summary>Exercise 1.1</summary>

```scm
10                                  ; 10
(+ 5 3 4)                           ; 12 
(- 9 1)                             ; 8
(/ 6 2)                             ; 3
(+ (* 2 4) (- 4 6))                 ; 6 
(define a 3)                        ;
(define b (+ a 1))                  ;
(+ a b (* a b))                     ; 19
(= a b)                             ; #f
(if (and                            ; 4
      (> b a) (< b (* a b))
    )     
      b
      a)
(cond ((= a 4) 6)                   ; 16
((= b 4) (+ 6 7 a))
(else 25))

(+ 2 (if (> b a) b a))              ; 6

(* (cond ((> a b) a)                ; 16
    ((< a b) b)
    (else -1))
(+ a 1))
```
</details>

<details><summary>Exercise 1.2</summary>

```scm
(/ (+ 5 4 (- 2 (- 3 (+ 6 (/ 4 5))))) (* 3 (- 6 2) (- 2 7))) ; -37/150
```
</details>

<details><summary>Exercise 1.3</summary>

```scm
(define (sumofsquares x y z) (+
    (*
      (cond ((> x y) (x)) (else y))
      (cond ((> x y) (x)) (else y))
    )
    (*
      (cond ((> y z) (y)) (else z))
      (cond ((> y z) (y)) (else z))
    )))
; ex: (sumofsquares 1 2 3) = 13
```
</details>

<details><summary>Exercise 1.4</summary>

```scm
(define (a-plus-abs-b a b)   ; function evaluates to (a+b) if b is positive, and (a-b) if b is negative
    ((if (> b 0) + -) a b)) 
```
</details>

<details><summary>Exercise 1.5</summary>

```scm
(define (p) (p))     ; causes infinite loop
(define (test x y)
  (if (= x 0) 0 y))
(test 0 (p))         ; applicative-order eval: result is infinite loop since (p) is eval. regardless of if stmt
                     ; normal-order eval: result should be 0
```
</details>

<details><summary>Exercise 1.6</summary>

```scm
; defining methods to allow exercise code snippet to work
(define (square x) (* x x))
(define (abs x) (cond ((> x 0) x) ((= x 0) 0) ((< x 0) (- x))))
(define (average x y) (/ (+ x y) 2))
(define (improve guess x) (average guess (/ x guess)))
(define (good-enough? guess x) (< (abs (- (square guess) x)) 0.001))
(define (sqrt-iter guess x) (if (good-enough? guess x) guess (sqrt-iter (improve guess x) x)))
(define (sqrt x) (sqrt-iter 1.0 x))

; Ex 1.6, modifying `sqrt-iter` to use a function to replace `if`
(define (new-if predicate then-clause else-clause)
  (cond (predicate then-clause)
  (else else-clause)))

(define (sqrt-iter guess x)
  (new-if (good-enough? guess x)
  guess
  (sqrt-iter (improve guess x) x)))

; evaluating the modified `sqrt-iter` will result in infinite loop since it uses a procedure in place of `if` which means all arguments are evaluated (with `if`, applicative order does not apply)
```
</details>

<details><summary>Exercise 1.7</summary>

- Skipped
- See [sicp-solutions](https://sicp-solutions.net/post/sicp-solution-exercise-1-7/) for detailed answer
</details>

<details><summary>Exercise 1.8</summary>

```scm
(define (cube x) (* x x x))
(define (improve3 guess x) (/ (+ (/ x (square guess)) (* 2 guess)) 3))
(define (good-enough3? guess x) (< (abs (- (cube guess) x)) 0.001))
(define (cube-iter guess x) (if (good-enough3? guess x) guess (cube-iter (improve3 guess x) x)))
(define (cubert x) (cube-iter 1.0 x))
```
</details>

## CH 1.2

<details><summary>Exercise 1.9</summary>

- Skipped, see [solution](https://sicp-solutions.net/post/sicp-solution-exercise-1-9/)
</details>

<details><summary>Exercise 1.10</summary>

- `(A 1 10)`: 1024
- `(A 2 4)`: 65536
- `(A 3 3)`: 65536
- `(define (f n) (A 0 n))`: 2n
- `(define (g n) (A 1 n))`: 2^n
- `(define (h n) (A 2 n))`: [see solution](https://sicp-solutions.net/post/sicp-solution-exercise-1-10/)
</details>



## CH 1.3

<details><summary>Exercise 1.29</summary>

- skipped!
</details>


<details><summary>Exercise 1.30</summary>

```scm
; term = computes the next iterative value in the sum (f(i) in summation)
; next = computes the next iteration (up to b) (i in summation)
(define (isum term a next b)
  (define (iter a result)
    (if (> a b)
      result
      (iter (next a) (+ result (term a)))
    )
  )
  (iter a 0)
)

; setup
(define (identity x) x)  ; term
(define (inc n) (+ n 1)) ; next
; test
(define (isum-integers a b) (isum identity a inc b))
(isum-integers 1 10) ; expected output: 55
```
</details>

<details><summary>Exercise 1.31</summary>

```scm
(define (identity x) x)
(define (inc x) (+ 1 x))

; product - recursive
(define (product term a next b)
  (if (> a b)
      1
      (* (term a) (product term (next a) next b))
  )
)

; product - iterative
(define (iproduct term a next b)
  (define (inner a result)
    (if (> a b)
        result
        (inner (next a) (* (term a) result))
    )
  )
  (inner a 1)
)

; 1*2*3*4*...*n
; test (factorial 1 5) = 120
(define (factorial a b)
  (iproduct identity a inc b)
)

; WALLIS FORMULA, NOT COMPLETED (INCORRECT)
(define (square x) (* x x))
(define (wallis-single n)
  (/
   (* 4 (square n))
   (- (* 4 (square n)))
  )
)

(define (wallis a b)
  (product wallis-single a inc b)
)
```
</details>

<details><summary>Exercise 1.32</summary>

```scm
; accumulation fx: (accumulate combiner null-value term a next b)
; combiner (arg): 
;   procedure of two args that specifies how the current term 
;   is to be combined with accumulation of the preceding terms
; null-value (arg): specifies what base value to use when the terms run out

; accumulator: recursive
(define (accumulate combiner null-value term a next b)
  (if (> a b)
      null-value
      (combiner (term a) (accumulate combiner null-value term (next a) next b))
  )
)

; accumulator: iterative
(define (iaccumulate combiner null-value term a next b)
  (define (iterate a result)
    (if (> a b)
        result
        (iterate (next a) (combiner (term a) result))
    )
  )
  (iterate a null-value)
)

; setup
(define (summation current next) (+ current next))
(define (pinotation current next) (* current next))
(define (identity x) x)  ; term
(define (inc n) (+ n 1)) ; next

; test
(accumulate summation 0 identity 1 inc 10) ; 55
(accumulate pinotation 1 identity 1 inc 5) ; 120
```
</details>

<details><summary>Exercise 1.33</summary>

_skipped!_
</details>


<details><summary></summary>

</details>