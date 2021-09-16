---
layout: page
title: Python Notes
permalink: /python-cheatcheet/
---

## Recipes
- Reverse digits in a number
  ``` python
  reversedNum = 0
  while (num != 0):
    pop = num % 10
    num = num // 10
    reversedNum = reversedNum * 10 + pop
  ```
- Find height of binary tree
  ``` python
  def height(node):
    if node is None:
      return 0
    else :
      # Compute the height of each subtree
      lheight = height(node.left)
      rheight = height(node.right)

      #Use the larger one
      return max(lheight+1, rheight+1)
  return height(root)

  # Alternative
  def height(node, depth):
    if (node == None):
      return depth
    
    left_d = helper(node.left, depth+1)
    right_d = helper(node.right, depth+1)
    return max(left_d, right_d)
  return height(root, 0)
  ```
- Find midpoint of linked list - two pointer method
  ``` python
  p1, p2 = head, head
  while p2.next and p2.next.next:
    p1 = p1.next
    p2 = p2.next.next
  # p1 will be at the midpoint

  # odd nodes: 1 -> 2 (p1) -> 3 (p2)
  # even nodes: 1 -> 2 (p1) -> 3 (p2) -> 4
  ```

## Sorting
- Bubble sort
  ``` python
  for i in range(len(array)):
    for j in range(len(array)-i-1):
      if (array[j] > array[j+1]):
        array[j], array[j+1] = array[j+1], array[j]
  ```
- Merge sort for linked list: https://www.geeksforgeeks.org/merge-sort-for-linked-list/
- Custom comparator for sorted (Python 3):
  ``` python
  def compare(item1, item2):
    return fn(item1) - fn(item2)

  from functools import cmp_to_key
  sortedList = sorted(mylist, key=cmp_to_key(compare))
  ```

## Searching
- Breadth first search for binary tree
  ``` python
  # find sum of nodes in each level
  q = [root]
  result = []
  while (len(q) != 0):
      levelSum = 0
      for i in range(len(q)):
          node = q.pop(0)
          levelSum += node.val
          if (node.left != None): q.append(node.left)
          if (node.right != None): q.append(node.right)
      result.append(levelSum)
  return result
  ```

## Arrays
- Access the items in reverse order (no copy): `for item in reversed(list)`
- Reverse the list in-place: `list.reverse()`
- Make a copy of the reversed list: `list[::-1]`
- Join items in list: `','.join(list) -> string`
- Sort list using sublist element: `sub_li.sort(key = lambda x: x[1], reverse: True)`
- Remove first occurrence of item: `list.remove(item)`
- Remove item at index `i` (removes last item when index is not given): `list.pop(i)`

## String
- Remove leading and trailing whitespace (returns new string): `string.strip()`
- Remove leading (left) whitespace (returns new string): `string.lstrip()`
- Remove trailing (right) whitespace (returns new string): `string.rstrip()`
- Check if string contains only alphabets: `string.isalpha()`
- Check if string contains only digits: `string.isdigit()`
- Find distance between two characters (`ord` returns acsii code): `ord('z') - ord('a')`
- Convert ascii code back to character: `chr(ascii_value)`

## Dictionary
- Remove key from dict: `del dict[key]`
- Remove key and get removed value: `dict.pop(key, default_value_if_key_doesnt_exist)`
- Get key with max value: `max(stats, key=stats.get)`

## Tree
- Find diameter of binary tree: https://www.geeksforgeeks.org/diameter-of-a-binary-tree/

## Arithmetic
- Integer division operator (divide and keep whole number component): `num // 10`
- Multiply two arrays elementwise: `[a*b for a,b in zip(listA, listB)]`
- Find HCF (GCD) of two numbers: `math.gcd(x,y)`
- Initialise infinity integer: `float('inf)` or `float('-inf') or math.inf`

## Set
- Add to a set: `set.add(item)`