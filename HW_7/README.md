# CSCI_163A_Algorithms
# Homework 7

*NOTE: This file stores the analysis for each problem*
*CODE DONE IN C++*

# *Q5: Design an algorithm for finding a maximum spanning tree—a spanning tree with the largest possible edge weight—of a weighted connected graph.*
A3: Adapted from the notes, do the opposite of Kruskal’s algorithm for minimum spanning trees; Choose the max weight at every step
```
wgraph kruskal(wgraph G)
{
  ds<int> D;
  for (auto v: G.V)
  ds.make_set(v);
  sort_Graph(G.E, DECREASING);
  // some sorting function in DECREASING mode
  // decreasing order of weight
  wgraph ans;

  for (auto e: G.E)
  if (ds.join(e.first, e.second))
  ans.add_edge(e);
  return ans;
}
```
