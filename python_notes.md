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

## Sorting
- Sort list using sublist element: `sub_li.sort(key = lambda x: x[1], reverse: True)`
- Bubble sort
  ``` python
  for i in range(len(array)):
    for j in range(len(array)-i-1):
      if (array[j] > array[j+1]):
        array[j], array[j+1] = array[j+1], array[j]
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

## String
- Remove leading and trailing whitespace (returns new string): `string.strip()`
- Remove leading (left) whitespace (returns new string): `string.lstrip()`
- Remove trailing (right) whitespace (returns new string): `string.rstrip()`
- Check if string contains only alphabets: `string.isalpha()`
- Check if string contains only digits: `string.isdigit()`

## Arithmetic
- Integer division operator (divide and keep whole number component): `num // 10`

