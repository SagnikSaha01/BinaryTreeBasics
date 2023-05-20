BinaryTree.java:
---------------
public class BinaryTree {
    public Node root;
    public int maxDepth = 0;
    public int temp = -1;
    public BinaryTree(char d,int dep){
        
        root = new Node (d,dep);
    }
    public void add(char data){
       root= recursiveAdd(root,data);
    }
    public Node recursiveAdd(Node current,char d){
       temp++;
        if(current == null){
            current = new Node(d,temp);
            return current;
        }
        if(current.data > d){
        current.left = recursiveAdd(current.left,d);
        }else{
        current.right = recursiveAdd(current.right,d);
        }
        if(temp > maxDepth){
            maxDepth = temp;
            temp = -1;
        }else{
            temp = -1;
        }
        return current;
    }
    public int getMaxDepth(){
        return maxDepth;
    }
   
    public void printAtDepth(Node current, int depth){
        if(depth > maxDepth){
            System.out.println("There are no nodes at that depth");
            
        }else{
            if(current == null){
             
                 return;
                }
         if(current.depth == depth){
               System.out.print(current.data + " ");
           }
            printAtDepth(current.left, depth);
            printAtDepth(current.right,depth);
 
        
    }
    return;
    }
    
   public void print(){
       System.out.println("Infix:");
       infixPrint(root);
       System.out.println("\nPrefix:");
       prefixPrint(root);
       System.out.println("\nPostfix:");
       postfixPrint(root);
   } 
    public boolean infixPrint(Node current){
        
        if(current == null){
            return true;
        }
            infixPrint(current.left);
            System.out.print(current.data + " ");
            infixPrint(current.right);
        
        return true;
        
    }
    public boolean prefixPrint(Node current){
        if(current == null){
            return true;
        }
        System.out.print(current.data + " ");
        prefixPrint(current.left);
        prefixPrint(current.right);
        
        return true;
        
    }
    public boolean postfixPrint(Node current){
        if(current == null){
            return true;
        }
        postfixPrint(current.left);
        postfixPrint(current.right);
        System.out.print(current.data + " ");
        return true;
    }
    public void toString(int depth){
        System.out.println("Nodes at depth of " + depth + ":");
        printAtDepth(root,depth);
        
    }
}

MyProgram.java:
--------------
import java.util.Scanner;

public class MyProgram
{
    public static void main(String[] args)
    {
        System.out.println("Please enter a word");
        Scanner in = new Scanner (System.in);
        String input = in.nextLine();
        BinaryTree tree = new BinaryTree(input.charAt(0),0);
        for(int x = 1; x < input.length(); x++){
       tree.add(input.charAt(x));
        }
      tree.print();
       
      System.out.println("\nThe max depth of the tree is: "+tree.getMaxDepth());
      System.out.println("Please enter a depth to print out");
      int val = in.nextInt();
      tree.toString(val);
      
    }
}

Node.java:
---------
public class Node {
   
   char data;
   Node right = null;
   Node left = null;
   int depth;
   public Node(char d, int dep){
       depth = dep;
       data = d;
   }
}

