# Day 3

## Part 1
session

```apl
      ↑ ⊃ ⎕NGET '/home/peter/src/advent21/3/input'1
      ex
00100
11110
10110
10111
10101
01111
00111
11100
10000
11001
00010
01010

      gamma ← {2⊥>/[1]+/[2]'10'∘.=⍵}
      epsilon ← {2⊥</[1]+/[2]'10'∘.=⍵}

      gamma ex
22
      epsilon ex
9
      (epsilon×gamma) ex
198
      (epsilon×gamma) data
693486
```

## Part 2

obit returns the most common bit in position alpha of omega

cbit returns the least common bit in the position alpha of omega

```apl
obit ← {⍕ ⍺ ⊃ ≥/[1]+/[2]'10'∘.= ⍵}
cbit←{⍕⍺⊃</[1]+/[2]'10'∘.=⍵}
```

obit should be applied in a loop with increasing
index positions and filtering

```apl
 oxygen←oxy log;bit;bits;wset
 bit←1
 wset←log

 :While 1≢⊃⍴wset
     wset←((bit obit wset)=wset[;bit])/[1]wset
     bit←bit+1
 :EndWhile

 oxygen←2⊥2⊥⍎¨wset
 
 carbon←co2 log;bit;bits;wset;lc
 bit←1
 wset←log

 :While 1≢⊃⍴wset
     wset←((bit cbit wset)=wset[;bit])/[1]wset
     bit←bit+1
 :EndWhile

 carbon←2⊥2⊥⍎¨wset
```

The answer
```apl
(oxy×co2) data
```

## Notes
I don't see why I need to decode twice on the return of the oxy and c02 functions
