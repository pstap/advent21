# Solution
## Part 1:

First working attempt
```apl
+/({⍵[1] < ⍵[2]}⌺2)⍎¨ ⊃ ⎕NGET '/home/peter/src/advent21/1/input'1
```

### Explanation
#### Subexpr 1: `⊃ ⎕NGET '/home/peter/src/advent21/1/input'1`
credit https://xpqz.github.io/learnapl/io.html for the referce on reading files

`⎕NGET` does the actual reading.
Called monadically with the path as the right argument

The 1 at the end of the pathname changes how the result is returned. 1 = each line is boxed, 0 (default) = 1 big char array

`⊃` takes the first element of NGET's output (the data)

#### Subexpr 2: `⍎¨`
Execute (`eval` in other languages) each (`¨`) line, producing a single array of numbers


#### Subexpr 3: `({⍵[1] < ⍵[2]}⌺2)`
take the array 2 elements at a time (with overlap) and evaluate the dfn (anonymous function) `{⍵[1] < ⍵[2]}` for each 2 element array.

the dfn returns booleans (0 or 1) for each 2 element array. 1 if the second element of the array is larger than the first

#### Subexpr 4: `+/`
sum the boolean array, returning the total count


## Part 2 Solution:
```apl
+/({⍵[1]<⍵[2]}⌺2) 3 {+/(⍺,⍵)} / ⍎¨⊃⎕NGET '/home/peter/src/advent21/1/input'1
```

Same as part 1 above but with the windowing added before Subexpr 3

Windowing: `3 {+/(⍺,⍵)} /`


### Improvements
`+/ 2 </ 3 {+/(⍺,⍵)} / ⍎¨⊃⎕NGET '/home/peter/src/advent21/1/input'1` N-wise (N=2) reduce with the dyadic `<`

`+/ 2 </ 3 +/ ⍎¨⊃⎕NGET '/home/peter/src/advent21/1/input'1` Replace the dfn for summing in the N-wise sum with monadic sum (+/) |



## NOTES:
From: https://aplwiki.com/wiki/Windowed_Reduce
>Stencil which can be seen as a generalisation of Windowed Reduce in that for a vector argument,
>({⊂f/⍵}⌺n)v is equivalent to n f/ v except in how they deal with the ends of the vector; Stencil includes "shards" and Windowed Reduce does not.
