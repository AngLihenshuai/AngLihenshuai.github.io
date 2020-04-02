---
layout: post
title:  "图的拓扑排序"
date:   2020-01-02 13:25:35 +0200
categories: jekyll update
---
## First Blog 

### 图的拓扑排序

`Test Code`

```python
def ladderLength(self, start, end, dict):
        # write your code here
        dict.add(end)
        stack = [start]
        if start == end:
            return 0
        node_dict = {start:1}
        distance = 0
        while stack:
            l = len(stack)
            distance += 1
            for i in range(l):
                word = stack.pop(0)
                if word == end:
                    return distance
                # next_words_list = self.findNextWorlds(word)
                
                for next_word in self.findNextWorlds(word):
                    if next_word in node_dict or next_word not in dict:
                        continue
                    stack.append(next_word)
                    node_dict[next_word] = 1
        return 0
                
    def findNextWorlds(self, word):
        next_list = []
        for i in "abcdefghijklmnopqrstuvwxyz":
            for j in range(len(word)):
                if i == word[j]:
                    continue
                new_word = word[:j] + i + word[j+1:]
                next_list.append(new_word)
        
        return next_list
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUxMTk5MTUwOSw5ODE2MjU2MjRdfQ==
-->