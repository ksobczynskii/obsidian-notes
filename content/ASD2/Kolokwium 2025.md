```
Zadanie 1:
int[] TopologicalSort(int[] V, (int from, int to)[] E)
{
	int[n] counter = {0};
	int[n] sorted = {-1};
	int idx = 0;
	foreach(var e in E)
	{
		counter[e.To]++;
	}
	
	Queue q;
	for(int i=0; i<n; i++)
	{
		if(counter[i]==0)
			q.ENQ(i);
	}
	
	while(!q.Empty)
	{
		int i = q.DEQ();
		sorted[idx++] = i;
		for(int v in N(i))
		{
			counter[i]--;
			if(counter[i]==0)
				q.ENQ(i);
		}
	}
}
```

Zadanie 2:
```
int[,] FloydWarshall(G, w)
{
	int[n,n] odl = ∞;
	foreach(var e in G.Edges)
	{
		odl[e.From, e.To] = e.Weight;
	}
	for(int i=0; i<n;i++)
		odl[i,i] = 0;
		
	
	for(int k=0; k<n;k++)
		for(int i = 0; i<n; i++)
			for(int j=0; j<n; j++)
				if(odl[i,k] + odl[k,j] < odl[i,j])
					odl[i,j] = odl[i,k] + odl[k,j];
}
```



$$
Rozpatrzmy 

$$


Zadanie 3:
```
int GetNoShortestPaths(G, w, u, v)
{
	int paths = Dijkstra(G,w,u,v);
	
	
}

int Dijkstra(G,w,u,v)
{
	int odl[n];
	int paths[n];
	for(int i=0; i<n; i++)
		odl[i] = ∞;
		paths[0];
	
	int odl[u] = 0;
	paths[1];
	
	Queue q;
	for(int i=0; i<n; i++)
	{
		q.ENQ(i, odl[i]);
	}
	
	while(!q.Empty)
	{
		int x = q.DEQ();
		foreach(var y in N(x))
		{
			if(odl[y] > odl[x] + w(xy))
				odl[y] = odl[x] + w(xy);
				paths[y] = paths[x];
				q.DecreaseKey(y, odl[y]);
			else if(odl[y] == odl[x] + w(xy))
				odl[y] += odl[x];
		}
	}
	
	return paths[v];
}
```
