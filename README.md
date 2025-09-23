# 🎯 Реализация HashMap и HashSet на Java
Этот проект демонстрирует реализацию хэш-таблиц с нуля. Классический пример того, как устроены HashMap и HashSet из Java Collections Framework.

# 📁 Структура проекта
1. _Pair<K, V>_ - Базовая пара ключ-значение
  
        java
        public class Pair<K, V> {
            private final K key;  // Ключ (неизменяемый)
            private V value;      // Значение (можно менять)
        }

2. _Bucket_ - Ведро хэш-таблицы

        java
        public class Bucket {
            private final List<Pair> list;  // Цепочка пар для разрешения коллизий
        }


Хранит список пар с одинаковым хэшем

Реализует метод цепочек для разрешения коллизий

3. _MyHashMap<K, V>_ - Основная хэш-таблица

   
        java
        public class MyHashMap<K, V> {
            private final int capacity = 10;     // Размер таблицы
            public final Bucket[] buckets;       // Массив ведер
            private int size = 0;                // Количество элементов
        }

4. _MyHashSet<E>_ - Множество на основе HashMap

        java
        public class MyHashSet<E> {
            private static final Object PRESENT = new Object();  // Фиктивное значение
            private final MyHashMap<E, Object> map;             // Делегирование логики
        }

# 🔧 Как работает хэширование
Метод _hash()_:

    java
    private int hash(K key) {
        return Math.abs(key.hashCode()) % this.capacity;
    }

_key.hashCode()_ - получаем хэш-код ключа

_Math.abs()_ - берем абсолютное значение

% capacity - ограничиваем размером таблицы (0-9)

Пример:

key = 25 → hashCode() = 25 → 25 % 10 = 5 → ведро #5

# ⚡ Основные операции
Добавление элемента (put):

    java
    public V put(K key, V value) {
        if(containsKey(key)) {  // Если ключ уже существует
            Pair<K, V> pair = getPair(key);
            pair.setValue(value);  // Обновляем значение
            return oldValue;
        }
    
    int hash = hash(key);
    if(buckets[hash] == null) {
        buckets[hash] = new Bucket();  // Создаем новое ведро
    }
    buckets[hash].addPair(new Pair<>(key, value));
    size++;
    return null;
    }
Разрешение коллизий методом цепочек:

    text
    Ведро #5: [25=value1] → [35=value2] → [15=value3]
    Все ключи с хэшем=5 хранятся в одном связном списке

# 🎨 Архитектурные паттерны
1. Делегирование (Delegation Pattern)

        java
        public class MyHashSet<E> {
           private final MyHashMap<E, Object> map;
           public boolean add(E element) {
           return map.put(element, PRESENT) == null;
           }
        }

_MyHashSet_ делегирует всю логику MyHashMap, используя фиктивные значения

3. Композиция vs Наследование
Проект использует композицию - более гибкий подход, чем наследование

# 📊 Визуализация работы
Исходные данные:

      java
      ints.add(67);   // hash = 67 % 10 = 7
      ints.add(25);   // hash = 25 % 10 = 5  
      ints.add(958);  // hash = 958 % 10 = 8
      ints.add(333);  // hash = 333 % 10 = 3

Структура хэш-таблицы:

    text
    Bucket[0]: null
    Bucket[1]: null
    Bucket[2]: null
    Bucket[3]: [333]
    Bucket[4]: null
    Bucket[5]: [25]
    Bucket[6]: null
    Bucket[7]: [67]
    Bucket[8]: [958]
    Bucket[9]: null
