# Bucket
    
    import java.util.LinkedList;
    import java.util.List;
    
    public class Bucket {
       private final List<Pair> list;
    
       public Bucket() {
           this.list = new LinkedList<>();
       }
       public void addPair(Pair p) {
           this.list.add(p);
       }
       public void removePair(Pair p) {
           this.list.remove(p);
       }
    
        public List<Pair> getList() {
            return this.list;
        }
    }
