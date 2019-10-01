#include <iostream>
#include <vector>
#include <stack>

using namespace std;

#define MAX 30001
vector<int> graph[MAX];
int path[MAX];
bool loopExists = false;

void DFS(int src){
    stack<int> s;
    stack<int> currentLoop;

    path[src] = 0;
    s.push(src);
    currentLoop.push(src);

    while(!s.empty()){
        int u = s.top();
        s.pop();
        for(int i = 0; i < graph[u].size(); i++){
            int v = graph[u][i];
            if(path[v] == -1 || path[v] == 2){
                path[v] = 0;
                s.push(v);
                currentLoop.push(v);
            } else if(path[v] == 0){
                loopExists = true;
                return;
            }
        }
    }

    while(!currentLoop.empty()){ // change all paths in the current loop to 2 before moving on
        int w = currentLoop.top();
        path[w] = 2;
        currentLoop.pop();
    }
    return;
}

int main(){
    int t, n, m, a, b;
    cin >> t;
    
    for(int testCase = 0; testCase < t; testCase++){
        cin >> n >> m;

        for(int i = 1; i <= n; i++){
            path[i] = -1;
        }

        for(int i = 0; i < m; i++){
            cin >> a >> b;
            int tobeAdded = true;
            for(int j = 0; j < graph[a].size(); j++){ // only add the connection if b is not yet connected with a (avoid redundencies)
                if(b == graph[a][j]){
                    tobeAdded = false;
                    break;
                }
            }
            if(tobeAdded){
                graph[a].push_back(b);
            }
        }

        int currentCase = 1;
        while(currentCase <= n && !loopExists){
            if(path[currentCase] == -1){
                DFS(currentCase);
            }
            currentCase++;
        }

        if(loopExists){
            cout << "YES" << endl;
            loopExists = false;
        } else {
            cout << "NO" << endl;
        }

        currentCase = 1;
        for(int k = 0; k < m; k++){
            graph[k].clear();
        }

    }

}
