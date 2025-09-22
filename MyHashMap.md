# MyHashMap

    public class MyHashMap<K, V> {
    
        private final int capacity = 10;
        public final Bucket[] buckets;
        private int size = 0;
    
        public MyHashMap() {
            this.buckets = new Bucket[this.capacity];
        }
    
        private int hash(K key) {
            return Math.abs(key.hashCode())%this.capacity;
        }
    
        public V put(K key, V value) {
            if(this.containsKey(key)) {
                Pair<K, V> pair = this.getPair(key);
                if(pair != null) {
                    pair.setValue(value);
                    return pair.getValue();
                } else {
                    return null;
                }
            }
            int hash = this.hash(key);
            if(this.buckets[hash] == null) {
                this.buckets[hash] = new Bucket();
            }
    
            this.buckets[hash].addPair(new Pair<>(key, value));
            this.size++;
            return null;
        }
    
        public V get(K key) {
            Pair<K, V> p = this.getPair(key);
            if(p == null) {
                return null;
            }
            return p.getValue();
        }
    
        private Pair<K, V> getPair(K key) {
            int hash = this.hash(key);
            if(this.buckets[hash] == null) {
                return null;
            }
            for(Pair<K, V> pair : this.buckets[hash].getList()) {
                if(pair.getKey().equals(key)) {
                    return pair;
                }
            }
            return null;
        }
    
        public boolean containsKey(K key) {
            return this.getPair(key) != null;
        }
    
        public V remove(K k) {
            if(this.containsKey(k)) {
                int hash = this.hash(k);
                Pair<K, V> pair = this.getPair(k);
                if(pair != null) {
                    this.buckets[hash].removePair(pair);
                    return pair.getValue();
                } else {
                    return null;
                }
            }
            return null;
        }
    
        public void printMap() {
            System.out.println("MyHashMap {");
            for(int i = 0; i < this.buckets.length; i++) {
                Bucket b = this.buckets[i];
                if(b != null) {
                    System.out.println("    Bucket #" + i + " {");
                    b.getList().forEach(pair -> {
                        System.out.println("        " + pair.getKey() + "=" + pair.getValue());
                    });
                    System.out.println("    }");
                    System.out.println();
                }
            }
            System.out.println("}");
        }
    }
    

