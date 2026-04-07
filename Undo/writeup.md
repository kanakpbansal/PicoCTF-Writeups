# <div align="center">[Undo](https://play.picoctf.org/practice/challenge/766)</div>
<div align="center">General CLI skills</div>
<br>


# Task 1. Challenge
Can you reverse a series of Linux text transformations to recover the original flag?
Start searching for the flag here nc foggy-cliff.picoctf.net 57528

> Flag

After typing the given command in my CLI i got the following output: 
```
===Welcome to the Text Transformations Challenge!===

Your goal: step by step, recover the original flag.
At each step, you'll see the transformed flag and a hint.
Enter the correct Linux command to reverse the last transformation.

--- Step 1 ---
Current flag: KW9zOHIwMG5uLWZhMDFnQHplMHNmYTRlRy1nazNnLXRhMWZlcmlyRShTR1BicHZj
Hint: Base64 encoded the string.
Enter the Linux command to reverse it:
```
I entered: `base64 -d`

Output:
```
Correct!

--- Step 2 ---
Current flag: )os8r00nn-fa01g@ze0sfa4eG-gk3g-ta1ferirE(SGPbpvc
Hint: Reversed the text.
Enter the Linux command to reverse it:
```

The answer was `rev`

Output:
```
Correct!

--- Step 3 ---
Current flag: cvpbPGS(Eriref1at-g3kg-Ge4afs0ez@g10af-nn00r8so)
Hint: Replaced underscores with dashes.
Enter the Linux command to reverse it:
```
I typed : `tr "-" "_"`

Output:
```
Correct!

--- Step 4 ---
Current flag: cvpbPGS(Eriref1at_g3kg_Ge4afs0ez@g10af_nn00r8so)
Hint: Replaced curly braces with parentheses.
Enter the Linux command to reverse it:
```
Answer: `tr "()" "{}"`

Output:
```
Correct!

--- Step 5 ---
Current flag: cvpbPGS{Eriref1at_g3kg_Ge4afs0ez@g10af_nn00r8so}
Hint: Applied ROT13 to letters.
Enter the Linux command to reverse it:
```
Finally I typed : `tr "A-Za-z" "N-ZA-Mn-za-m"`

Output:
```
Correct!

Congratulations! You've recovered the original flag:
>>> picoCTF{Revers1ng_t3xt_Tr4nsf0rm@t10ns_aa00e8fb}
```

Answer : 

```
picoCTF{Revers1ng_t3xt_Tr4nsf0rm@t10ns_aa00e8fb}
```


<br>

# 🧠 Summary
- Reversed multiple transformations step-by-step using Linux commands
- Used base64 -d to decode Base64 encoded text
- Used rev to reverse the string
- Used tr to replace characters (- ↔ _, () ↔ {})
- Applied ROT13 using tr "A-Za-z" "N-ZA-Mn-za-m"
- Successfully reconstructed the original flag

<br>
