# TreeInterviews
Minimum distance for the truck to deliver the order
package trees;

import java.util.LinkedList;
import java.util.Queue;

public class TruckRoute {
	public static void main(String args[]){
		 int arr[][] ={{1,1,0},{1,0,1},{1,1,9}};
		 int minDistance = minDistance(arr,3,3);
		 System.out.println("distance "+minDistance);
		 
		
	}

	private static int minDistance(int[][] arr, int i, int j) {
		Queue<Integer> rq = new LinkedList<Integer>();
		Queue<Integer> cq = new LinkedList<Integer>();
		int[] dr ={-1,1,0,0};
		int [] dc ={0,0,1,-1};
		int tempRow;
		int tempCol;
		
		
		int count=0;
		int row;
		int col;
		boolean reachedEnd = false;
		
		boolean visited[][] = new boolean[i][j];
		rq.add(0);
		cq.add(0);
		visited[0][0]=true;
		int nodesLeftInLayer = 1;
		int nodeInNextLayer =0;
		while(rq.size() > 0){
			row = rq.poll();
			col = cq.poll();
			
			if(arr[row][col] == 9){
				reachedEnd =true;
				break;
			}
			//exploreNeighbours
			
			for(int p=0;p<4;p++){
				tempRow = row +dr[p];
				tempCol = col + dc[p];
				
				if(tempRow<0 || tempCol<0){
					continue;
				}
				if(tempRow>=i ||tempCol>=j){
					continue;
				}
				if(visited[tempRow][tempCol]){
					continue;
				}
				if(arr[tempRow][tempCol]==0){
					continue;
				}
				
				rq.add(tempRow);
				cq.add(tempCol);
				 visited[tempRow][tempCol] = true;
				 //System.out.println("("+tempRow+","+tempCol+"),");
				 nodeInNextLayer++;
				
			}
			
			nodesLeftInLayer--;
			if(nodesLeftInLayer==0){
				nodesLeftInLayer= nodeInNextLayer;
				nodeInNextLayer=0;
				count++;
			}
			
		}
		 if(reachedEnd){
			 return count;
		 }
		
		
		return 0;
	}

	}
