### 题目

  二叉树中序遍历

### 思路

二叉树的中序遍历题目，一般有递归方式与非递归方式两种。这里不介绍递归方式，而是用栈的特性，来帮助我们完成遍历。

1. 维护一个栈 stackNodes 和一个当前节点 traversalNode。初始时将 traversalNode 赋值为根节点。

2. 将当前节点 traversalNode 的左子链上的节点逐个推入栈中，直到没有左儿子。

3. 取出栈顶的节点，访问该节点，将 traversalNode 赋值为该节点的右儿子。

4. 不断执行 2，3，直到栈为空且当前节点也为空。

### 代码示例

```java
private List<Integer> inorderTraversalV2(TreeNode root) {
    List<Integer> values = new ArrayList<>();
    Stack<TreeNode> stackNodes = new Stack<>();
    TreeNode traversalNode = root;
    while (traversalNode != null || !stackNodes.isEmpty()) {
        while (traversalNode != null) {
            stackNodes.add(traversalNode);
            traversalNode = traversalNode.left;
        }
        TreeNode currentNode = stackNodes.pop();
        values.add(currentNode.val);
        if (currentNode.right != null) {
            traversalNode = currentNode.right;
        }
    }
    return values;
}
```