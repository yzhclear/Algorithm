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

    bool contain(Key key){
        return contain(root, key);
    }

    Value* search(Key key){
        return search( root , key );
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

    // 查看以node为根的二叉搜索树中是否包含键值为key的节点
    bool contain(Node* node, Key key){

        if( node == NULL )
            return false;

        if( key == node->key )
            return true;
        else if( key < node->key )
            return contain( node->left , key );
        else // key > node->key
            return contain( node->right , key );
    }

    // 在以node为根的二叉搜索树中查找key所对应的value
    Value* search(Node* node, Key key){

        if( node == NULL )
            return NULL;

        if( key == node->key )
            return &(node->value);
        else if( key < node->key )
            return search( node->left , key );
        else // key > node->key
            return search( node->right, key );
    }
};
```
