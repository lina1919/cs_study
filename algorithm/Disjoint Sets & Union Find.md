## Disjoint Set
Disjoint Set이란 서로 공통된 원소를 가지고 있지 않은 2개 이상의 집합

**Basic Operations**
- Makeset(x) : O(1)
- Find(x)
	- 어떤 원소가 주어졌을 때 이 원소가 속한 집합의 루트노드를 반환하는 연산
- Union(x,y) 

Ex)
U = {a,b,c,d,e}
Makeset(x); -> {a}, {b}, {c}, {d}, {e}
Union(a,c); -> {a,c}, {b}, {d}, {e}

- Union과 find 연산은 트리의 높이에 크게 의존한다. 성능을 높이려면 트리의 높이를 최소화해야함.
**1. Path Compression**
	find 연산을 수행할 때마다 트리의 구조를 평평하게 만듦.
	-> 루트노드까지 순회 중 방문한 각 노드들이 직접 루트 노드를 가리키도록 함
	모든 노드들은 같은 대표 노드 공유
	find O(1)
**2. Union By Rank**
	1. 항상 작은 트리를 큰 트리 루트에 붙인다.
	2. Union 과 Find 는 worst case에 O(logn)
	3. tree의 element 개수는 최소 2^r(r=tree의 rank)

```
Find(x) {
	while( x != parent(x))
		x := parent(x)
	return x
}

Find(x){
	if(x == parent(x))
		return x
	else
		return Find(parent(x))
}


Union(x,y){
	x0:=Find(x)
	y0:=Find(y)
	if(x0==y0)
		return
	if(rank(x0) > rank(y0))
		parent(y0) := x0
	else
		parent(x0) := y0
		if(rank(x0) == rank(y0))
			rank(y0) := rank(y0)+1
}


```

##Scheduling with Deadlines using disjoint sets

1. 주어진 jobs들을 profit 값을 기준으로 비증가 순서대로 정렬한다.
2. dmax + 1개의 disjoint set으로 초기화합니다. 각 집합에는 0부터 dmax까지의 정수가 포함된다. 이 집합들은 각각 시간 슬롯을 나타낸다.
2. 작업들을 정렬된 순서대로 순회한다.
3. 각 작업에 대해 다음 작업을 수행한다:
    - 작업의 마감 시간과 n 중 작은 값으로 이루어진 집합 S를 찾는다.
    - S의 최소 값이 0이라면 작업을 거부합니다. 즉, 해당 작업을 마감 시간 내에 처리할 수 없다는 의미이다.
    - 그렇지 않다면, 작업을 S의 최소 값에 스케줄링하고, S를 small(S)-1 값을 가지는 집합과 병합한다.
시간복잡도 : O(nlogm) m = min(n,dmax)
					dmax : n개의 job들의 maximum deadline
					O(nlogn) : qsort

![Pasted image 20230606230957](https://github.com/lina1919/cs_study/assets/63230463/58e0173a-6c82-42a4-a670-fe99483241da)
