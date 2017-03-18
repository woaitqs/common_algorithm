### 题目

  > Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

  题目大意是，给出一个包含 '(', ')', '{', '}', '[' 和 ']' 的字符串，判断这个字符串是否符合数学常识，也就是是否成双成对。

### 解答：

  利用栈的特性，将属于带有左性质(左小括号，左大括号等等)的符号入栈，当遇到右性质的符号就出栈，同时比较两个符号是否成对。

### 代码示例

```java
public boolean isValid(String s) {

    if (s == null || s.isEmpty()) {
        return true;
    }

    Stack<Character> characters = new Stack<>();

    for (char item : s.toCharArray()) {
        if (item == '(' || item == '{' || item == '[') {
            characters.push(item);
        } else {
            if (characters.isEmpty()) {
                return false;
            }

            char top = characters.pop();
            switch (item) {
                case ')':
                    if (top != '(') {
                        return false;
                    }
                    break;
                case '}':
                    if (top != '{') {
                        return false;
                    }
                    break;
                case ']':
                    if (top != '[') {
                        return false;
                    }
                    break;
                default:
                    return false;
            }
        }
    }
    return characters.isEmpty();
}
```