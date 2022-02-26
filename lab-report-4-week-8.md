# **Lab Report 4 Week 8**

## Snippet 1
Test for Snippet 1:
![snippet1Test](snippet1Test.png)
Snippet 1 on My Implementation: My implementation failed the test since it gave `url.com` when it should not have and did not give `ucsd.edu` when it should have.
![snippet1Mine](snippet1Mine.png)
Snippet 1 on Reviewed Implementation: The implementation I reviewed with my lab group failed the test since it gave a no links when it should have given ``google.com`, `google.com`, and `ucsd.edu`.
![snippet1Other](snippet1Other.png)

## Snippet 2
Test for Snippet 2:
![snippet2Test](snippet2Test.png)
Snippet 2 on My Implementation: My implementation failed the test since it gave `a.com((` when it was supposed to give `a.com(())`, and because it did not give `example.com` when it should have.
![snippet2Mine](snippet2Mine.png)
Snippet 2 on Reviewed Implementation: The implementation I reviewed with my lab group failed the test since it gave no links when it should have given `a.com`, `a.com(())`, and `example.com`.
![snippet2Other](snippet2Other.png)


## Snippet 3
Test for Snippet 3:
![snippet3Test](snippet3Test.png)
Snippet 3 on My Implementation: My implementation failed the test since it should have provided only `https://ucsd-cse15l-w22.github.io/` but gave more links than that. 
![snippet3Mine](snippet3Mine.png)
Snippet 3 on Reviewed Implementation: The implementation I reviewed with my group failed the test since it provided no links when it should have given `https://ucsd-cse15l-w22.github.io/`. 
![snippet3Other](snippet3Other.png)

## Code Changes
Code Changes for Snippet 1:
The code changes to make the program handle code blocks correctly would likely take under 10 lines. It would mostly involve having variables store the index position of the backticks starting and ending the code blocks. If there is only a single backtick, that means it is not a code block and could be processed like the rest of the lines. If there are 2 backticks found together, then the code would check the index of the backticks in relation to the index of the brackets and parenthesis. If the front codetick is found to be before the open bracket like in `url.com`, then it is counted as a code block and the code skips to the index of the end codetick + 1 and parses from there. If the front codetick is found to be inside the brackets but not the end codetick, then it is a codeblock and the code should skip to the index of end codetick +1 and parse from there. Since the changes would require only adding new instance variables to track index of backticks and if conditionals, I think it could be done under 10 lines.

Code Changes for Snippet 2:
My code incorrectly handles the nested parenthesis case and the escaped brackets case. To fix this I believe I would need more than 10 lines since I would need to create a helper method to find the corresponding end parenthesis of the open parenthesis beginning the link, and then I could print the link that is between them. The helper method would be like the one that Professor Politz displayed in his lectures which starts at an open parenthesis and then keeps looping through the text file until the openParenthesisCount is zero and then returns the index when openParenthesisCount hit 0. This method would be similar to Professor Politz's `findCloseParen(String markdown, int openParen)` method. To handle the escaped bracket case described by `[some escaped \[ brackets \]](example.com)`, I would add an if condition to make sure that there is not a `\` immediately before the `[` or `]` and if there is then depending on which bracket has the `\` in front it would handle the case differently. If `[` has the `\` before it then it would skip the text until it finds the next `[` without `\` in front. If `]` has a `\` in front then it would only need to find the next `]` without it and continue parsing from there. In the case of `[some escaped \[ brackets \]](example.com)`, it would see that `[` does not have a `\` in front so it would only need to find a `]` without `\` in front. These code changes would take more than 10 lines since the `findCloseParen` method takes a little more than 10 lines and adding the fixes for escaped brackets would push it further over. 

Code Changes for Snippet 3:
Snippet 3 tests for how my code would handle newlines within brackets and parenthesis. For the bracket case, I would write a helper boolean method `isConsecutiveNewLineBracket` containing a for-loop from the beginning bracket to the corresponding end bracket that checks if there are two consecutive new lines. If there are then the `isConsecutive` method returns `false`. I would also need to write another helper method for newlines between parenthesis called `newLineParenthesis` that checks the index of newLines between the parenthesis. If there is a newLine immediately after the `(` or immediately before the `)` then it is fine and returns true, or there are no newLines it would return true. Otherwise it returns false. I would add an if condition in `getLinks` that checks that both `isConsecutiveNewLineBracket` and `newLineParenthesis` are true and if they are false to set currentIndex to the index of the next open bracket and begin parsing from there. 