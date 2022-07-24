# 平衡二叉树


上一篇把树旋转了解清楚，是为这一篇平衡二叉树准备的。

平衡二叉树，就是在二叉树的基础上加上一个条件：对于任意节点，左子树和右子树的树高之差不超过 1。

从实现的角度看，就是在已具备旋转功能的 Node 上增加一个 height 字段，并且在原先的代码上增加对 height 的操作。关键操作是判断左右子树的树高之差，根据树高之差选择需要执行的旋转。

<!-- more -->

## 示例

![](balanced-binary-tree-1.svg)

如图所示，这是一颗高为 3 的树。根节点左右两边的高度差为 1，满足平衡条件。

此时插入一个值为 1 的节点来破坏这个平衡。当节点 1 插入后，需要逐级往上更新节点的高度。

![](balanced-binary-tree-2.svg)

在高度更新后，发现根节点左右两边的高度差为 2，因此需要通过右旋调整平衡。节点 3 是转轴，按照旋转的规则执行。得到以下结果：

![](balanced-binary-tree-3.svg)

基本思路很简单。剩下的问题放到后面的内容处理。

以下内容会以可旋转的二叉排序树的代码（前篇文章的内容）为基础，添加 Height 这一属性。并根据树高的要求调整代码。

## 可旋转的二叉排序树

以下是原始代码，不难。与上一篇文章不同的是把 PutChild 改为 Insert，还有简化了旋转的代码。

```go
package main

import "fmt"

type TreeNode struct {
	Parent *TreeNode

	Value  int

	Left   *TreeNode
	Right  *TreeNode
}

// Insert 往树中合适位置插入节点
func Insert(root *TreeNode, value int) *TreeNode {
	if root == nil {
		return &TreeNode{Value: value}
	}

	if value < root.Value {
		root.Left = Insert(root.Left, value)
		root.Left.Parent = root
	} else if value > root.Value {
		root.Right = Insert(root.Right, value)
		root.Right.Parent = root
	} else {
		return root
	}

	return root
}

// RotateRight 右旋
func RotateRight(root *TreeNode) *TreeNode {
	if root.Left == nil {
		return root
	}

	newRoot := root.Left
	tmp := newRoot.Right
	newRoot.Right = root
	root.Left = tmp

	if tmp != nil {
		tmp.Parent = root
	}
	newRoot.Parent = root.Parent
	root.Parent = newRoot

	return newRoot
}

// RotateLeft 左旋
func RotateLeft(root *TreeNode) *TreeNode {
	if root.Right == nil {
		return root
	}

	newRoot := root.Right
	tmp := newRoot.Left
	newRoot.Left = root
	root.Right = tmp

	if tmp != nil {
		tmp.Parent = root
	}
	newRoot.Parent = root.Parent
	root.Parent = newRoot

	return newRoot
}

// PrintTree 以树状形式打印树
func PrintTree(root *TreeNode) {
	// 这里先不管
}

func main() {
	var root *TreeNode
	root = Insert(root, 7)
	root = Insert(root, 3)
	root = Insert(root, 2)
	root = Insert(root, 5)
	root = Insert(root, 8)
	PrintTree(root)
	fmt.Println("------------")

	root = RotateLeft(root)
	PrintTree(root)
	fmt.Println("------------")

	root = RotateRight(root)
	PrintTree(root)
	fmt.Println("------------")
}
```

## 添加 Height 参数

```go
type TreeNode struct {
	Parent *TreeNode
	
	Value  int
	Height int

	Left   *TreeNode
	Right  *TreeNode
}

func NewTreeNode(value int) *TreeNode {
	return &TreeNode{Value: value, Height: 1}
}
```

因为每次插入的节点都是作为叶子节点，所以新节点的树高都为 1。这里新增 New 函数，在初始化时自动指定。

## 检测树平衡

在修改的时候才需要检测树平衡，因此需要关注三个操作：插入、旋转、删除。这里忽略删除的部分，仅关注插入和旋转。

原始代码：

```go
func Insert(root *TreeNode, value int) *TreeNode {
	if root == nil {
		return &TreeNode{Value: value}
	}

	if value < root.Value {
		root.Left = Insert(root.Left, value)
		root.Left.Parent = root
	} else if value > root.Value {
		root.Right = Insert(root.Right, value)
		root.Right.Parent = root
	} else {
		return root
	}

	return root
}
```

每次插入一个叶子节点，有可能使其父节点树高增加，因此必须更新其父节点的树高。接着由于父节点树高的更新，需要再更新上一层树高，直到根节点。

由于 Insert 是递归调用，在递归下面写插入完成后的代码。分为两部分：1. 更新当前节点的树高；2. 如果左右子树树高相差超过 1，则通过旋转平衡该树。

首先第一部分，更新树高。

