백트래킹을 대신해서 편리하게 순열을 구할 수 있다
크기가 있는 값이면 가능 (int, char ..)
```c++
	// {1, 2, 3, 4}
	do{

		for(int i=0; i<4; i++){
			cout << v[i] << " ";
		}

		cout << '\n';

	}while(next_permutation(v.begin(),v.end()));


	// 출력 값
	1 2 3 4
	1 2 4 3
	1 3 2 4
	
	...
	
	4 2 3 1
	4 3 1 2
	4 3 2 1
```
[next_permutation](https://twpower.github.io/82-next_permutation-and-prev_permutation)