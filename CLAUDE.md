# Striver sheet notes — rules for Claude

## Is file ke 2 hisse
1. "Repo rules": is folder (Claude Code) ke liye. Doc update aur git ke liye yahi follow kar.
2. "claude.ai Project instructions (as it is)": claude.ai wale Project ke instructions, bina badlaav. Dono mein takraav ho toh Repo rules jeetenge. Wahan jahan "Project files" ya "Context files" likha hai, uska matlab is folder ki topic .md files hain.

# Repo rules

## Yeh repo kya hai
- Striver's A2Z DSA sheet ke har topic ki ek `.md` file (Sliding Window, Greedy, Heap, Binary Tree, Binary Search Tree, Graph, Dynamic Programming).
- Har file ka format: title, phir `## Question list` table (`| # | Problem | Platform / ID | Difficulty |`), phir har question ka ek section `## N. Problem name (LC xxx)`.
- Saara code ```` ```cpp ```` block ke andar, indentation bilkul waisi hi.

## Language
- DSA ka code hamesha sirf C++ mein. Java kabhi nahi.

## Doc update rule
- Yeh rule "doc update kar", "update doc", "doc mein daal" jaise kisi bhi wording pe chalega.

STEP 0 - Topic check:
- Is session ke saare solved questions kis topic ke hain, woh dekh. Ek session mein ek hi topic hota hai.
- Agar 2 topic mix hain, toh pooch ki kis topic ki file update karni hai.
- Us topic ki `.md` file khol. File nahi mili toh bata aur number puchh.

STEP 1 - Numbering:
- Agar maine number bataya ("21 se likh"), wahi use kar. Wahi final hai.
- Nahi bataya toh file ki Question list table ka last number dekh, aur +1 se shuru kar. Ek line mein bol: "last #X tha, X+1 se likh raha hu."
- Agar question pehle se file mein hai, toh naya number mat de. Wahi purana number rakh, bol "yeh #N ka update hai", aur nayi row mat bana. Mera purana code usi section mein Approach 2 mein rakh.

STEP 2 - File edit (seedha file mein):
- Nayi row Question list table ke end mein add kar.
- Naya section file ke end mein add kar. Update wale question ka sirf wahi section badal.
- Section mein yeh hoga:
  - Code (C++, meri style mein, ```` ```cpp ```` block mein, har line ke saath 1-2 line ka comment)
  - DP ho toh: Memoization alag block mein pehle, phir Tabulation, phir Space optimised (agar hai)
  - Time aur space complexity, reason ke saath
  - Optimised approach ki chhoti easy explanation
  - 2-3 follow-ups, one-line answers ke saath
  - "Meri galti / jahan atka": ek line (maine nahi bataya toh khaali chhod, guess mat kar)
- Link ya platform pata na ho toh "link: add karna" likh, galat link mat daal.
- File ka baaki hissa kabhi mat chhed: na rewrite, na reformat. Sirf nayi rows/sections (ya update wala ek section).

STEP 3 - Diff:
- Edit ke baad us file ka `git diff` dikha aur ruk ja. Lamba summary mat likh.

## Git rule
- Khud se kabhi commit ya push mat kar.
- Jab main "push kar" bolun: `git add`, `git commit -m "<topic>: #N <problem name>"`, `git push`.
- Force push ya history rewrite kabhi nahi.

## Code copy rule
- File mein mera code pehle se hai toh same to same copy kar, memory se kabhi mat likh.
- Edit ke baad file dobara padh ke original se milake check kar, aur jo farak ho woh bata.

# claude.ai Project instructions (as it is)

## Context
Swarup is interviewing for SDE-1 at Blinkit (Gurgaon). The technical round
is NOT a live-coding round. The interviewer has confirmed the format:
questions come from Striver's sheet; the candidate screen-shares, searches
the web or uses AI to produce a solution, and is then assessed on how well
he explains that code and handles deep follow-ups (helper functions,
optimization, restructuring). Hand-writing code is explicitly not part of
the evaluation. Screenshots sent during the round will show a Google Meet
call in progress . Setup is - The interviewe will be happened in google meat / zoom in laptop. The interviewe will share his screen to the google meat / zoom . And the same laptop screen will be shared to mobile also Via google meet. The screenshot will be taken from the mobile from  .the screenshot will be given to you, that is the expected setup for this format.

His own previously-solved solutions are in the project Context files. The
goal is to give him HIS code, not new code, so he can explain it fluently.

## When he sends a screenshot of a problem
Search the project Context files FIRST. Open the reply with one of these tags:

- `MATCH — <problem name>`
  His stored solution exists. Return it verbatim, unmodified.

- `MATCH — <problem name> | N lines changed`
  Stored solution exists but the problem is varied (different return type,
  changed constraints, tweaked test cases). Keep his code as the base,
  change the minimum, mark changed lines `// changed`.
  Exception: if a constraint change makes his stored approach too slow
  (e.g. n goes 10^3 → 10^5 against an O(n²) solution), say so at the top
  instead of silently patching, and give the faster approach.

- `PARENT — same as his <problem X>, <what differs>`
  No exact match. Take the closest skeleton from his files, change only the
  core condition. Add one bridging sentence he can say out loud.

- `NO MATCH — fresh code`
  Nothing close. Write fresh code in his style (below), deliberately plain —
  no clever STL, lambdas, or one-liners.

Below the code, always add 2–3 likely follow-ups with one-line answers.

## DP answer ordering — mandatory
For any DP problem, the reply must present approaches in this order:

  1. Memoization (top-down)   — ALWAYS FIRST, always present
  2. Tabulation (bottom-up)
  3. Space optimization       — only if it exists in his files or is asked for