由于左右子树高度不一定一致，所以要取较高的那一颗子树的树高，加上 1 就是以当前节点作为根节点的子树的高度。

```go
func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}

// GetHeight 用来处理节点为 nil 的情况
func GetHeight(node *TreeNode) int {
	if node == nil {
		return 0
	}

	return node.Height
}

func Insert(root *TreeNode, value int) *TreeNode {
	// ...

	root.Height = max(GetHeight(root.Left), GetHeight(root.Right)) + 1

	return root
}
```

接着第二步，判断树平衡。

引入一个函数来获取平衡因子。当平衡因子小于 -1 的时候，表示右边的子树比左边高大于 1，此时应该左旋。反之，平衡因子大于 1 的时候表示应该右旋。

```go
// GetBalanceFactor 获取平衡因子
func GetBalanceFactor(node *TreeNode) int {
	if node == nil {
		return 0
	}

	return GetHeight(node.Left) - GetHeight(node.Right)
}

func Insert(root *TreeNode, value int) *TreeNode {
	// ...

	root.Height = max(GetHeight(root.Left), GetHeight(root.Right)) + 1

	bf := GetBalanceFactor(root)
	if bf < -1 { // 应该左旋
		root = RotateLeft(root)
	} else if bf > 1 { // 应该右旋
		root = RotateRight(root)
	} else {
		// do nothing
	}

	return root
}
```

## 旋转时更新树高

这里要先更新原先 root 节点的树高，因为旋转后它是 newRoot 的子节点。总是要按照先子节点再父节点的顺序更新树高。

另外由于 tmp 子树本身没有修改，因此不需要更新树高。

```go
// RotateRight 右旋
func RotateRight(root *TreeNode) *TreeNode {
	// ...

	root.Height = max(GetHeight(root.Left), GetHeight(root.Right)) + 1
	newRoot.Height = max(GetHeight(newRoot.Left), GetHeight(newRoot.Right)) + 1

	return newRoot
}

// RotateLeft 左旋
func RotateLeft(root *TreeNode) *TreeNode {
	// ...

	root.Height = max(GetHeight(root.Left), GetHeight(root.Right)) + 1
	newRoot.Height = max(GetHeight(newRoot.Left), GetHeight(newRoot.Right)) + 1

	return newRoot
}
```

## 目前为止的完整代码

在进入下一个阶段前，有必要浏览一遍当前的完整代码。

```go
package main

import "fmt"

type TreeNode struct {
	Parent *TreeNode

	Value  int
	Height int

	Left  *TreeNode
	Right *TreeNode
}

func NewTreeNode(value int) *TreeNode {
	return &TreeNode{Value: value, Height: 1}
}

// Insert 往树中合适位置插入节点
func Insert(root *TreeNode, value int) *TreeNode {
	if root == nil {
		return &TreeNode{Value: value}
	}

	if value < root.Value {
		root.Left = Insert(root.Left, value)
		root.Left.Parent = root
	} else if value > root.Value {
		root.Right = Insert(root.Right, value)
		root.Right.Parent = root
	} else {
		return root
	}

	root.Height = max(GetHeight(root.Left), GetHeight(root.Right)) + 1

	bf := GetBalanceFactor(root)
	if bf < -1 { // 应该左旋
		root = RotateLeft(root)
	} else if bf > 1 { // 应该右旋
		root = RotateRight(root)
	} else {
		// do nothing
	}

	return root
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}

// GetHeight 用来处理节点为 nil 的情况
func GetHeight(node *TreeNode) int {
	if node == nil {
		return 0
	}

	return node.Height
}

// GetBalanceFactor 获取平衡因子
func GetBalanceFactor(node *TreeNode) int {
	if node == nil {
		return 0
	}

	return GetHeight(node.Left) - GetHeight(node.Right)
}

// RotateRight 右旋
func RotateRight(root *TreeNode) *TreeNode {
	if root.Left == nil {
		return root
	}

	// 旋转
	newRoot := root.Left
	tmp := newRoot.Right
	newRoot.Right = root
	root.Left = tmp

	// 更新节点的父节点信息
	if tmp != nil {
		tmp.Parent = root
	}
	newRoot.Parent = root.Parent
	root.Parent = newRoot

	// 更新树高
	root.Height = max(GetHeight(root.Left), GetHeight(root.Right)) + 1
	newRoot.Height = max(GetHeight(newRoot.Left), GetHeight(newRoot.Right)) + 1

	return newRoot
}

// RotateLeft 左旋
func RotateLeft(root *TreeNode) *TreeNode {
	if root.Right == nil {
		return root
	}

	// 旋转
	newRoot := root.Right
	tmp := newRoot.Left
	newRoot.Left = root
	root.Right = tmp

	// 更新节点的父节点信息
	if tmp != nil {
		tmp.Parent = root
	}
	newRoot.Parent = root.Parent
	root.Parent = newRoot

	// 更新树高
	root.Height = max(GetHeight(root.Left), GetHeight(root.Right)) + 1
	newRoot.Height = max(GetHeight(newRoot.Left), GetHeight(newRoot.Right)) + 1

	return newRoot
}

func PrintTree(root *TreeNode) {
}

func main() {
	var root *TreeNode
	root = Insert(root, 7)
	root = Insert(root, 3)
	root = Insert(root, 2)
	root = Insert(root, 5)
	root = Insert(root, 8)
	PrintTree(root)
	fmt.Println("------------")

	root = Insert(root, 6)
	PrintTree(root)
	fmt.Println("------------")
}
```

