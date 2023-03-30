# Union-Find
并查集是一种树形结构，通常在一个并查集中维护多个集合，一般提供合并和查找的功能。

## 表示
使用数组$parent[i]$表示节点 $i$ 的父节点。
```python
class Unionfind:
	def __init__(self):
		# 表示每个节点的父节点
		self.parent: List[int]
		# 以该节点为根的树的节点个数
		self.size: List[int]
	# 查找节点 p 的祖先节点
	def find(self, p: int) -> int:
		pass
	# 将 p 和 q 所在的两个集合合并
	def union(self, p: int, q: int) -> void:
		pass
```

## 查找操作的实现
### 普通查找
```python
# 查找p的祖先节点
def find(self, p: int) -> int:
	while p != self.parent[p]:
		p = self.parent[p]
	return p
```
### 复杂度分析
时间复杂度：$O(h)$ 其中，h 为树的高度

### 路径压缩
```python
def findWithPathCompress(self, p: int) -> int:
	if p != self.parent[p]:
		self.parent[p] = self.find(self.parent[p])
	return self.parent[p]
```
### 复杂度分析
时间复杂度：$O(\alpha(n))$

## 合并操作的实现
### 普通合并
```python
def union(self, p: int, q: int) -> void:
	pRoot: int = self.find(p)
	qRoot: int = self.find(q)
	self.parent[pRoot] = qRoot
```
### 复杂度分析
时间复杂度：$O(h)$

### 考虑合并后集合的结构
目的是为了防止合并后的集合退化为线性结构
```python
def unionWithWeighted(self, p: int, q: int) -> void:
	pRoot: int = self.findWithPathCompress(p)
	qRoot: int = self.findWithPathCompress(q)
	if self.size[pRoot] >= self.size[qRoot]:
		self.parent[qRoot] = pRoot
		self.size[pRoot] += self.size[qRoot]
	else:
		self.parent[pRoot] = qRoot
		self.size[qRoot] += self.size[pRoot]
```
### 复杂度分析
时间复杂度：$O(\alpha(n))$

## 完整实现参考
```python
from typing import List

class  UnionFind:

	def  __init__(self, n: int):

		self.parent: List[int] = [i for i in  range(n)]

		self.size: List[int] = [1  for i in  range(n)]

	# 查找 p 所在集合的代表节点（祖先节点）
	def  find(self, p: int) -> int:
		while p !=  self.parent[p]:
			p =  self.parent[p]
		return p


	def union(self, p: int, q: int) -> None:

		pRoot: int  =  self.find(p)

		qRoot: int  =  self.find(q)

		self.parent[pRoot] = qRoot

	def  findWithPathCompress(self, p: int) -> int:

		if p !=  self.parent[p]:

		self.parent[p] = self.findWithPathCompress(self.parent[p])

		return  self.parent[p]

	def  unionWithWeighted(self, p: int, q: int) -> None:

		qRoot: int  =  self.findWithPathCompress(q)

		pRoot: int  =  self.findWithPathCompress(p)

		if  self.size[qRoot] >  self.size[pRoot]:

			self.parent[pRoot] = qRoot

			self.size[qRoot] +=  self.size[pRoot]

		else:

			self.parent[qRoot] = pRoot

			self.size[pRoot] +=  self.size[qRoot]
```
## 并查集的应用

1. 连通性问题
   - [合根植物](records/union-find/合根植物.md)
   - [判断二分图](records/union-find/判断二分图.md)
   - [账户合并](records/union-find/账户合并.md)
2. 最短路问题
	- [除法求值](records/union-find/除法求值.md)

