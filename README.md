# Binary-Search-Tree
#include<stdio.h>
#include<stdlib.h>

struct Node
{
    int ele;
    struct Node *left,*right;
};

struct Node *root=NULL;

void insert(struct Node *root,struct Node *nn)
{
    //printf("Parent ele = %d , NN ele = %d\n",root->ele,nn->ele);
    if(root->ele > nn->ele)
    {
        if(root->left == NULL)
        {
            //printf("Inserting %d at Left  of the Parent Node as it is Smaller than %d\n\n",nn->ele,root->ele);
            root->left=nn;
        }
        else
        {
            //printf("Root->Left  is Not NULL - so Inserting Next\n");
            insert(root->left,nn);
        }
    }
    else
    {
        if(root->right == NULL)
        {
            //printf("Inserting %d at Right of the Parent Node as it is Greater than %d\n\n",nn->ele,root->ele);
            root->right=nn;
        }
        else
        {
            //printf("Root->Right is Not NULL - so Inserting Next\n");
            insert(root->right,nn);
        }
    }
}

void create_node(int num)
{
    struct Node *nn;
    nn=(struct Node *)malloc(sizeof(struct Node));
    nn->ele=num;
    nn->left=NULL;
    nn->right=NULL;
    if(root==NULL)
    {
        //printf("Root Node Inserted = %d\n\n",num);
        root=nn;
    }
    else
    {
        //printf("Inserting New Node = %d\n",num);
        insert(root,nn);
    }
}

void printInorder(struct Node* n) //LNR
{
    if (n != NULL)
    {
        printInorder(n->left);
        printf("\t%d ", n->ele);
        printInorder(n->right);
    }
}

void printPreorder(struct Node* n) //NLR
{
    if (n != NULL)
    {
        printf("\t%d ", n->ele);
        printInorder(n->left);
        printInorder(n->right);
    }
}

void printPostorder(struct Node* n) //NLR
{
    if (n != NULL)
    {
        printPostorder(n->left);
        printPostorder(n->right);
        printf("\t%d ", n->ele);
    }
}


void main()
{
    int arr[10]={8,5,6,4,7,9,3,1,2,0};

    for(int i=0;i<10;i++)
    {
        create_node(arr[i]);
    }

    printf("\nInorder traversal  \n");
    printInorder(root);

    printf("\nPrenorder traversal  \n");
    printPreorder(root);

    printf("\nPostnorder traversal  \n");
    printPostorder(root);
}

