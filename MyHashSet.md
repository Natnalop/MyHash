# MyHashSet
    
    import java.util.ArrayList;
    import java.util.List;
    
    public class MyHashSet<E> {
        private static final Object PRESENT = new Object();
        private final MyHashMap<E, Object> map;
    
        public MyHashSet() {
            this.map = new MyHashMap<>();
        }
        public boolean add(E element) {
            return this.map.put(element, PRESENT) == null;
        }
        public boolean remove(E key) {
            return this.map.remove(key) == PRESENT;
        }
        public void printSet() {
            List<Object> list = new ArrayList<>();
            for(Bucket b : this.map.buckets) {
                if(b != null) {
                    for(Pair p : b.getList()) {
                        list.add(p.getKey());
                    }
                }
            }
            System.out.println(list);
        }
    }
