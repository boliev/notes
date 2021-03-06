# alg-notes
## trees
### Traversal
 - Pre-order Traversal: ROOT-LEFT-RIGHT
 - In-order Traversal: LEFT-ROOT-RIGHT
 - Post-order Traversal: LEFT-RIGHT-ROOT
 - Level-order traversal: neighbors on each level. Breadth-First

```golang
func preorderTraversal(root *TreeNode) []int {
    var res []int
    if root == nil {
        return res
    }
    res = append(res, root.Val)
    if root.Left != nil {
        res = append(res, preorderTraversal(root.Left)...)
    }
    if root.Right != nil {
        res = append(res, preorderTraversal(root.Right)...)
    }
    
    return res
}
```

```golang
func inorderTraversal(root *TreeNode) []int {
    var ret []int
    if root == nil {
        return ret
    }
    if root.Left != nil {
        ret = append(ret, inorderTraversal(root.Left)...)
    }
    ret = append(ret, root.Val)
    if root.Right != nil {
        ret = append(ret, inorderTraversal(root.Right)...)
    }
    
    return ret
}
```

```golang
func postorderTraversal(root *TreeNode) []int {
    var res []int
    if root == nil {
        return res
    }
    
    if root.Left != nil {
        res = append(res, postorderTraversal(root.Left)...)
    }
    if root.Right != nil {
        res = append(res, postorderTraversal(root.Right)...)
    }
    res = append(res, root.Val)
    
    return res
}
```

```golang
func levelOrder(root *TreeNode) [][]int {
    var toProcess []*TreeNode
    var res []int
    toProcess = append(toProcess, root)
    for len(toProcess) > 0 {
        el := toProcess[0]
        if el.Left != nil {
            toProcess = append(toProcess, el.Left)
        }
        if el.Right != nil {
            toProcess = append(toProcess, el.Right)
        }
        res = append(res, el.Val)
        toProcess = toProcess[1:]
    }

    return res
}
```
### Solve Tree Problems Recursively
 - "Top-down" Solution. Value - then children
 - "Bottom-up" Solution. Children then value
 
### Tasks
#### tree max depth
```golang
func maxDepth(root *TreeNode) int {
    if(root == nil) {
        return 0
    }
    left := 0
    right := 0
    if root.Left != nil {
        left = maxDepth(root.Left)
    }
    if root.Right != nil {
        right = maxDepth(root.Right)
    }
    
    max := 0
    if left > right {
        max = left
    } else {
        max = right
    }
    
    return max + 1
}
```
#### Binary search
```golang
func searchBST(root *TreeNode, val int) *TreeNode {
    if root == nil || root.Val == val {
        return root
    }
    
    if val < root.Val {
        return searchBST(root.Left, val)
    }
    
    return searchBST(root.Right, val)
}
```
### construct trees
#### from preorder and postorder
The last element in postorder is the root
The elements on the left side of the root element in preorder - the left subtree
The elements on the right side of the root element in preorder - the right subtree
#### from preorder and inorder
The first element in preorder is the root
The elements on the left side of the root element in inorder - the left subtree
The elements on the right side of the root element in inorder - the right subtree
### tips
Root always appear in the end of postorder traversal array
### good examples
https://leetcode.com/explore/learn/card/data-structure-tree/133/conclusion/932/
https://leetcode.com/explore/learn/card/data-structure-tree/133/conclusion/995/

## Recursion
[Time Complexity](https://leetcode.com/explore/learn/card/recursion-i/256/complexity-analysis/1669/)
