# Future_Work
用于以后找工作相关事宜
### 并查集模板

```c++
class unionFind{
    public:
        vector<int>father;
        unionFind(int num){
            for(int i = 0; i < num ; i++)
                father.push_back(i);//箭头指向自己
        }
        int Find(int n){//寻找集合中的老大
            while(n != father[n]){
                father[n] = father[father[n]];
                n = father[n];
            }
            return n;
        }
        void Union(int a ,int b){//结合起来，形成集合
            int fa = Find(a);
            int fb = Find(b);
            father[fa] = fb;
        }
};
```

#### 案例一(leetcode_547)

班上有 N 名学生。其中有些人是朋友，有些则不是。他们的友谊具有是传递性。如果已知 A 是 B 的朋友，B 是 C 的朋友，那么我们可以认为 A 也是 C 的朋友。所谓的朋友圈，是指所有朋友的集合。

给定一个 N * N 的矩阵 M，表示班级中学生之间的朋友关系。如果M[i][j] = 1，表示已知第 i 个和 j 个学生互为朋友关系，否则为不知道。你必须输出所有学生中的已知的朋友圈总数。

##### 示例 1:

```c++
输入: 
[[1,1,0],
 [1,1,0],
 [0,0,1]]
输出: 2 
说明：已知学生0和学生1互为朋友，他们在一个朋友圈。
第2个学生自己在一个朋友圈。所以返回2。
```

##### 示例 2:

```c++
输入: 
[[1,1,0],
 [1,1,1],
 [0,1,1]]
输出: 1
说明：已知学生0和学生1互为朋友，学生1和学生2互为朋友，所以学生0和学生2也是朋友，所以他们三个在一个朋友圈，返回1。
```

###### 注意：

**1.N 在[1,200]的范围内。**
**2.对于所有学生，有M[i][i] = 1。**
**3.如果有M[i][j] = 1，则有M[j][i] = 1。**

```c++
class UnionFind{
    public:
        vector<int>father;
        UnionFind(int num){
            for(int i = 0; i < num ; i++)
                father.push_back(i);//箭头指向自己
        }
        int Find(int n){//寻找集合中的老大
            while(n != father[n]){
                father[n] = father[father[n]];
                n = father[n];
            }
            return n;
        }
        void Union(int a ,int b){//结合起来，形成集合
            int fa = Find(a);
            int fb = Find(b);
            father[fa] = fb;
        }
};
class Solution {
public:
    int findCircleNum(vector<vector<int>>& M) {
    	int N = M.size();
    	UnionFind UF(N);
    	for(int i=0; i < N; i++){
    		for(int j=0; j < N;j++)
    		{
    			if(M[i][j] == 1){
					UF.Union(i,j);				
				}
    		}
    	}
    	int res=0;
    	for(int i=0; i < N; i++)
    	{
    		if(UF.Find(i) == i){
    			res++;
    		}
    	}
    	return res;

    }
};
```

#### 案例二(leetcode_200)

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

 

示例 1:

```c++
输入:
11110
11010
11000
00000
输出: 1
```


示例 2:

```c++
输入:
11000
11000
00100
00011
输出: 3
解释: 每座岛屿只能由水平和/或竖直方向上相邻的陆地连接而成。
```

```c++
class UnionFind{
    public:
        vector<int>father;
        UnionFind(int num){
            for(int i = 0; i < num ; i++)
                father.push_back(i);//箭头指向自己
        }
        int Find(int n){//寻找集合中的老大
            while(n != father[n]){
                father[n] = father[father[n]];
                n = father[n];
            }
            return n;
        }
        void Union(int a ,int b){//结合起来，形成集合
            int fa = Find(a);
            int fb = Find(b);
            father[fa] = fb;
        }
};
class Solution {
public:
    int direction[4][2] = {{1,0},{-1,0},{0,-1},{0,1}};
    int encode(int i ,int j ,int n){
        return i*n+j;
    }

    int numIslands(vector<vector<char>>& grid) {
        
        int M = grid.size();
        if(M==0)return 0;
        int N = grid[0].size();
        if(N==0)return 0;
        UnionFind UF(M*N);
        for(int i=0;i<M;i++)
            for(int j=0;j<N;j++)
            {
                if(grid[i][j] == '1'){
                    for(int d=0;d<4;d++)
                    {
                        int di = direction[d][0];
                        int dj = direction[d][1];
                        if(i+di >= 0 && i+di < M && j+dj >= 0
                        && j+dj < N && grid[i+di][j+dj] == '1'){
                            UF.Union(encode(i,j,N), encode(i+di, j+dj, N));
                        }
                    }
                }
            }
        int res=0;
        for(int i=0;i<M;i++){
            for(int j=0;j<N;j++){
                if(grid[i][j] == '1'){
                    int id =encode(i, j, N);
                    if(UF.Find(id) == id)
                    {
                        res++;
                    }
                }
            }
        }
        return res;
    }
};
```


```




