this folder is heap introduction

''''
#include<stdio.h>
#include<stdlib.h>

int main(void)
{
    int iMatrixNumber;
 
    scanf("%d", &iMatrixNumber);
    int iaMatrixRowCol[iMatrixNumber][2];
    for(int i = 0; i< iMatrixNumber; i ++)
    {
        scanf("%d %d", &iaMatrixRowCol[i][0],  &iaMatrixRowCol[i][1]);
    }
    // read the formula
    char caString[100];
    int iLeftBracket[100] = {-1};
    int iLeftBrackPointer = -1;  
    int iCount = 0;
    scanf("%s",caString);
    // initialize stack pointer, -1 means it is emptey
    int top = -1;
    int pos = 0;
    
    int iaStack[iMatrixNumber][2];
    for(int i = 0; i < strlen(caString); i++)
    {
        // maintain the left bracket
        if(caString[i] =='(')
        {
            iLeftBrackPointer++;
            iLeftBracket[iLeftBrackPointer] = top + 1; 
        }
        
        if(caString[i] >='A' && caString[i] <='Z')
        {
            // copy the corresponding matrix data into stack;
            ++top;
            iaStack[top][0] = iaMatrixRowCol[pos][0];
            iaStack[top][1] = iaMatrixRowCol[pos][1];
            pos ++;
        }
        
        // when see the ')' start the computation from last '('
        if(caString[i] ==')')
        {
            int j;
            for ( j = iLeftBracket[iLeftBrackPointer]; j < top; j++)
            {
                iCount += iaStack[iLeftBracket[iLeftBrackPointer]][0]*iaStack[j+1][0]*iaStack[j+1][1];
            }
            iaStack[iLeftBracket[iLeftBrackPointer]][1] = iaStack[j][1];
            top = iLeftBracket[iLeftBrackPointer];
            iLeftBrackPointer -= 1;
        }
        
    }
    
    printf("%d", iCount);
    
    return 0;
}

''''
