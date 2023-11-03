```c++
vector<int> map(rows+1);

vector<vector<int>> map(rows+1, vector<int>(columns+1));
```
c++의 vector로 편리하게 동적 할당 가능

#### 행렬 회전 팁
값을 옮기는 과정에서 유실되는 값이 있다면, 복제 map을 만들자
```c++
vector<vector<int>> map(rows+1, vector<int>(columns+1));

// 사본 생성
vector<vector<int>> temp = map;

...

// 연산 끝나고 사본 반영
map = temp;
``` 