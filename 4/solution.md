# Day 4

## Part 1
Read data dropping metadata
```apl
data ← ⊃ ⎕NGET '/home/peter/src/advent21/4/example'1
```

Parse first line into an array
```apl
nums ← ⍎¨(','∘≠⊆⊢) ⊃data
```

Read the rest of the data into a brick
```apl
games ← ↑{↑⍎¨⍵}¨(''∘≢¨⊆⊢) 2↓data
```

Wrapped up into a nice parsing dfn
```apl
parse←{
    nums←⊂⍎¨(','∘≠⊆⊢)⊃data
    games←⊂↑{↑⍎¨⍵}¨(''∘≢¨⊆⊢)2↓⍵
    nums,games
}
```

### Game logic
Score a game. 

Determine any winning rows

Determine any winning columns
```apl
scoreBoard ← +⌿⍤(∘.=)
winRow ← ∨/5=(+/⍤2)⍤scoreBoard
winCol ← ∨/5=+/[2]⍤scoreBoard
win ← winRow∨winCol
sumUnmarked ← {+/,⍵×(~+⌿⍺∘.=⍵)}
```

### Artisan Solution
I gave the computer a break and looked for the result myself.

Taking the scan of all nums, I searched for a Winner
```apl
⍸∨/¨{⍵ win games}¨,\num
```
This showed the first winner happened after pulling 34 numbers

I then looked at the state of each board after drawing 34 numbers, and saw that the 8th board was a winner
```apl
({⍵ win games}¨,\nums)[34]
```

I then calculated the answer with the functions above
```apl
      (34 ↑ nums) sumUnmarked games[8;;]
330
      ⊃⌽34↑nums
26
      26×330
8580
```
## Part 2

Which board wins last? Using the same logic above to look for a single win, we can look for the boards where all win. After drawing 82 numbers, not all boards have won, but after 83, all have.


We can find which game was the last to win by marking with the 82 numbers, and finding the game which didn't win (game 69)
```apl
      ⍸∧/¨({⍵ win games}¨,\nums)
83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100
      ⍸⊃~({⍵ win games}¨,\nums)[82]
69
      (82↑nums) scoreBoard games[69;;]
1 1 1 0 1
0 1 0 1 1
1 0 1 1 1
1 1 1 1 0
1 1 0 1 1
      ⍝ wins now
      (83↑nums) scoreBoard games[69;;]
1 1 1 0 1
0 1 0 1 1
1 0 1 1 1
1 1 1 1 0
1 1 1 1 1
      (83↑nums) sumUnmarked games[69;;]
228
      ⊃⌽83↑nums
42
      228×42
9576
```
