---
title: "Maior obstáculo de um curso"
date: 2023-05-07T19:17:17-03:00
draft: true
description: "Post"
categories: ["dev"]
tags: ["Algoritmos", "Leetcode"]
---

Essse post vai ser um ínicio de uma série onde eu vou pegar alguns problemas sejam eles de qualquer site no caso deste artigo vai ser do leetcode e vou explicar meu racícionio por que fiz para resolver ele neste caso vai ser deste [problema](https://leetcode.com/problems/find-the-longest-valid-obstacle-course-at-each-position/) do leetCode.

## Código

```csharp
public class Solution {
    public static int BisectRight<T>(List<T> list, T value) where T : IComparable<T> {
        int index = list.BinarySearch(value);
        if (index < 0) index = ~index;
        else {
            while (index < list.Count && list[index].CompareTo(value) == 0)
                index++;
        }
        return index;
    }

    public int[] LongestObstacleCourseAtEachPosition(int[] obstacles) {
        int n = obstacles.Length;
        int[] answer = Enumerable.Repeat(1, n).ToArray();
        List<int> list = new List<int>();
        for (int i = 0; i < n; i++) {
            int idx = Solution.BisectRight(list, obstacles[i]);
            if (idx == list.Count)
                list.Add(obstacles[i]);
            else 
                list[idx] = obstacles[i];

            answer[i] = idx + 1;
        }
        return answer;
    }
}
```
