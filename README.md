# leetcode-from-zjd
describe the method of leetcode
leetcode:542.01.矩阵
problem description:给定一个由 0 和 1 组成的矩阵，找出每个元素到最近的 0 的距离。
                    两个相邻元素间的距离为 1 。
My solution:

class Solution {
    public int[][] updateMatrix(int[][] matrix) {
        int row=matrix.length,col=matrix[0].length;
        int[][] move={{0,1},{1,0},{0,-1},{-1,0}};
        int[][] dist=new int[row][col];
        LinkedList<int[]> li=new LinkedList<>();
        boolean flag=true;
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(matrix[i][j]==0){
                    li.offer(new int[]{i,j});
                }
                else {flag=false;}
            }
        }
        if(flag) return dist;
        int cnt=0;
        while(!li.isEmpty()){
            cnt++;
            int size=li.size();
            while(size>0){
                int[] m=li.poll();
                int x=m[0],y=m[1];
                for(int i=0;i<move.length;i++){
                    int x1=x+move[i][0],y1=y+move[i][1];
                    if(x1>=0 && x1<row && y1>=0 && y1<col){
                        if(matrix[x1][y1]==1){
                            matrix[x1][y1]=0;
                            dist[x1][y1]=cnt;
                            li.offer(new int[]{x1,y1});
                        }
                    }
                }
                size--;
            }
        }
        return dist;
    }
}
