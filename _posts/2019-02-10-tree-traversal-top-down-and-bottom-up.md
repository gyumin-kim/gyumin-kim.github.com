---
layout: post
title: "Tree 문제 재귀로 풀기: Top-down / Bottom-up"
date: 2019-02-10 13:01:00 +0300
description: Tree 문제를 접근하는 2가지 방식, Top-down / Bottom-up # Add post description (optional)
img: 7fYjq.png # Add image post (optional)
---

## Top-down Solution

"Top-down"이란 각 재귀 level에서, 어떤 값을 먼저 결정하고 그 값들을 재귀 함수를 호출하면서 자식 node들에게 함께 넘기는 것을 의미한다. 그래서 "top-down" 방식은 **preorder**(전위) 순회로 볼 수 있다.
재귀함수 `top_down(root, params)`의 대략적인 구조는 다음과 같다:

```
1. node가 null이면, 특정한 값을 리턴한다
2. 필요한 경우 answer를 update한다                    // anwer <-- params
3. left_ans = top_down(root.left, left_params)      // left_params <-- root.val, params
4. right_ans = top_down(root.right, right_params)   // right_params <-- root.val, params 
5. 필요한 경우 answer를 update한다                    // answer <-- left_ans, right_ans
```

예를 들어, 주어진 **이진 트리에서 depth의 최대값을 구하는 문제**를 생각해보자.

먼저 root node의 depth는 1이다. 또한 각 node의 depth를 알고 있다면, 당연히 그 자식 node들의 depth도 도출할 수 있다. 따라서, 함수를 재귀적으로 호출할 때 매개변수로 해당 node의 depth를 넘기다 보면, 결국 모든 node가 자신의 depth를 알 수 있게 된다. 그런 방식으로 계속 내려가다보면 leaf node(단말 노드)도 자신의 depth를 가질 것이고, 그것이 이 문제의 최종 정답이 될 것이다(물론 leaf node라고 해서 정답이라고 하면 안되고, 가장 큰 값이 무엇인지 구해야 한다).
다음은 함수 `maximum_depth(root, depth)`의 수도코드이다:

```
1. root가 null이면 return
2. if (root가 leaf node):
3.      answer = max(answer, depth)         // 필요한 경우 answer를 update
4. maximum_depth(root.left, depth + 1)      // 왼쪽 자식에 대해 재귀함수 호출
5. maximum_depth(root.right, depth + 1)     // 오른쪽 자식에 대해 재귀함수 호출
```

그림으로 표현하면 다음과 같다. 
![top-down](https://user-images.githubusercontent.com/26949964/52529118-aebf5b80-2d2f-11e9-8530-e52e68e17ac7.png)

이것을 java로 구현한 코드는 다음과 같다:
```java
private int answer;		// maximum_depth() 호출하기 전 반드시 answer 초기화할 것!
// 최초 root의 depth는 1이다
private void maximum_depth(TreeNode root, int depth) {
    if (root == null) return;
    if (root.left == null && root.right == null)
        answer = Math.max(answer, depth);
    maximum_depth(root.left, depth + 1);
    maximum_depth(root.right, depth + 1);
}
```





## Bottom-up Solution

"Bottom-up"이란, 각 재귀 level에서, 먼저 모든 자식 node들에 대해 재귀적으로 함수를 호출한 뒤 리턴값과 root node의 값에 따라 정답을 결정하는 방식이다. 이 방식은 **postorder**(후위) 순회로 볼 수 있다.
"bottom-up" 방식의 재귀함수 `bottom_up(root)`은 보통 아래와 같다:

```
1. node가 null이면, 특정한 값을 리턴한다
2. left_ans = bottom_up(root.left)          // 왼쪽 자식에 대해 재귀함수 호출
3. right_ans = bottom_up(root.right)        // 오른쪽 자식에 대해 재귀함수 호출
4. return answers                           // answer <-- left_ans, right_ans, root.val
```

방금 전과는 조금 다른 방식으로 depth의 최대값을 다뤄보자. 트리에서 어떤 node 자체를 root로 간주했을 때, 그 node의 depth의 최대값 `x`는 무엇인가?

만약 특정 node의 **왼쪽** 자식의 depth의 최대값 `l`과 **오른쪽** 자식의 depth의 최대값 `r`을 알고 있다면, 위의 질문에 답할 수 있을까? 물론이다. `l`과 `r` 중 더 큰 값을 고르고 1을 더해주면 해당 node의 depth의 최대값이 될 것이다. 즉 `x = max(l, r) + 1`인 셈이다.

정리하면, 각 node에 대해 그 자식들의 depth의 최대값을 구한 이후에 원하는 답을 도출할 수 있다는 것이다. 따라서 이 문제를 "bottom-up" 방식을 사용해서 풀 수 있다. 다음은 `maximum_depth(root)`의 수도코드이다:
```
1. root가 null이면 0을 return
2. left_depth = maximum_depth(root.left)
3. right_depth = maximum_depth(root.right)
4. return max(left_depth, right_depth) + 1  // 해당 node가 root인 subtree의 depth를 리턴
```

그림으로 표현하면 다음과 같다.
![bottom-up](https://user-images.githubusercontent.com/26949964/52529122-b252e280-2d2f-11e9-88db-2af3e553be0d.png)

이것을 java로 구현한 코드는 다음과 같다:
```java
public int maximum_depth(TreeNode root) {
	if (root == null)	return 0;                   // node가 null이면 0을 리턴
	int left_depth = maximum_depth(root.left);
	int right_depth = maximum_depth(root.right);
	return Math.max(left_depth, right_depth) + 1;	// 해당 node가 root인 subtree의 depth를 리턴
}
```





## 결론

트리 문제를 만났을 때, 2가지 질문을 던져보자.

node 자체가 정답과 연관성이 있는 몇 가지 매개변수를 결정할 수 있는가? 그 매개변수와 node의 값을 사용해서 자식 node들에게 넘겨줄 매개변수를 결정할 수 있는가?
이 2가지 질문에 모두 해당한다면, 문제를 **"top-down"** 방식의 재귀로 풀어보자.

혹은 트리의 어떤 node에 대해, 그 자식들이 자신의 depth를 갖고 있다면, 해당 node의 정답을 계산할 수 있는가?
만약 그렇다면, **"bottom-up"** 방식의 재귀가 좋은 방법이 될 수 있다.