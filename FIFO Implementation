#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#define ARRAYSIZE(x)  (sizeof(x)/sizeof(*(x)))
#define N 10000;
/* Data should be in the format arc number, tail node, head node, length, opp. arc number if present */

int max(int a, int b)
    {
        return a>b ? a : b;
    }

int main()
    {
        /* Initially using an excel macro, all cell values of excel are multiplied by N and TRUNC function is used
        This is done to avoid the decimal points to be confused as delimiters */
        int max_row;
        const char filename[] = "networkinput.csv";
        /* Open the data file. */
        FILE *file = fopen(filename, "r");
        int array_read[5000][5];
        if ( file )
            {
                int array[5000][5];
                size_t i, j, k;
                char buffer[BUFSIZ], *ptr;
                /* Read each line from the file using fgets */
                for ( i = 0; fgets(buffer, sizeof buffer, file); ++i )
                    {
                        /*
                        Parse the comma-separated values from each line into 'array'. */
                        for ( j = 0, ptr = buffer; j < ARRAYSIZE(*array); ++j, ++ptr )
                            {
                                array[i][j] = (int)strtol(ptr, &ptr, 10);
                            }
                    }
                max_row=i;
                fclose(file);
                /* The array elements are fed into a new array which is float and contains the original values */

                for ( j = 0; j < i; ++j )
                    {
                        for ( k = 0; k < ARRAYSIZE(*array); ++k )
                            {
                                array_read[j][k]=(int)array[j][k]/N;
                            }
                    }
            }
        else /* If the file does not exist, error message pops up. */
            {
                perror(filename);
            }
        int source_node;
        int num_nodes=0;
        int i,j,k,l,m,n;
        printf("Please enter source node number:");
        scanf("%d", &source_node);
        printf("\nProcessing..");
        for (m=0; m<max_row ; m++)
            {
                num_nodes = max(array_read[m][1],num_nodes);
            }
        /*List to be explored*/
        int LIST[max_row+1];
        memset( LIST, 0, (max_row+1)*sizeof(int) );
        int PRELIST[num_nodes];
        memset( PRELIST, 0, (num_nodes)*sizeof(int) );
        LIST[0] = source_node;
        PRELIST[source_node-1] = 1;
        int Final_data[num_nodes][3];
        /*Node number, reachability, predecessor*/
        //The For loop below initializes the Final Data matrix
        for(m=0;m<num_nodes;m++)
            {
                Final_data[m][0] = m+1;
                if (m==(source_node-1))
                    {
                        Final_data[m][1] = 1;
                        Final_data[m][2] = -1;
                    }
                else
                    {
                        Final_data[m][1] = 0;
                        Final_data[m][2] = 0;
                    }
            }
        int numite=0; //Number of iterations, just to decide if negative cycle exists.
        int ntbe = 0;
        k = 0;
        n = 1;
        do
        {
            if (numite>max_row)
                {
                    printf("There is a cycle in the network.");
                    break;
                }
            numite++;

            ntbe = LIST[k];
            PRELIST[ntbe-1] = 0;
            k++;
            for (l=0; l<max_row;l++)
                {
                    if (array_read[l][1] == ntbe)
                        {
                            if (PRELIST[(array_read[l][2] - 1)] == 0)
                                {
                                    LIST[n] = array_read[l][2];
                                    Final_data[array_read[l][2] - 1][1] = 1;
                                    Final_data[array_read[l][2] - 1][2] = ntbe;
                                    PRELIST[array_read[l][2]-1] = 1;
                                    n++;
                                }
                        }
                }
        }while (ntbe != 0);
        printf("\nNode \t Is accessible \t Predecessor \n");
        for(i=0;i<num_nodes; i++)
            {
                    for (j=0;j<3;j++)
                        {
                         printf("%d \t\t",Final_data[i][j]);
                        }
                    printf("\n");
            }
        return 0;
    }
