#The Gromov Centrality for a node i in graph G can be computed using any distance metric. In our paper, we focus on the shortest path distances between nodes. The matrix of shortest path distances can be computed using Networkx. 

#importing networkx, and other packages 

import numpy as np
import matplotlib.pyplot as plt
import networkx as nx

#computing shortest path distance matrix for graph G 

def shortest_path_matrix(G): 
   lengths = dict(nx.all_pairs_shortest_path_length(G))
   shortest_path_matrix = np.array([[length[n][m] for m in G.nodes] for n in G.nodes], dtype=np.int32)
   return shortest_path_matrix

#function that returns the Gromov centrality for a given node. The function takes the node number, the distance matrix, and the maximum path (which is the scale l) 
   
def Gromov_Centrality(node, path_matrix, max_path): 
    
    #find the size of the l-hood for node, depending on the chosen scale 
    
    node_paths = path_matrix[node,:]
    lhood = np.where((node_paths <= max_path) & (node_paths > 0))
    lhood_size = len(lhood[0])
    
    #if the lhood size is 0, the Gromov product is undefined 
    if lhood_size > 1: 
        #find the set of all tuples j,k composed of nodes in the lhood 
        tuples = list(itertools.permutations(lhood[0], 2))
        tuples_size = len(tuples)
        subtract = 2*np.sum(path_matrix[node,lhood[0]])*(lhood_size -1)
    
        summation = 0 
        for i in range(tuples_size):
            a = tuples[i]
            summation += path_matrix[a]
        
        #compute the final gromov product 
        final_return = (summation - subtract)*(1/((lhood_size)*(lhood_size-1)))
    
        return final_return
    else: 
        return 0   
   
