### 0-1 Knapsack Problem

원소의 개수가 n인 집합 2개가 있다.
각각 무게(weight)는 wi, 이득(profit)은 pi  
가방에 최대한 넣을 수 있는 무게는 W  
W를 넘지 않으면서 이득(profit)을 최대화하려면 각 item을 넣을까(1)/말까(0) 결정하는 것

### 해결
1. Naive approach
	1. O(2^n)
2. Dynamic Programming approach
	1. ![Pasted image 20230607175509](https://github.com/lina1919/cs_study/assets/63230463/303d014d-032d-474a-9a75-5f7a54cf57ba)
	2. code
		```
		int zero_one_knapsack(int *p, int *w, int n, int W) { 
			int i, ww, tmp;
			 …
			for (ww = 0; ww <= W; ww++) P[0][ww] = 0; 
			for (i = 1; i <= n; i++) { 
				P[i][0] = 0; 
				for (ww = 1; ww <= W; ww++) { 
					if (w[i] <= ww) { 
						if ((tmp = p[i] + P[i-1][ww-w[i]]) > P[i-1][ww]) 
							P[i][ww] = tmp; 
						else 
							P[i][ww] = P[i-1][ww]; 
						} 
						else P[i][ww] = P[i-1][ww]; 
					} 
				}
				return P[n][W]; 
			}
		```


3. knapsack 알고리즘 결과 출력하기
	  ```
		while(i>0 && j>0){
			if(k[i][j] == k[i-1][j]){
				cout << i << "=0" << endl;
				i--;
			}
			else{
				cout << i << "=1" << endl;
				i--;
				j=j-w
			}
		}
	```
![Pasted image 20230608133022](https://github.com/lina1919/cs_study/assets/63230463/687bd560-3242-4850-8942-f533e0759b5f)
	1. Time Complexity
		**=> O(nW)**
		linear time algorithm이 아니다.
		그 누구도 0-1 Knapsack Problem에 대한 polynomial한 알고리즘을 찾아내지 못했다.
