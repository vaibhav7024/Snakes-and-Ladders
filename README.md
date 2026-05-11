# Snakes-and-Ladders

class Solution {
public:
    int snakesAndLadders(vector<vector<int>>& board) {
        int n=board.size();
        vector<int> v(n*n+1,-1);
        int idx=1;
        bool leftToright = true;
        for(int r =n-1;r>=0;r--){
            if(leftToright){
                for(int c=0;c<n;c++){
                    v[idx++]=board[r][c];
                }
            }else{
                for(int c=n-1;c>=0;c--){
                    v[idx++]= board[r][c];
                }
            }
            leftToright = !leftToright;
        }
        vector<bool> visited(n*n+1,false);
        queue<pair<int,int>> q;
        q.push({1,0});
        visited[1]=true;
        while(!q.empty()){
            auto [curr,step] = q.front();q.pop();
            if(curr==n*n) return step;

            for(int dice=1;dice<=6;dice++){
                int next = curr+dice;
                if(next>n*n) break;
                if(v[next]!=-1) next=v[next];
                if(!visited[next]){
                    visited[next]=true;
                    q.push({next,step+1});
                }
            }
        }
        return -1;
    }
};