## 旋转的问题

与最开始示例不同的是，上面的代码最后插入的是 6。执行这些代码，发现得到的仍然是一颗不平衡的树。

为什么？

用图来解释：

![](balanced-binary-tree-1.svg)

这是原始图，插入节点 6 后得到：

![](balanced-binary-tree-4.svg)

此时对于节点 7，左子树比右子树高 2。因此需要右旋，根据规则右旋后得到：

![](balanced-binary-tree-5.svg)

为什么会这样？

从第二张图可以看到，之所以平衡被打破，是因为 A 的高度发生变化，导致节点 3 的高度变化。当右旋开始时，这个打破平衡的 A 被抽离了。

![](balanced-binary-tree-6.svg)

抽离后节点 3 的高度变回 2，也就是说根节点左子树的高度为 2。如果执行右旋，那么根节点的左子树的高度必定会减 1，变成 1。

不管原先根节点右子树的树高是多少，在旋转后树高为 2 的部分必然要挂到原先根节点 7 上。此时根节点的右子树高度必大于 2。

![](balanced-binary-tree-7.svg)

上图把节点 8 隐藏起来，可以直观地看到问题。

也就是说，继续按照之前的方式，旋转后必处于不平衡状态。而且从这个状态出发，也只能执行左旋，旋转后回到原来的样子。进入死循环。

怎么解决？

根据上面的描述，右旋是必然要做的，并且右旋时必然使左子树高度减 1。

要解决这个问题，需要让根节点的左子树去掉其右子树剩下的部分的高度增加，然后再右旋。

有没有办法？

有，让左子树左旋就行。

![](balanced-binary-tree-8.svg)

根据规则旋转后：

![](balanced-binary-tree-9.svg)

接着，对根节点执行右旋：

![](balanced-binary-tree-10.svg)

去掉 A 的部分后，左子树的高度仍然为 3，右旋后为 2。

![](balanced-binary-tree-11.svg)

平衡了。

综上，当一个节点的左右子树不平衡时，要分两步判断：

1. 左子树高还是右子树高
2. 不平衡是由子树的左子树还是右子树引起的

如果是左子树的右子树引起的，则子树需要先旋转。同理，如果是右子树的左子树引起的，子树也要先旋转。（发现没？两者都是在旋转曲线的内侧）

## 旋转方式改进

从前面的内容可以总结出旋转有四种类型：

1. 左子树的左子树引起的失衡，用 LL（Left-Left） 表示；
2. 左子树的右子树引起的失衡，用 LR（Left-Right） 表示；
3. 右子树的左子树引起的失衡，用 RL（Right-Left） 表示；
4. 右子树的右子树引起的失衡，用 RR（Right-Right） 表示。

在 Insert 的时候，要区分这四种情况。

```go
func Insert(root *TreeNode, value int) *TreeNode {
	// ...

	bf := GetBalanceFactor(root)
	if bf < -1 { // 应该左旋
		if value < root.Right.Value { // 在右子树的左子树上
			root = RLRotation(root)
		} else { // 在右子树的右子树上
			root = RRRotation(root)
		}
	} else if bf > 1 { // 应该右旋
		if value < root.Left.Value { // 在左子树的左子树上
			root = LLRotation(root)
		} else { // 在左子树的右子树上
			root = LRRotation(root)
		}
	} else {
		// do nothing
	}

	return root
}

func LLRotation(root *TreeNode) *TreeNode {
	return RotateRight(root)
}

func LRRotation(root *TreeNode) *TreeNode {
	root.Left = RotateLeft(root.Left)
	return RotateRight(root)
}

func RRRotation(root *TreeNode) *TreeNode {
	return RotateLeft(root)
}

func RLRotation(root *TreeNode) *TreeNode {
	root.Right = RotateRight(root.Right)
	return RotateLeft(root)
}
```

## 结尾

以前一直认为二叉树旋转和平衡二叉树很难，现在认真看的时候却觉得其实也没什么。

接下去先用二叉树的打印水一篇，然后就是红黑树了。

以前也一直觉得红黑树很难，但最近看了资料（特别是那本《算法》），觉得挺容易理解的，就干脆一起写出来吧。

