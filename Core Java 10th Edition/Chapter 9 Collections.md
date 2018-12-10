# Chapter 9
## 9.1 The Java Collections Framework
- As of Java SE 8, you can call ```forEachRemaining``` method with a lambda expression that consumes an element:
    - ```iterator.forEachRemaining(element -> do something with element);```
- Think of Java iterators as being **between elements**. When you call ```next```, the iterator *jumps over* the next element, and it returns a reference to the element that it just passed.

## 9.2 Concrete Collections
- Linked List
    - Effecient for insert and remove element from the middle of a list.
    - Not good at random accessing.
- Array List
    - Reverse of Linked List
- Hash Sets
    - Unordered set for effecient lookup.
- Tree Sets
    - Sorted set
- Queues and Deques
    - Queues: add element at the end and remove from the head
    - Deque: operate on both ends
- Priority Queues
    - Effeciently return the minimal element
    - But not sorted
    - Use heap data structure

## 9.3 Maps
- The hash or comparision function is applied only to the keys.
- Hash Map
    - Effecient for lookup
- Tree Map
    - Sorted by the key
- Map Views
    - ```Set<K> keySet()```
    - ```Collection<V> values()```
    - ```Set<map.Entry<K, V>> entrySet()```
- Invoking the ```remove``` method of the the iterator on the key set view will actually remove the key and associated value from the map. But you cannot ```add``` to the key set view.
- Weak Hash Maps
    - Garbage collector will remove the key/value pair that the key is no longer referenced.
- Linked Hash Sets and Maps
    - Remember in which order you inserted items.
    - Use doubly linked list data structure.
    - You can configure the data structure to store elements in access order.
- Enumeration Sets and Maps
    - Sets for Enum types
    - Maps' key belongs to Enum types
- Identity Hash Maps
    - Calculate key's hash value by memory location

## 9.5 Algorithms
- Sorting and Shuffling

```
List<String> staff = new LinkedList<>();
// fill collection
Collections.sort(staff);
staff.sort(Comparator.comparingDouble(Employee::getSalary));
staff.sort(Comparator.reverseOrder());
staff.sort(Comparator.comparingDouble(Employee::getSalary).reversed());
Collections.shuffle(staff);
```
- Binary search
```
i = Collections.binarySearch(c, element);
i = Collections.binarySearch(c, element, comparator);
```
- Simple Algorithms
```
words.removeIf(w -> w.length() <= 3);
words.replaceAll(String::toLowerCase);
```
- Bulk Operations
```
coll1.removeAll(coll2);
coll1.retainAll(coll2);

// Intersection of a and b
Set<String> result = new HashSet<>(a);
result.retainAll(b);

// Remove terminated employees
Map<String, Employee> staffMap = ...;
Set<String> terminatedIDs = ...;
staffMap.keySet().removeAll(terminatedIDs);

// Sublist
relocated.addAll(staff.subList(0, 10));
staff.subList(0, 10). clear();
```
- Converting between Collections and Arrays
```
String[] values = ...;
HashSet<String> staff = new HashSet<>(Arrays.asList(values));

// toArray() return an array of Object and it can't be changed.
// Use this:
String[] values = staff.toArray(new String[0]);
```
- Property Maps: ```Properties```
    - The keys and values are strings.
    - The table can be saved to a file and loaded from a file.
    - A secondary table for defaults is used.
- Bit Sets
```
bucketOfBits.get(i);    // return true if set
bucketOfBits.set(i);    // turn on
bucketOfBits.clear(i);  // turn off
```
