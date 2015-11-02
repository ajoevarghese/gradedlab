//Monday 02 November 2015 08:20:17 AM IST 
import java.util.ArrayList;
import java.util.Scanner;
public class mainfn {
	public static void adj(int input[][],int max)
	{
		System.out.print("	");
		for (int  i = 1; i < max; i++)

            System.out.print( i+"	");
		for(int i=1; i<max; i++)
		{
			System.out.print("\n"+i+"	" );
			for(int j=1; j<max; j++)
			{
				System.out.print(input[i][j]+"	");
				
			}
			System.out.println();
		}
		

		
	}
	
	public static void neighbours(int check,int input[][],  int max)
	{
		if(check> max-1)
		{
			System.out.println("wrong input");
			return;
		}
		else
		{
			for(int i=1; i<max; i++)
			{
				if(input[check][i]==1) System.out.print(i+" ");
				else if(input[i][check]==1) System.out.print(i+" ");
			}
			
		}
	}
	
	public static boolean[][] pathfind(int[][]input, int max)
	{
		int path[][];
		path= new int[max][max];
		int k,c,d, sum=0, pathdeg=2;
		
		
        boolean[][] tc = new boolean[max][max];
        int i,j;

        for ( i = 1; i < max; i++) 

        {    

            for ( j = 1; j < max; j++) 

                if (input[i][j] != 0)

                    tc[i][j] = true;

           

        }

        for ( i = 1; i < max; i++) 

        {

            for ( j =1 ; j < max; j++) 

            {

                if (tc[j][i]) 

                    for ( k = 1; k < max; k++) 

                        if (tc[j][i] && tc[i][k]) 

                            tc[j][k] = true;             

            }

        }
        return tc;
		
	}
	
	public static void checkcycle(boolean[][] path, ArrayList<Integer> list, int max)
	{
		int upperlimit=list.size();
		boolean condition=true;
		for(int i=0; i<upperlimit; i++)
		{
			condition&=path[list.get(i)][list.get(i)];
	}
		if(condition==true)
		{
			System.out.println("cycle exists b/w the set of nodes you sent");
		}
		
		for(int i=1; i<max; i++)
		{
			
				if(path[i][i]==true)
				{
					System.out.println("there exists a cycle for sure in this graph"); 
				}
			
		}
	}

	public static void main(String[] args) {
		
		// TODO Auto-generated method stub
		int[][] input;
		input= new int[5][5];
		int max=5;
		input[2][1]=1;
		input[1][3]=1;
		input[3][4]=1;
		input[4][2]=1;
		/*input[3][6]=1;
		input[4][2]=1;
		input[4][6]=1;
		input[4][5]=1;
		input[6][5]=1;
		input[6][2]=1;*/
		int i, j;
		Scanner take=new Scanner(System.in);
		
		
		//to show the adjacency matrix
		System.out.println("\nadjacency matrix\n");
		adj(input, max);
		//to check on the neighbours
		
		System.out.println("enter the element for which you want to know the neighbours has to be less than "+(max-1));
		int check=take.nextInt();
		neighbours(check,input,max);
		System.out.println("\n");
		
		//to check for cycle
		boolean[][] path;
		path= new boolean[max][max];
		path=pathfind(input, max);
		for(i=1; i<max; i++)
		{
			for(j=1; j<max;j++)
			{
				 if (path[i][j]) 

                     System.out.print("1"+"	");

                 else                  

                     System.out.print("0"+"	");
			}
			System.out.println();
		}
		
		System.out.println("\nenter the set of nodes you want to check for cycle");
		ArrayList<Integer> list=new ArrayList<Integer>();
		int more;
		do
		{
			int e=take.nextInt();
			list.add(e);
			System.out.println("do u want to enter more?");
			 more=take.nextInt();
		}while(more==1);
		
		checkcycle(path, list,max);
		
		
		
		
		
	 

		
	}

}
