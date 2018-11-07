### 二分搜索树的前中后序遍历
前序遍历：先访问根节点，再访问左子节点，最后访问右子节点   
中序遍历：先访问左子节点，再访问根节点，最后访问右子节点    
后序遍历：先访问左子节点，再访问右子节点，最后访问根节点   

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
       destroy( root );
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

   // 前序遍历
   void preOrder(){
       preOrder(root);
   }

   // 中序遍历
   void inOrder(){
       inOrder(root);
   }

   // 后序遍历
   void postOrder(){
       postOrder(root);
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

   // 对以node为根的二叉搜索树进行前序遍历
   void preOrder(Node* node){

       if( node != NULL ){
           cout<<node->key<<endl;
           preOrder(node->left);
           preOrder(node->right);
       }
   }

   // 对以node为根的二叉搜索树进行中序遍历
   void inOrder(Node* node){

       if( node != NULL ){
           inOrder(node->left);
           cout<<node->key<<endl;
           inOrder(node->right);
       }
   }

   // 对以node为根的二叉搜索树进行后序遍历
   void postOrder(Node* node){

       if( node != NULL ){
           postOrder(node->left);
           postOrder(node->right);
           cout<<node->key<<endl;
       }
   }

   void destroy(Node* node){

       if( node != NULL ){
           destroy( node->left );
           destroy( node->right );

           delete node;
           count --;
       }
   }
};
```
### 二叉搜索树的广度优先遍历以及深度优先遍历
```
// 广度优先遍历
void breadthFirstSearch(Node* root){

    queue<Node*> q;
    q.push(root);
    while( !q.empty() ){

        Node *node = q.front();
        q.pop();

        cout<<node->key<<endl;

        if( node->left )
            q.push( node->left );
        if( node->right )
            q.push( node->right );
    }
}

//深度优先遍历
void depthFirstSearch(Node* root){

    stack<Node*> s;  
    s.push(root);

    while(!s.empty()){
	    Node* node = s.top();
        nodeStack.pop();

        cout<<node->key<<endl;

        if(node->right){
            nodeStack.push(node->right);  //先将右子树压栈
        }
        if(node->left){
            nodeStack.push(node->left);  //再将左子树压栈
        }
    }
}
```
