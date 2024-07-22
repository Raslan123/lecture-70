# lecture-70
#include <iostream>
using namespace std;

// Node class
class Node {
public:
    int key;
    Node* left;
    Node* right;

    Node(int key) {
        this->key = key;
        left = right = nullptr;
    }
};

// BinarySearchTree class
class BinarySearchTree {
public:
    Node* root;

    BinarySearchTree() {
        root = nullptr;
    }

    // Insert a node
    void insert(int key) {
        root = insertRec(root, key);
    }

    // Search for a node
    bool search(int key) {
        return searchRec(root, key) != nullptr;
    }

    // Delete a node
    void deleteNode(int key) {
        root = deleteRec(root, key);
    }

    // Inorder traversal
    void inorder() {
        inorderRec(root);
        cout << endl;
    }

    // Preorder traversal
    void preorder() {
        preorderRec(root);
        cout << endl;
    }

    // Postorder traversal
    void postorder() {
        postorderRec(root);
        cout << endl;
    }

private:
    // Helper function to insert a node
    Node* insertRec(Node* node, int key) {
        if (node == nullptr) {
            return new Node(key);
        }
        if (key < node->key) {
            node->left = insertRec(node->left, key);
        } else if (key > node->key) {
            node->right = insertRec(node->right, key);
        }
        return node;
    }

    // Helper function to search for a node
    Node* searchRec(Node* node, int key) {
        if (node == nullptr || node->key == key) {
            return node;
        }
        if (key < node->key) {
            return searchRec(node->left, key);
        }
        return searchRec(node->right, key);
    }

    // Helper function to delete a node
    Node* deleteRec(Node* root, int key) {
        if (root == nullptr) {
            return root;
        }

        if (key < root->key) {
            root->left = deleteRec(root->left, key);
        } else if (key > root->key) {
            root->right = deleteRec(root->right, key);
        } else {
            if (root->left == nullptr) {
                Node* temp = root->right;
                delete root;
                return temp;
            } else if (root->right == nullptr) {
                Node* temp = root->left;
                delete root;
                return temp;
            }

            Node* temp = minValueNode(root->right);
            root->key = temp->key;
            root->right = deleteRec(root->right, temp->key);
        }
        return root;
    }

    // Helper function to find the minimum value node
    Node* minValueNode(Node* node) {
        Node* current = node;
        while (current && current->left != nullptr) {
            current = current->left;
        }
        return current;
    }

    // Helper function for inorder traversal
    void inorderRec(Node* root) {
        if (root != nullptr) {
            inorderRec(root->left);
            cout << root->key << " ";
            inorderRec(root->right);
        }
    }

    // Helper function for preorder traversal
    void preorderRec(Node* root) {
        if (root != nullptr) {
            cout << root->key << " ";
            preorderRec(root->left);
            preorderRec(root->right);
        }
    }

    // Helper function for postorder traversal
    void postorderRec(Node* root) {
        if (root != nullptr) {
            postorderRec(root->left);
            postorderRec(root->right);
            cout << root->key << " ";
        }
    }
};

int main() {
    BinarySearchTree bst;

    bst.insert(50);
    bst.insert(30);
    bst.insert(20);
    bst.insert(40);
    bst.insert(70);
    bst.insert(60);
    bst.insert(80);

    cout << "Inorder traversal: ";
    bst.inorder();
    cout << "Preorder traversal: ";
    bst.preorder();
    cout << "Postorder traversal: ";
    bst.postorder();



    cout << "Search for 40: " << (bst.search(40) ? "Found" : "Not Found") << endl;
    cout << "Search for 25: " << (bst.search(25) ? "Found" : "Not Found") << endl;




    bst.deleteNode(20);
    cout << "Inorder traversal after deleting 20: ";
    bst.inorder();
    cout << "Preorder traversal after deleting 20: ";
    bst.preorder();
    cout << "Postorder traversal after deleting 20: ";
    bst.postorder();



    bst.deleteNode(30);
    cout << "Inorder traversal after deleting 30: ";
    bst.inorder();
    cout << "Preorder traversal after deleting 30: ";
    bst.preorder();
    cout << "Postorder traversal after deleting 30: ";
    bst.postorder();



    bst.deleteNode(50);
    cout << "Inorder traversal after deleting 50: ";
    bst.inorder();
    cout << "Preorder traversal after deleting 50: ";
    bst.preorder();
    cout << "Postorder traversal after deleting 50: ";
    bst.postorder();

    return 0;
}
