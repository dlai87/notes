## Cheapest Flights Within K Stops

There are `n` cities connected by some flights. Each flight (u, v, w) starts from city u and arrives at v with a price w.

Given `n`, `flights`, together with starting city `src` and the destination `dst`, your task is to find the cheapest price from src to dst with at most `K` stops.

If there is no such route, return `-1`.



最短路径问题，做一个复习总结： 

+ 无权图： bfs 
+ 有权图
  Floyd  任意两点间的最短路径
  Dijkstra  某一点到任意一点的最短路径