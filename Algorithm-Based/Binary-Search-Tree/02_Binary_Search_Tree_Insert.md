一颗二分搜索树(BST)是一颗二叉树，其中每个结点都包含有一个Comparable的键(以及相关联的值)且每个结点的键都大于    
其左子树中的任意结点而小于右子树的任意结点的键。    
二分搜索树不一定是完全二叉树
二分搜索树查找元素、插入元素、删除元素的时间复杂度近乎都是O(logn)
```
template <typename Key, typename Value>
class BST{

private:
    struct Node{
        Key key;
        Value value;
        Node *left;
        Node *right;

        Node(Key key, Value value){
            this->key = key;
            this->value = value;
            this->left = this->right = NULL;
        }
    };

    Node *root;
    int count;

public:
    BST(){
        root = NULL;
        count = 0;
    }
    ~BST(){
        // TODO: ~BST()
    }

    int size(){
        return count;
    }

    bool isEmpty(){
        return count == 0;
    }

    void insert(Key key, Value value){
        root = insert(root, key, value);
    }

private:
    // 向以node为根的二叉搜索树中,插入节点(key, value)
    // 返回插入新节点后的二叉搜索树的根
    Node* insert(Node *node, Key key, Value value){

        if( node == NULL ){
            count ++;
            return new Node(key, value);
        }

        if( key == node->key )
            node->value = value;
        else if( key < node->key )
            node->left = insert( node->left , key, value);
        else    // key > node->key
            node->right = insert( node->right, key, value);

        return node;
    }
};


int main() {

    return 0;
}
```
