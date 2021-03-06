# **Lab Report 2 Week 4**

## Code Change 1: Fixing Infinite While Loop Caused by `)` Not Being the Last Character of the File
Fix for Infinite While Loop Caused by `)` Not Being the Last Character: ![infiniteWhileLoopFix](infiniteWhileLoopFix.png)

Link to Failure-Inducing Input: [https://github.com/jwong1209/markdown-parse/blob/c0518531ee48080ba5e5c76d54f7290ab257f3be/test-file2.md](https://github.com/jwong1209/markdown-parse/blob/c0518531ee48080ba5e5c76d54f7290ab257f3be/test-file2.md)

Symptom of Failure-Inducing Input: 
![Infinite While Loop](infiniteWhileLoop.png)

Explanation: The bug is the code `currentIndex = closeParen + 1` which will reset the `currentIndex` back to the last parenthesis's index. This is an issue because if the last `)` is not at the end of the file as in the case of `test-file2.md`, then the condition `currentIndex < markdown.length()` would never be fulfilled and thus cause the while loop to keep repeating and the code in the body of the loop to keep traversing through the file. This is an infinite loop and the symptom of the bug. This bug is fixed by checking if one of the variables is equal to -1 and doing `return toReturn` if true because at least one of the variables will be -1 if you tried to find the indexOf a bracket(`[` and `]`) or parenthesis(`(` and `)`) during one of the while loop's faulty iterations since those iterations calls the method `indexOf()` from currentIndex which is past the last `)`'s index.

## Code Change 2: Fixing Code Giving Images as Links
Fix for Code Giving Images as Links: ![imageGivenFix](imageGivenFix.png)

Link to Failure-Inducing Input: [https://github.com/jwong1209/markdown-parse/blob/c0518531ee48080ba5e5c76d54f7290ab257f3be/test-file4.md](https://github.com/jwong1209/markdown-parse/blob/c0518531ee48080ba5e5c76d54f7290ab257f3be/test-file4.md)

Symptom of Failure-Inducing Input:
![imageGiven](imageGiven.png)

Explanation: The bug is that the code only uses the index of the brackets(`[` and `]`) and parenthesis(`(` and `)`) to decide what is a link or not. Since the format for an image is similar to the format for a link with its use of brackets and parenthesis, this causes the code to identify images as links such as `cat.png` and `cow.png` from the `test-file4.md` file and add them to `toReturn`, which gets printed and this is the symptom. To fix this bug, I used exclamation marks as the differentiator between images and links since image format has that at the start so if a `[` had a `!` in front of it, then it would mean its an image. This was done through having the `if` condition `(nextOpenBracket == 0 || markdown.indexOf("!", nextOpenBracket-1) != nextOpenBracket-1)` which would evaluate to false if there was a `!` in front of the `[` and would thus not execute the code in the body of the if statement, `toReturn.add(markdown.substring(openParen + 1, closeParen))`.

## Code Change 3: Fixing Code Giving Links When Characters Exist Between `]` and `(`
Fix for Code Giving Link Despite Characters Existing Between Bracket and Parenthesis:
![gapNotLinkFix](gapNotLinkFix.png)

Link to Failure-Inducing Input: 
[https://github.com/jwong1209/markdown-parse/blob/c0518531ee48080ba5e5c76d54f7290ab257f3be/professorFile5.md](https://github.com/jwong1209/markdown-parse/blob/c0518531ee48080ba5e5c76d54f7290ab257f3be/professorFile5.md)

Symptom of Failure-Inducing Input:
![gapNotLink](gapNotLink.png)

Explanation: The bug is that the code only looks at where the `[` is and then the `]` and then the `(` and then the `)` is but does not take into account the distance between the `]` and`(`. That means even though in `professorFile5.md` there are characters between the `]` and `(`, the code still adds `page.com` to `toReturn` as if it were a correctly formatted link when it should not, and this gets printed and that is the symptom. The fix for this bug was adding code to check that the `]` and `(` were right next to each other by adding `(openParen - nextCloseBracket == 1)` into the condition of the if statement and therefore the body of the if statement, `toReturn.add(markdown.substring(openParen + 1, closeParen))`, would not get executed if the distance between `openParen` and `nextCloseBracket` was greater than 1 meaning there were characters between them. 