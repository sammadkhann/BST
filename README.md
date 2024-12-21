# BST
TreeNode.h
#include<iostream>
using namespace std;

class TreeNode {
private:
	int key;
	TreeNode* left;
	TreeNode* right;


public:
	TreeNode();
	TreeNode(int);
	int getKey();
	void setKey(int);
	TreeNode* getLeft();
	TreeNode* getRight();
	void setLeft(TreeNode*);
	void setRight(TreeNode*);


};

tree.h
#include"TreeNode.h"
using namespace std;

class Tree {
private:
	TreeNode* root;

public:
	Tree();
	bool isEmpty();
	void insert(int);
	TreeNode* findPlace(int);
	void display();
	void inorder(TreeNode*);

};

imp

#include"Tree.h"
#include<iostream>
using namespace std;

//---------- TreeNode------

TreeNode::TreeNode() {
    key = -1;
    left = NULL;
    right = NULL;

}

TreeNode::TreeNode(int key) {
    this->key = key;
    left = NULL;
    right = NULL;

}

void TreeNode::setKey(int key) {
    this->key = key;
}

void  TreeNode::setLeft(TreeNode* left) {
    this->left = left;
}

void TreeNode::setRight(TreeNode* right) {
    this->right = right;
}

int TreeNode::getKey() {
    return key;
}

TreeNode* TreeNode::getLeft() {
    return left;
}

TreeNode* TreeNode::getRight() {
    return right;
}


//------ Tree --------

Tree::Tree() {
    root = NULL;
}

bool Tree::isEmpty() {
    if (root == NULL) {
        return true;
    }
    else {
        return false;
    }
}

TreeNode* Tree::findPlace(int key) {
    TreeNode* temp = root;
    TreeNode* parent = NULL;

    while (temp != NULL) {
        if (temp->getKey() == key) {
            return NULL;
        }
        parent = temp;
        if (temp->getKey() > key) {
            temp = temp->getLeft();
        }
        else {
            temp = temp->getRight();
        }
    }

    return parent;
}

void Tree::insert(int key) {
    if (isEmpty()) {
        root = new TreeNode(key);
        return;
    }

    TreeNode* parent = findPlace(key);
    if (parent == NULL) {
        cout << "Duplication not allowed" << endl;
        return;
    }

    TreeNode* newNode = new TreeNode(key);
    if (key < parent->getKey()) {
        parent->setLeft(newNode);
    }
    else {
        parent->setRight(newNode);
    }
}

void Tree::display()
{
    inorder(root);

}

void Tree::inorder(TreeNode* temp) {
    if (temp != NULL) {
        inorder(temp->getLeft());
        cout << temp->getKey() << endl;
        inorder(temp->getRight());
    }
}

main

#include <iostream>
#include "Tree.h"
using namespace std;

void displayMenu() {
    cout << "\n--- Binary Search Tree Operations ---" << endl;
    cout << "1. Insert a Node" << endl;
    cout << "2. Display Tree (Inorder Traversal)" << endl;
    cout << "3. Exit" << endl;
    cout << "Enter your choice: ";
}

int main() {
    Tree tree1;
    int choice, value;

    do {
        displayMenu();
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter the value to insert: ";
            cin >> value;
            tree1.insert(value);
            cout << "Inserted " << value << " into the tree." << endl;
            break;

        case 2:
            cout << "Inorder Traversal of the Tree:" << endl;
            tree1.display();
            break;

        case 3:
            cout << "Exiting program. Goodbye!" << endl;
            break;

        default:
            cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 3);

    return 0;
}
