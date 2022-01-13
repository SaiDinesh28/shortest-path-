//# shortest-path-
//shortest path in a directed acyclic graph

#include<bits/stdc++.h>
using namespace std;
void dfs(vector<pair<int,int>>adj[],vector<int>&topo,int node,vector<int>&vis){

   vis[node]=1;
   for(auto it:adj[node]){
	   if(vis[it.first]==0){
		   dfs(adj,topo,it.first,vis);
		
	   }
   }
      topo.push_back(node);

}
vector<int> toposort(vector<pair<int,int>>adj[],int n){
	vector<int>topo;
	vector<int>vis(n,0);
	for(int i=0;i<n;i++){
		if(vis[i]==0){
		   dfs(adj,topo,i,vis);
		}

	}
	reverse(topo.begin(),topo.end());
	return topo;
}
int shortdist(vector<pair<int,int>>adj[],vector<int>topo,int n,int node1,int node2){
	vector<int>dist(n,INT_MAX);
  dist[node1]=0;
         for(auto it:topo){
			 if(dist[it]!=INT_MAX){
            for(auto i:adj[it]){
				dist[i.first]=min(dist[i.first],dist[it]+i.second);
			}
			 }
		 }
		 return dist[node2];

}
int main(){
	int t ;
	cin>>t;
	while(t--){
		int n,m;
		cin>>n>>m;
		vector<pair<int,int>>adj[n];
		for(int i=0;i<m;i++){
			int a,b,c;
			cin>>a>>b>>c;
			adj[a].push_back({b,c});
		}
		int a,b;
		cin>>a>>b;

        vector<int>topo=toposort(adj,n);
	    int x=shortdist(adj,topo,n,a,b);
		cout<<x<<endl;
		//for(auto it:v) cout<<it<<" ";
	}
}
