# incremental-ad

Example:

- Facebook as a graph
  - nodes = humans
  - edges = friends 

events: 
  - create edge 
  - destroy edge

  - a click is a tuple (userid, userid, action, timestamp) representing
    - an instance of user A interacting with user B at time t 
	- a new edge event when user A friends user B 

  - add node (eg, new human makes an account)

1. At each node, we have a machine-learned embedding vector with the
   idea that the dot product of two vectors is how much two people
   should be friends.

2. If there is an event, we need to update the embedding

Operations:
```
   type human = (name, place, newsfeed)
   type node = (id, embedding, human) 
   type edge = (node, node, event)

   add-node : graph × human → graph × node 
   add-edge : graph × edge → graph 
   remove-node : graph × id → graph
   remove-edge : graph × edge → graph
```
a sample ML model: initial-embedding : name × place × newsfeed → embedding 


when we invoke add-edge, some of the embeddings in the graph will be updated. 

  Nodes: x_i is embedding of node i

  (i, j, becomes-friend) => x_i . x_j high

Before event, we had xs such that
  {x_1, ..., x_n} = argmax_{x_1..x_n}  (\sum_{(i,j) \in E}  x_i . x_j)/(\sum_i |x_i - mean(xs)|)

Event E += (i',j')

x_k === x[k]

After E, we want xs such that
  {x'_1, ..., x'_n} = argmax_{x_1..x_n}  (\sum_{(i,j) \in E}  x_i . x_j + x[i'] . x[j'])/(\sum_i |x_i - mean(xs)|)

Tricky because edges (i,i') or (j,j') may already exist...

         


