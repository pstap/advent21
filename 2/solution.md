# Day 2
this one is bad

## Part 1

Read input
```apl
⊃ ⎕NGET '/home/peter/src/advent21/2/input'1
```

Read input and parse into a 2 column matrix of chars and numbers.
```apl
data ← ↑ {(⊃⊃⍵[1]),(⍎⊃⍵[2])}¨ {' ' (≠⊆⊢) ⍵}¨ ⊃ ⎕NGET '/home/peter/src/advent21/2/input'1
```

Example of data:

```
       16 ↑ data
f 4
d 8
d 3
d 1
f 8
u 6
d 4
f 2
d 4
d 6
d 7
f 1
d 4
d 6
f 7
d 2
       ⍴ 16 ↑ data
16 2
```

Makes some binary masks for each type
```
      fs ← 'f' = data[;1]
      ds ← 'd' = data[;1]
      us ← 'u' = data[;1]
```
 
Calculate
```
forward ← +/+/¨ fs ⊆ data[;2]
up ← ¯1 × +/+/¨ us ⊆ data[;2]
down ← +/+/¨ ds ⊆ data[;2]
forward × up+down
1648020
```
This solution is quite straightforward.

Could be cleaned up with getting rid of some layers of nesting.
Can we lookup a complex number by 'fud' then multiply and add? Inner product?
```
(complex directions) * (magintudes) = complex
(real complex) * (imaginary complex) 
```

## Part2

take the aim and do a `+\` to get the aim at each point.

then you can do a mulitply reduce.

```
      fs ← 'f' = data[;1]
      us ← - 'u' = data[;1]
      ds ← 'd' = data[;1]
      angle ← +\ data[;2] × us+ds
```

get all the forwards. multiply by 0 to make none of these have an effect
```
⍝ total forward distance
f ← +/ fs × data[;2]

⍝ answer
forward × +/ angle × fs × data[;2]
```


## notes
`/` should be used for filtering with `=`.  Partition with unboxing is messy
