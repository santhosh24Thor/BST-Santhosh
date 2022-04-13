# BST-Santhosh
#Implementation of Binary Search tree 

#include<stdio.h>
#include<stdlib.h>

struct node
{
  int data;
  struct node*left;
  struct node*right;
};
typedef struct node TREENODE;
TREENODE*current = NULL;

TREENODE* minValue(TREENODE* temp)
{
    TREENODE*current = temp;
    while(current->left!=NULL)
    {
        current = current->left;

    }
    return current;
}

int max(int a,int b)
{
    if(a<b)
    {
        return b;
    }
    else if(a>b)
    {
        return a;
    }
    else
    {
        return a;
    }
}

TREENODE* insertNode(TREENODE*temp, int value)
{
    if(temp == NULL)
    {
        TREENODE* ptr = malloc(sizeof(TREENODE));
        ptr->data = value;
        ptr->left = ptr->right = NULL;
        temp = ptr;
    }
    else
    {
        if(temp->data>value){
            temp->left = insertNode(temp->left,value);
        }
        else if(temp->data<value){
            temp->right = insertNode(temp->right,value);
        }
        return temp;
    }
}

void inOrder(TREENODE*temp)
{
    if(temp!=NULL){
        inOrder(temp->left);
        printf("%d\n",temp->data);
        inOrder(temp->right);
    }
}

void preOrder(TREENODE*temp)
{
    if(temp!=NULL){
        printf("%d\n",temp->data);
        preOrder(temp->left);
        preOrder(temp->right);
    }
}

void postOrder(TREENODE*temp)
{
    if(temp!=NULL){
        postOrder(temp->left);
        postOrder(temp->right);
        printf("%d\n",temp->data);
    }
}

TREENODE* delNode(TREENODE*temp, int value)
{
    if(temp == NULL)
    {
        printf("Data not Found \n");
        return temp;
    }
    else if(value<temp->data){
        temp->left = delNode(temp->left,value);
    }
    else if(value>temp->data){
        temp->right = delNode(temp->right,value);
    }
    else
    {
        if(temp->left == NULL)
        {
            TREENODE*current = temp->right;
            free(temp);
            return current;
        }
        else if(temp->right == NULL)
        {
            TREENODE*current = temp->left;
            free(temp);
            return current;
        }
        TREENODE* current = minValue(temp->right);
        temp->data = current->data;
        temp->right = delNode(temp->right,current->data);
    }
    return temp;
}

TREENODE* search(TREENODE*temp, int value)
{
    if(temp == NULL)
    {
        return NULL;
    }
    else
    {
        if(temp->data>value)
        {
            return search(temp->left,value);
        }
        else if(temp->data<value)
        {
            return search(temp->right,value);
        }
        else if(temp->data == value)
        {
            return temp;
        }
    }
}

int Height(TREENODE* temp)
{
    if(temp == NULL)
    {
        return -1;
    }
    else if(temp->left == NULL && temp->right == NULL)
    {
        return 0;
    }
    else
    {
        return 1 + max(Height(temp->left),Height(temp->right));
    }
}

//-----------------------------------------------------------------------------------------

main()
{
    TREENODE* root = NULL;
    int ch;
    int data;
    TREENODE* element = NULL;
    printf("1.Insert\n2.Delete\n3.InOrder Treversal\n4.PreOrder Treversal\n5.PostOrder Treversal\n6.Search\n7.Height\n8.Exit\n");
    while(1)
    {
        printf("Enter your choice : ");
        scanf("%d",&ch);
        if(ch==1)
        {
            printf("Enter value to be inserted : ");
            scanf("%d",&data);
            root = insertNode(root,data);
        }
        else if(ch == 2)
        {
            printf("Enter value to be deleted : ");
            scanf("%d",&data);
            root = delNode(root,data);
        }
        else if(ch == 3)
        {
            if(root == NULL)
            {
                printf("Nothing to Itrate\n");
                continue;
            }
            inOrder(root);
        }
        else if(ch == 4)
        {
            if(root == NULL)
            {
                printf("Nothing to Itrate\n");
                continue;
            }
            preOrder(root);
        }
        else if(ch == 5)
        {
            if(root == NULL)
            {
                printf("Nothing to Itrate\n");
                continue;
            }
            postOrder(root);
        }
        else if(ch == 6)
        {
            printf("Enter value to be searched : ");
            scanf("%d",&data);
            element = search(root,data);
            if(element!= NULL)
            {
                printf("Data is present in the Tree...\n");
            }
            else
            {
                printf("Data not availabe in the Tree...\n");
            }
        }
        else if(ch == 7)
        {
            int h = Height(root);
            printf("The height of the tree is %d \n",h);
        }
        else
        {
            break;
        }
    }
}

