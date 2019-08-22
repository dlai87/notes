## cheapest flights within K stops 

https://www.lintcode.com/problem/cheapest-flights-within-k-stops/description

复习图的最短路径算法

+ Floyd 

+ Dijkstra

+ Bellman 

  这题用到bellman的算法

```python
import sys 

class Solution:
    """
    @param n: a integer
    @param flights: a 2D array
    @param src: a integer
    @param dst: a integer
    @param K: a integer
    @return: return a integer
    """
    def findCheapestPrice(self, n, flights, src, dst, K):
        INF = sys.maxsize
        dis = [] 
        for i in range(n): 
            dis.append(INF)
        for flight in flights: 
            if flight[0] == src: 
                dis[flight[1]] = flight[2]
        for i in range(K): 
            for flight in flights: 
                u = flight[0]
                v = flight[1]
                cost = flight[2]
                dis[v] = min(dis[v], dis[u]+cost)
        if dis[dst] == INF:
            return -1 
        return dis[dst]
                
```

