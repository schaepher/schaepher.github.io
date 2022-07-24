# 打印二叉树


## 背景

之前在了解二叉树旋转的时候，为了方便查看中间状态，就写了个以树状形式打印二叉树的函数。

起初是使用二叉树中序遍历的结果展开的方式，简单但打印出来的树有一定的倾斜。

<!-- more -->

例如这棵树：

```
  5
 3  7
2  6 8
```

它的中序遍历结果为：

```
+++++++++++++
|2|3|5|6|7|8|
+++++++++++++
```

打印出来的结果中，节点 3 和节点 7 不是对称的。因为节点 3 距离其父节点 5 的距离只有 1，而节点 7 距离其父节点 5 的距离则是 2。

于是做了一番改造，打印了对称的树：

```
   5
 3   7
2   6 8
```

对应的数组是：

```
+++++++++++++
|2|3| |5|6|7|8|
+++++++++++++
```

## 中序遍历

这里改成返回遍历结果而不是直接打印。

```go
// InorderIteration 中序遍历迭代法
func InorderIteration(root *TreeNode) []*TreeNode {
	rs := make([]*TreeNode, 0)
	stack := make([]*TreeNode, 0)
	for len(stack) != 0 || root != nil {
		for root != nil {
			stack = append(stack, root)
			root = root.Left
		}

		root = stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		rs = append(rs, root)

		root = root.Right
	}

	return rs
}
```

## 基于中序遍历结果的展开

```go
// PrintTree 以中序遍历结果展开树
func PrintTree(root *TreeNode) {
	if root == nil {
		return
	}
	inorder := InorderIteration(root)

	row := []*TreeNode{root}
	var cache []*TreeNode
	for len(row) != 0 {
		// 每次取一整行出来，并重新申请空间存放下一行
		cache = row
		row = make([]*TreeNode, 0)

		// 从中序遍历中寻找当前行的数据，不匹配的打印空格
		i := 0
		for _, node := range inorder {
			if node.Value != cache[i].Value {
				fmt.Print(" ")
			} else {
				fmt.Print(node.Value)
				i++
				if i == len(cache) {
					break
				}
			}
		}
		fmt.Println()

		for _, node := range cache {
			if node.Left != nil {
				row = append(row, node.Left)
			}
			if node.Right != nil {
				row = append(row, node.Right)
			}
		}
	}
}
```

## 补全空位置的打印

借鉴中序遍历展开的思路。根据树的高度，申请一个可以容纳这个高度满节点状态的节点数量的数组。从根节点开始，宽度优先遍历。让每个节点都把一个范围平均分成两部分。

为了方便，这里先展示具有破坏性的打印。破坏的地方为 Node 的 Height 属性。在打印时，会发生变化。如果不想破坏，则再增加一个 Layer 属性即可。

```go
func PrintTree(root *TreeNode) {
	// 把子节点的高度更新为父节点高度-1
	UpdateHightToMax(root)
	data := ToStrictInorderArray(root)
	height := root.Height
	for height > 0 {
		// 每次遍历完整的中序遍历结果，当元素的层级与当前层级相同时打印值，不同时打印空格
		for _, element := range data {
			if element == nil || element.Height != height {
				fmt.Print(" ")
			} else {
				fmt.Printf("%d", element.Value)
			}
		}
		height--
		fmt.Println()
	}
}

// UpdateHightToMax 前序遍历更新高度，把子节点的高度更新为父节点高度-1
func UpdateHightToMax(root *TreeNode) {
	stack := make([]*TreeNode, 0)
	for len(stack) != 0 || root != nil {
		for root != nil {
			if root.Parent != nil {
				root.Height = root.Parent.Height - 1
			}
			stack = append(stack, root)
			root = root.Left
		}

		node := stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		root = node.Right
	}
}

// ToStrictInorderArray 对称的树
func ToStrictInorderArray(root *TreeNode) []*TreeNode {
	if root == nil || root.Height < 0 {
		return make([]*TreeNode, 0)
	}

	// 总节点数为 (2^n)-1
	result := make([]*TreeNode, (1<<root.Height)-1)

	// 确保操作下一层节点时，父节点已放入结果集
	queue := BreadthFirstIteration(root)

	// root 的位置无法从父节点算出，先算出来
	index := 1<<(root.Height-1) - 1
	result[index] = queue[0]
	queue = queue[1:]

	for len(queue) > 0 {
		iterNode := queue[0]
		queue = queue[1:]

		distance := 1 << (iterNode.Height - 1)

		idx := FindIndexStrictInorder(result, iterNode.Parent)
		if iterNode.Value < iterNode.Parent.Value {
			idx -= distance
		} else {
			idx += distance
		}

		result[idx] = iterNode
	}

	return result
}

// BreadthFirstIteration 广度优先遍历
func BreadthFirstIteration(node *TreeNode) []*TreeNode {
	data := []*TreeNode{node}
	for index := 0; index < len(data); index++ {
		node = data[index]
		if node.Left != nil {
			data = append(data, node.Left)
		}
		if node.Right != nil {
			data = append(data, node.Right)
		}
	}
	return data
}

// FindIndexStrictInorder 在数组中找到指定节点的位置
func FindIndexStrictInorder(tree []*TreeNode, node *TreeNode) int {
	cut := (len(tree) + 1) >> 1
	middle := cut - 1
	for cut > 1 && middle <= len(tree) {
		cut = cut >> 1
		if node.Value < tree[middle].Value {
			middle -= cut
		} else if node.Value > tree[middle].Value {
			middle += cut
		} else {
			return middle
		}
	}

	return middle
}
```

