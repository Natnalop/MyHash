# Main
    
    public class Main {
        public static void main(String[] args) {
    
            MyHashSet<Integer> ints = new MyHashSet<>();
            ints.add(67);
            ints.add(25);
            ints.add(958);
            ints.add(333);
    
            ints.printSet();
            System.out.println("_________________________");
    
            ints.remove(958);
            ints.printSet();
            System.out.println("__________________________");
    
            ints.add(721);
            ints.printSet();
        }
    }
