### 题目

Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, \*, /. Each operand may be an integer or another expression.

Some examples:

>  ["2", "1", "+", "3", "\*"] -> ((2 + 1) * 3) -> 9

>  ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6

### 思路

考察了逆波兰表达式的用法。操作数入栈；遇到操作符时，操作数出栈，求值，将结果入栈；当一遍后，栈顶就是表达式的值。

### 代码示例

```java
public class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();

        String operations = "+-*/";

        for (String item : tokens) {

          if (operations.contains(item)) {
            // 操作符
            int right = stack.pop();
            int left = stack.pop();

            if (item.equals("+")) {
              stack.push(left + right);
            } else if (item.equals("-")) {
              stack.push(left - right);
            } else if (item.equals("*")) {
              stack.push(left * right);
            } else if (item.equals("/")) {
              stack.push(left / right);
            }
          } else {
            // 操作数
            stack.push(Integer.valueOf(item));
          }
        }
        return stack.pop();
    }
}
```