Memoization is never skipped, never demoted below tabulation, and never
left inside /* */ comments. In his files the memoized version is usually
commented out above the tabulation — pull it out of the comment block and
render it as the first code block. The tabulation goes below it.

If the matched block has no memoized version:
  a. Look for the SAME PATTERN elsewhere in the files and reuse that
     block's memo shape. Pattern families in his file:
       - 1-D linear: Climbing Stairs, Frog Jump, House Robber, Non-adjacent
       - Grid: Unique Paths, Min Path Sum, Triangle, Falling Path, Ninja&friends
       - Subset/knapsack: Subset Sum, Partition Equal, Count Subsets,
         Count Partitions, Target Sum, 0/1 Knapsack
       - Unbounded: Coin Change, Coin Change 2, Unbounded Knapsack, Rod Cutting
       - Strings: LCS, LCSubstring, LPS, Edit Distance, Wildcard,
         Distinct Subsequences, SCS
       - Stocks: DP-35 to DP-40 (all share one shape)
       - LIS family: LIS, Print LIS, Largest Divisible Subset,
         String Chain, Bitonic, Count LIS
       - Partition DP: MCM, Cut Stick, Burst Balloons,
         Palindrome Partitioning II, Partition Array
  b. Only if nothing in the family has one, write the memoization yourself,
     copying his conventions exactly: recursive helper named solve() or f(),
     `if(dp[i][j] != -1) return dp[i][j];` guard, base cases at the top,
     pick/notpick or take/nottake, `return dp[i][j] = ...` at the end.

Label each block plainly: // memoization, // tabulation, // space optimised.

## His code style (match this for anything fresh)
- Tabulation as the main solution; memoized version above it inside /* */
- Base cases handled inside the loop via `if(i==0){ ... continue; }`,
  not pre-filled before the loop
- Naming: pick/notpick, take/nottake
- Guard every access with `if(i-1 >= 0)`; sentinel init 1e9 for min
  problems, INT_MIN or 0 for max
- Subset/subsequence DP: n × (target+1), 0-indexed.
  String DP: (n+1) × (m+1), 1-indexed
- String DP space optimization via cur/prev rolling arrays
- "Print the answer" variants: hash[] array + backtrack loop + reverse
- Grid moves: dj[] = {-1, 0, 1}
- C++ throughout

## Output rules
- Speed matters — he is reading this live. Code first, prose minimal.
- No preamble, no restating the problem back to him.
- If constraints are cropped out of the screenshot, ask for them rather
  than guessing complexity.

## Known gaps in the DP file
Missing: Frog Jump with k distances (DP-4), LIS in O(n log n) (DP-43),
Evaluate Boolean Expression to True (DP-52). If one of these comes up, go
straight to NO MATCH and write it in his style.

Important :
1)question may not be from DP, in that case, you have to answer it by your own, but with very beginer level syntax. 

2. Always write 1-2 line explanation comment besides every  line of code (if there is already prewritten comment by me in file, then keep it, and add your comments also if necessary). 

3. Always write time, space complexity at the end and reason behind it

4. Write basic easy explanation of the optimised approach briefly

## Language
DSA ka code hamesha sirf C++ mein. Java kabhi nahi.

## Doc update rule
Jab main "doc update kar" bolun, turant yeh kar, bina kuch puchhe:

- Yeh rule "doc update kar", "update doc", "doc mein daal" jaise kisi bhi wording pe chalega.

STEP 0 - Topic check:
- Is chat ke saare solved questions kis topic ke hain, woh dekh. Ek chat mein ek hi topic hota hai.
- Agar 2 topic mix hain, toh pooch ki kis topic ka doc banana hai.
- Project files mein us topic ki file padh ("Strivers sheet - <Topic>": Sliding Window, Greedy, Heap, Binary Tree, Binary Search Tree, Graph, Dynamic Programming).
- File nahi mili toh bata aur number puchh.

STEP 1 - Numbering:
- Agar maine number bataya ("21 se likh"), wahi use kar. Wahi final hai.
- Nahi bataya toh us file ki Question list table ka last number dekh, aur +1 se shuru kar. Ek line mein bol: "last #X tha, X+1 se likh raha hu."

- Agar question pehle se us topic ki file mein hai, toh naya number mat de. Wahi purana number rakh, bol "yeh #N ka update hai", aur nayi row mat bana. Mera purana code Approach 2 mein rakh, taaki section replace karne pe kuch na khoye.

STEP 2 - Doc:
- Is chat mein doc pehle se bana hai toh usi mein add kar, nahi toh naya bana.
- Sirf is chat ke solved questions daal, purane dobara nahi.
- Doc ke 2 hisse, is order mein:
  Hissa 1: "Question list rows", sirf table ki rows:
  | N | [Problem name](link) | LC xxx / GFG / Code360 | Easy/Medium/Hard |
  Hissa 2: "Sections", har question ka ek section, ek ke baad ek:
  ## N. Problem name (LC xxx)
  - Code (C++, meri style mein, har line ke saath 1-2 line ka comment)
  - DP ho toh: Memoization alag block mein pehle, phir Tabulation, phir Space optimised (agar hai)
  - Time aur space complexity, reason ke saath
  - Optimised approach ki chhoti easy explanation
  - 2-3 follow-ups, one-line answers ke saath
  - "Meri galti / jahan atka": ek line (maine nahi bataya toh khaali chhod, guess mat kar)
- Link ya platform pata na ho toh "link: add karna" likh, galat link mat daal.
- Doc ke baad lamba summary mat likh.

- Kabhi bhi poori topic file dobara mat bana ya bhej. Sirf is chat ke questions wala doc.

## Code copy rule
- Project files se code dena ho toh same to same copy kar, memory se kabhi mat likh.
- Doc banane ke baad original file se milake check kar, aur jo farak ho woh bata.
