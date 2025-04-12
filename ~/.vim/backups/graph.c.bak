#include <stdio.h>
#include <stdlib.h>
#include <string.h>

static char buffer[8];
static int choice; 

typedef enum{ true = 1,false=0} bool;

bool fill(int toadd[],int lenNodes);
void fillMat(int lenNodes, int adjmat[lenNodes][lenNodes],int toadd[]);
void printMatrix(int nodes,int adjmat[nodes][nodes]);
void printNeighors(int lenNodes,int adjmat[lenNodes][lenNodes], int i);

int main(){
    bool defAult = true;
    //    char buffer[8];
    //   int choice;
begin:
    printf("Create Adjacency Matrix (1)\nLoad Default (2)\nQuit (3)\nInput--> ");

    scanf("%s",buffer);      
    choice = atoi(buffer);
    int nodes;
    bool create = false;

    switch(choice){
        case 1:
            printf("How many elements? (<=26) --> ");
            scanf("%s",buffer);
            choice = atoi(buffer);
            nodes = choice;
            if(choice < 1|| choice >= 26){printf("Invalid input\n\n");goto begin;}
            create = true;
            break;
        case 2:
            nodes = 4;
            break;
        case 3: 
            return 0;
        default:
            goto begin;
    }

    printf("Nodes: %i\n",nodes);
    int toadd[nodes*nodes];

    if(create){
        if(fill(toadd,choice)) defAult = false;
        else printf("Error detected. Loading default...\n");
    }

    int adjmat[nodes][nodes];

    if(defAult){
        int defaultMat[4][4] = 
        {//        A B C D
            /* A */{0,1,1,1}, 
            /* B */{1,0,1,0},
            /* C */{1,1,0,0},
            /* D */{1,0,0,0}
        };
        memcpy(adjmat,defaultMat,sizeof(defaultMat));
    }else{
        fillMat(nodes,adjmat,toadd);
    }

    while(1){
        printf("Display Matrix (1)\nSearch element (2)\nQuit (3)\nInput--> ");
        if(!scanf("%s",buffer)) continue;
        choice = atoi(buffer);

        switch(choice){
            case 1:
                printMatrix(nodes,adjmat);
                break;
            case 2:
                printf("Which Element?(A,B,C,D) --> ");
                if(!scanf("%s",buffer)) continue;
                if(!(buffer[0] >= 'A' && buffer[0] <= 'D')) goto def;
                else printNeighors(nodes,adjmat,buffer[0] - 'A');
                break;
            case 3:
                goto quit;
            default:
def:
                    printf("Invalid Input\n\n");
                    break;
        }    }

quit:
    return 0;
}

bool fill(int toadd[], int lenNodes){
    char refRel = 'A'; 
    char refRow;
    int jlen;

    //    char buffer[8];
    //  int choice; 

    for(int i=0; i<lenNodes; ++i){
        refRow = 'A';
        int j = (refRow - 'A');
        jlen = j + lenNodes;
        for(;j<jlen; ++j){
            //printf("refRel: %c, refRow: %c\n",refRel,refRow);
            
            if(refRel == refRow){
                ++refRow;
                continue;
            }
weight:
            printf("Edge Weight between %c and %c? --> ",refRel,refRow);
            scanf("%s",buffer);
            choice = atoi(buffer);

            if(choice < 0 || choice > lenNodes){
                printf("Invalid weight.\n");
                goto weight;
            }else{
                ++refRow;
                toadd[j] = choice;
            }
        }
        ++refRel;
    }
    printf("\n");
    return true;
}


void fillMat(int lenNodes, int adjmat[lenNodes][lenNodes],int toadd[]){
    for(int i=0,k=0; i<lenNodes; ++i){
        for(int j=0; j<lenNodes; ++j){
            adjmat[i][j] = toadd[k++]; 
        }
    }
}



void printMatrix(int lenNodes,int adjmat[lenNodes][lenNodes]){
    char c = 'A';

    printf("  ");
    while(c<(lenNodes + 'A')) printf("%c ",c++);
    printf("\n");

    c = 'A';
    for(int i=0; i<lenNodes; ++i){
        printf("%c ",c++);
        for(int j=0; j<lenNodes; ++j){
            printf("%i ",adjmat[i][j]);
        }
        putchar('\n');
    }
    putchar('\n');
}

void printNeighors(int lenNodes,int adjmat[lenNodes][lenNodes], int i){
    for(int j=0; j<lenNodes; ++j){
        printf("%i ",adjmat[i][j]);
    }
    printf("\n\n");
}

