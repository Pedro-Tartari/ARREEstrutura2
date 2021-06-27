# Árvore Binária

## O que é
___

As árvores são utilizadas para construir e manter listas, principalmente de forma ordenada.
Para construção de uma árvore, temos os seguintes componentes: Raiz, Nós e Folhas.

![Imagem de Lista1](https://lh4.googleusercontent.com/W0AP6eYcHo2sxPl9qTe2FIi1RogDOVA3IVhaCE4vO-XTCw_Y3CWOXdoXyKiVMVa-CJpxDj6JLAmZRU38zUSHX1CDOlXXtzvuR6fcucS5hCAkIHYTQ-DyegjTkFwgbxU54j12kdze)

A raiz é começo de uma árvore, dessa raiz podemos ir para dois lados, esquerdo (L) e direito ('R) ramificando em números menores que a raiz e os maiores respectivamente. No nível 2, na foto, podemos ver os nós que também tem  suas ramificações e caso cheguem ao final sem modificações se tornam folhas. 

>>Outra forma de se olhar é em relação ao parentesco, podendo ser Pai, Filho ou descendente. 

![](https://lh6.googleusercontent.com/3L2sbo6sZpueD08TfvI5F4B4RmZxedIQwBdvmqOYhCzbvMPJr2vwdY4jcv88cVCQKKUen7bp4qaH6SiZfjZ9shL9okP6obLsJVIuZtBx5GJKgZlgtRpgkF8BGKA4rOHZSqvQqQjv)

## Árvore Não Balanceada
___
A árvore não balanceada pode se definir de duas formas, um padrão linear como nas imagens mostradas abaixo ou então na má distribuição de  futuros nós, na qual o ramo à esquerda pode conter mais inserções do que o lado direito, por exemplo. Dessa forma, a inserção, busca  e remoção dos elementos a  serem feitas será  exponencial, seguindo a quantidade de itens, 0(n).

  ![](https://lh6.googleusercontent.com/ZgoKlCrzuYwVegxUB4cF36QHW6D9uuQjwADRL2wypY7EECLEig3ZMpjZ3UThEn023iNYzga-jCMw3PSyi3hs4H_7FMGpwHz012jFEILw5HZL9V5ZePlLEgrrtTUAHWc6wvQyfPJf)
 

```Java
package pkg;

public class BinaryTree {
    private Node root;

    public boolean isEmpty(){
        if(root == null){
            return true;
        }
        return false;
    }
    
    public int getAltura(){
        return getAltura(this.root);
    }
    
    private int getAltura(Node root){
        if(root == null){
            return 0;
        }
        int altEsq = getAltura(root.getNoEsquerda());
        int altDir = getAltura(root.getNoDireita());
        if(altEsq > altDir){
            return altEsq + 1;
        } else {
            return altDir + 1;
        }
    }
    
    public int getQtdNode(){
        return getQtdNode(root);
    }
    
    private int getQtdNode(Node root){
        if(root == null){
            return 0;
        }
        int qtdNodeEsq = getQtdNode(root.getNoEsquerda());
        int qtdNodeDireita = getQtdNode(root.getNoDireita());
        return qtdNodeEsq + qtdNodeDireita + 1;
    }
    
    public void imprimirArvore(){
        if(this.root == null)
            System.out.println("Árvore vazia");
        else
            imprimirArvore(this.root);
    }
    
    private void imprimirArvore(Node node){
        if(node.getNoEsquerda() != null){
            imprimirArvore(node.getNoEsquerda());
        }
        if (node.getNoDireita() != null){
            imprimirArvore(node.getNoDireita());
        }
        System.out.println("Nó: " + node.getValor());
    }
    
    public void inserir(int valor){
        inserir(this.root, valor);
    }
    
    public void inserir(Node node, int valor) {
        if(this.root == null){
            this.root = new Node(valor);
        } else {
            if (valor < node.getValor()) {
                if (node.getNoEsquerda() != null) { 
                    inserir(node.getNoEsquerda(), valor); 
                } else { 
                    //Se nodo esquerdo vazio insere o novo no aqui 
                    node.setNoEsquerda(new Node(valor)); 
                } 
                //Verifica se o valor a ser inserido é maior que o no corrente da árvore, se sim vai para subarvore direita 
            } else if (valor > node.getValor()) { 
                //Se tiver elemento no no direito continua a busca 
                if (node.getNoDireita() != null) { 
                    inserir(node.getNoDireita(), valor); 
                } else {
                    //Se nodo direito vazio insere o novo no aqui 
                    node.setNoDireita(new Node(valor)); 
                } 
            }
        }
    }
    
    public Node remover(int valor) throws Exception{
        return remover(this.root, valor);
    }
    
    private Node remover(Node node, int valor) throws Exception{
        if(this.root == null){
            throw new Exception("Árvore vazia");
        } else {            
            if(valor < node.getValor()){
                node.setNoEsquerda(remover(node.getNoEsquerda(), valor));
            } else if(valor > node.getValor()){
                node.setNoDireita(remover(node.getNoDireita(), valor));
            } else if (node.getNoEsquerda() != null && node.getNoDireita() != null) {
                /*2 filhos*/  
                System.out.println("  Removeu No " + node.getValor());
                node.setValor(encontraMinimo(node.getNoDireita()).getValor());
                node.setNoDireita(removeMinimo(node.getNoDireita()));
            } else {  
                System.out.println("  Removeu No " + node.getValor());  
                node = (node.getNoEsquerda() != null) ? node.getNoEsquerda() : node.getNoDireita();  
            }  
            return node;
        }
    }
    
    private Node removeMinimo(Node node) {  
        if (node == null) {  
            System.out.println("  ERRO ");  
        } else if (node.getNoEsquerda() != null) {  
            node.setNoEsquerda(removeMinimo(node.getNoEsquerda()));  
            return node;  
        } else {  
            return node.getNoDireita();  
        }  
        return null;  
    }  
  
    private Node encontraMinimo(Node node) {  
        if (node != null) {  
            while (node.getNoEsquerda() != null) {  
                node = node.getNoEsquerda();  
            }  
        }  
        return node;  
    }
}
````
## Árvore Balanceada
___
A árvore balanceada por sua vez, tem a ideia de nós iguais em todos os níveis, seja para esquerda ou direita. Uma forma de se verificar é comparar se o nó de um nível mais alto (nível 2) é a metade do nível inferior (nível 3).

![](https://lh6.googleusercontent.com/xTM64ChBMBHmqNryiY1LXmkNV4psiAvrF7yeyjIjYBJy61F1OeRTQ2TD6Xdv4z_KKVZaX7gJWu_tRgXXwpcCfuZoKIBDrLoLv8M3IhaUHJldXuYQkNzPyFRdasDcwPpgO4Htcqhi)

Graças a essa forma de “montagem” seu tempo leva O(log(n)) para sua inserção, remoção e pesquisa, sendo muito mais rápido do que uma desbalanceada.

```Java
package pkg;
public class AvlTree {  
       private AvlNode root = null;  
  
       public AvlTree( ) {  
           root = null;  
       }  
         
       public void clear() {  
           root = null;  
       }  
       public boolean isEmpty() {  
           return root == null;  
       }  
         
       public AvlNode getRootNode (){  
           return root;  
       }  
         
       /** Retorna a altura da árvore */  
       private static int height( AvlNode t ) {  
           return t == null ? -1 : t.height;  
       }  
         
        /** 
        * Retorna o maior valor ente lhs e rhs. 
        */  
       private static int max( int lhs, int rhs ) {  
           return lhs > rhs ? lhs : rhs;  
       }  
         
       /** Retorna o fator de balanceamento da árvore com raiz t */   
       private int getFactor (AvlNode t) {  
           return height( t.left ) - height( t.right );  
       }  
         
       public boolean insert (int x) {  
           root = insert (x, root);  
           return true;  
       }  
         
       private AvlNode insert (int x, AvlNode t) {  
           if( t == null )  
               t = new AvlNode( x, null, null );  
           else if( x<t.key ) t.left = insert( x, t.left );  
           else if( x>t.key) t.right = insert( x, t.right );  
           t = balance (t);  
           return t;  
       }  
         
       public AvlNode balance (AvlNode t) {  
           if ( getFactor(t) == 2 ) {  
                   if (getFactor (t.left)>0) t = doRightRotation( t );  
                   else t = doDoubleRightRotation( t );  
           }  
           else if ( getFactor(t) == -2 ) {  
                   if ( getFactor(t.right)<0 ) t = doLeftRotation( t );  
                   else t = doDoubleLeftRotation( t );  
           }  
           t.height = max( height( t.left ), height( t.right ) ) + 1;  
           return t;  
       }  
  
       /** Faz Rotação simples a direita */  
       private static AvlNode doRightRotation( AvlNode k2 ) {  
           AvlNode k1 = k2.left;  
           k2.left = k1.right;  
           k1.right = k2;  
           k2.height = max( height( k2.left ), height( k2.right ) ) + 1;  
           k1.height = max( height( k1.left ), k2.height ) + 1;  
           return k1;  
       }  
  
       /** Rotação simples à esquerda */  
       private static AvlNode doLeftRotation( AvlNode k1 ) {  
           AvlNode k2 = k1.right;  
           k1.right = k2.left;  
           k2.left = k1;  
           k1.height = max( height( k1.left ), height( k1.right ) ) + 1;  
           k2.height = max( height( k2.right ), k1.height ) + 1;  
           return k2;  
       }  
  
       /** Rotação dupla à direita */  
       private static AvlNode doDoubleRightRotation( AvlNode k3 ) {  
           k3.left = doLeftRotation( k3.left );  
           return doRightRotation( k3 );  
      }  
  
       /** Rotação dupla à esquerda */  
       private static AvlNode doDoubleLeftRotation( AvlNode k1 ) {  
           k1.right = doRightRotation( k1.right );  
           return doLeftRotation( k1 );  
       }  
         
       public AvlNode search(int el) {  
           return search(root,el);  
       }  
       protected AvlNode search(AvlNode p, int el) {  
           while (p != null) {  
               /* se valor procuradp == chave do nó retorna referência ao nó */   
               if (el==p.key) return p;  
               /* se valor procurado < chave do nó, procurar na sub-árvore esquerda deste nó */  
               else if (el<p.key) p = p.left;  
               /* se valor procurado > chave do nó, procurar na sub-árvore direita deste nó */  
               else p = p.right;  
           }  
           // caso chave não foi achada, retorna null  
           return null;  
       }  
         
       public void inorder() {  
           inorder(root);  
       }  
       protected void inorder(AvlNode p) {  
           if (p != null) {  
                inorder(p.left);  
                System.out.print(p.key+" - ");  
                inorder(p.right);  
           }  
       }  
         
       public void preorder() {  
           preorder(root);  
       }  
       protected void preorder(AvlNode p) {  
           if (p != null) {  
                System.out.print(p.key + " ");  
                preorder(p.left);  
                preorder(p.right);  
           }  
       }  
         
       public void postorder() {  
           postorder(root);  
       }  
     
       protected void postorder(AvlNode p) {  
           if (p != null) {  
                postorder(p.left);  
                postorder(p.right);  
                System.out.print(p.key + " ");  
           }  
       }  
         
   protected AvlNode searchFather (int el) {  
       AvlNode p = root;  
       AvlNode prev = null;  
       while (p != null && !(p.key==el)) {  // acha o nó p com a chave el  
           prev = p;                             
           if (p.key<el)  
                 p = p.right;  
           else p = p.left;  
       }  
       if (p!=null && p.key==el) return prev;  
       return null;  
   }  
     
   /* método de autoria de Leonardo Zandoná - 2006/2 */  
   public void displayTree() {  
    if (isEmpty()){  
        System.out.println("Árvore vazia!");  
        return;  
    }             
    String separator = String.valueOf("  |__");  
    System.out.println(this.root.key+"("+root.height+")");  
    displaySubTree(root.left,  separator);  
    displaySubTree(root.right, separator);  
}  
private void displaySubTree(AvlNode node, String separator) {  
      
    if (node != null) {  
          
        AvlNode father = this.searchFather(node.key);  
        if (node.equals(father.left) == true) {  
            System.out.println(separator+node.key+"("+node.height+")"+" (ESQ)");  
        }else{  
            System.out.println(separator+node.key+"("+node.height+")"+" (DIR)");  
        }             
        displaySubTree(node.left,  "     "+separator);  
        displaySubTree(node.right, "     "+separator);  
    }  
}  
         
       public static void main (String args[]){  
           AvlTree t = new AvlTree();  
           t.insert(10);  
           t.insert(5);  
           t.insert(15);  
           t.insert(23);  
           t.insert(32);  
           t.insert(1);  
           t.insert(3);   
           t.displayTree();  
       }
}
```

## Exemplos Práticos

 - Árvores binárias são usadas na codificação Huffman , que são usadas como um código de compactação.
- As árvores binárias são usadas nas árvores de pesquisa binária , que são úteis para manter registros de dados sem muito espaço extra. 
- Árvores balanceadas são frequentemente usadas para implementar mapas ou conjuntos.
- Árvore de sintaxe: Construída por compiladores e calculadoras para analisar expressões.
- Árvores de hash: Usadas em programas p2p e assinaturas de imagem especializadas nas quais um hash precisa ser verificado, mas o arquivo inteiro não está disponível.

## Conclusão
Em pequenas quantidades de nós, as arvores não balanceadas e balanceadas acabam por não terem muitas diferenças, entretanto ao colocarmos em situações com milhões ou bilhões dados a árvore balanceada se destaca devido a sua fórmula `O(log(n))`. 
