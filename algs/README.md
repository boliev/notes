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