- Data compression
- text file을 binary file로 변환하는 방법

### Prefix Code
- 접두부가 겹치지 않는 것이 중요!
	- a = 101 이라면 b는 1, 10, 101이 될 수 없다
![Pasted image 20230606233516](https://github.com/lina1919/cs_study/assets/63230463/09719ba3-f4a8-4add-9144-f47aa96cf223)

- 이걸 minimize 하기

### Huffman Tree
- 허프만 트리를 만드는 법
	- 각 문자가 개별적인 트리인 상태에서 시작해서 빈도수가 작은 두 트리를 합쳐서 보다 큰 트리를 생성하는 과정을 반복
	- 각 노드는 빈도수를 표시
	- 좌우의 두 간선은 각각 0과 1로 써줌
	- 합쳐지는 두 트리는 자식노드를 갖는 부모노드를 생성.
	- 부모노드의 빈도수는 두 자식 노드의 빈도수의 합
![Pasted image 20230606233549](https://github.com/lina1919/cs_study/assets/63230463/4e37e3e5-1e84-4d0d-a303-b3e5db0ca854)

```
typedef struct _node { 
	char symbol; 
	int freq; 
	struct _node *left; 
	struct _node *right;
} NODE; 
NODE *u, *v, *w;
… 
for (i = 1; i <= n; i++) { 
	/* insert the n single-node trees */ 
} 
for (i = 1; i <= n-1; i++) {
	u = PQ_delete(); 
	v = PQ_delete(); 
	w = make_a_new_node(); 
	w->left = u; 
	w->right = v; 
	w->freq = u->freq + v->freq; 
	PQ_insert(w); 
}
w = PQ_delete();
/* w points to the optimal tree. */
```
**=> O(nlogn)**

### Correctness of the Huffman's Algorithm
- 귀류법을 통한 증명
	- i번째 단계에서 얻은 트리 집합이 optimal code에 해당하는 binary tree의 가지(branch)들이라면, (i+1)번째 단계에서 얻은 트리 집합 또한 optimal code에 해당하는 binary tree의 가지들이 된다.
- Base Strep
	- When k=0, 각 tree는 trivial하게 optimal tree의 branch다
- Induction step
	- k가 i일 때 명제가 참이라고 가정하고, S가 i번째 단계 후에 존재하는 트리의 집합이며, T가 해당하는 optimal tree라고 가정. u와 v는 (i+1)번째 단계에서 결합되는 트리의 루트이다.
	- Case 1 : u 와 v가 sibling이라면 증명 끝
	- Case2 : u와 v가 sibling이 아니라면
		![Pasted image 20230607021924](https://github.com/lina1919/cs_study/assets/63230463/ad3b75e5-789a-40d3-abef-882923554d8b)
		- T는 i 번째 단계 계산 후의 트리 집합에 해당하는 optimal code에 대응하는 어떤 optimal tree
		- v와 w를 루트노드로 하는 두 트리를 서로 맞바꿔 새로운 트리 T'를 구축
		- 따라서 freq(w) ≥ freq(v) and depth(w) ≥ depth(v) in T
		- bits(T’) = bits(T) + (depth(w) – depth(v)) * (freq(v) – freq(w)) ≤ bits(T).
		- bits(T') ≤ bits(T)이므로 T가 optimal tree인데 T'의 비용이 T보다 작은 모순 발생
		- 따라서 i번째 선택된 u와 v가 T에서 sibling이어야 함
	  - 증명 끝!
