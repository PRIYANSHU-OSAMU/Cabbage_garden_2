#date:8/22/25 , 10:50 pm
i have officially covered binary search tree entirely and written down the code and my mistakes:

#include<iostream>
using namespace std;


class Node{
public:         //if not declared public class members and methods are
    int data;   //private by default
    Node *left ;
    Node *right;
    Node(int value){
        this->data=value;
        this->left=nullptr;
        this->right=nullptr;
    }
};

Node* insert(int dval, Node*root){
    //Node noot = new Node(data);
    Node* noot = new Node(dval);//the above line is wrong because of wrong
    if(root==nullptr){          //datatype assignment , new keyword does heap allocation
        return noot;            //and returns pointer to the memory location
    }
    if(root->data==dval){
        cout<<"cant insert same number";
        return root;
    }
    if(root->data>dval){
        root->left=insert(dval,root->left);//dont worry it will return the right pointer
    }                                      //to the next node , and it will finally check out 
    if(root->data<dval){
        root->right=insert(dval,root->right);
    }
    return root;//helps in doing the correct pointer allocation 
}

Node* search (int dval,Node *root){
    if(root==nullptr){
        return root;
    }
    if(root->data==dval){
        return root;
    }
    if(root->data>dval){
        return search(dval,root->left);//essentially , returns in the same way insert function does
    }
    else{
        return search (dval, root->right);
    }
    // return nullptr;//probably would do anyway but for return type, dont need to do compilers smart
}

int findmin(Node* root){
    if(root==nullptr){
        return -1;
    }
    while(root->left!=nullptr){
        root=root->left;
    }
    return root->data;
}
int findmax(Node* root){
    if(root==nullptr){
        return -1;
    }
    while(root->right!=nullptr){
        root=root->right;
    }
    return root->data;
}
void inorder (Node* root){
    if (root == nullptr) {
     	   return;
    	}
    	inorder(root->left);
    	std::cout << root->data << " ";
    	inorder(root->right);
    }
int main(){
    Node* nd = new Node(20);
    nd = insert(10,nd);
    nd= insert(30,nd);
    nd= insert(13,nd);
    cout<<"minimum value is :"<<findmin(nd)<<endl;//return 10 as expected
    Node* nd2 = search(99,nd);
    if(nd2!=nullptr){
    cout<<nd2->data<<endl;}//checks out for the correct search
    else{cout<< "value not found"<<endl;}
    cout<<findmax(nd)<<endl;//returns 30 checks out
    inorder(nd);}

i ll take some good sleep now :)
