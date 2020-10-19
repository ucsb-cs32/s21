---
num: "Lecture 6"
desc: "Hashing"
ready: true
lecture_date: 2020-10-20 14:00:00.00-7:00
---

# Hashing
* The ability to address unique key values in an array whose size may be smaller than the set of possible key values.
* Generally, keys are unique values that identify some record of information.
	* In order to put data (value) in the appropriate place in the collection, a hash function is required.
		* The hash function outputs a position in the collection based on the key value
		* Hash function outputs should be uniformly distributed
			* Or else all data would try to be stored in the same index.
		* For example, if you have array of 100 elements, a simple hash function could be:
			* key % 100 = [0-99]

![Hash Table](hashTable.png)

* Examples of hashing applications:
	* As a data structure (search)
	* Cryptography:
		* password verification
		* file verification 

* Hashing is very efficient for searching for data in an array.
	* Recall binary search: O(log n) search time (if elements are sorted).
	* Linear search: O(n) search time.
	* Hash Table search: O(1) average search time in unsorted order.
		* Hash Table searching provides instant access to an element in an array since the hash function computes the index where the data is stored.


## Collisions
* It's possible that two elements may be indexed to the same location.
	* This is known as collisions

## Open-address Hashing
* Collisions are resolved by placing the item in the next open spot in the array.
* For example, if a record is hashed to position i and data already exists in that index, then check the next available spot i+1, i+2, etc.
	* Known as linear probing
	* What is a problem with this mechanism?
		* Delayed Insertion – inserting an item in a crowded hash table takes time since it must look for an empty spot.
			* Elements are inserted farther away from their actual hashed index.
		* Clustering – When different keys are hashed to the same index, there may be groups of data records grouped in the same place.

![Open Address](openAddress.png)

## Example

```
//Makefile
CXX=g++

main: main.o hash.o
	${CXX} -o main -std=c++11 main.o hash.o

clean:
	rm -f *.o main
```

```
//hash.h
#include<list>
class Hash 
{ 
	private:
		int BUCKET;    // No. of buckets 
		int curr_size;
		std::list<int> *table; // Pointer to an array containing buckets 
	public: 
		Hash(int V);  // Constructor
		void insertItem(int x); // inserts a key into hash table 
		void searchItem(int key);
		void deleteItem(int key); // deletes a key from hash table 
		int hashFunction(int x); // hash function to map values to key
	 	void displayHash(); 
}; 
```

```
//hash.cpp
#include<iostream>
#include "hash.h"

using namespace std;

Hash::Hash(int b) 
{ 
	this->BUCKET = b; 
	table = new list<int>[BUCKET]; 
} 
  
void Hash::insertItem(int key) 
{ 
	if(curr_size == this->BUCKET){
		cout << "Cannot insert " << key << " -- table is full" << endl;
		return;
	}

	int index = hashFunction(key); 

	cout << "Inserting:" << key << " at index: " << index << endl;
	if(table[index].empty()){
		table[index].push_back(key);  
	}
	else{
		int new_index = index;
		while(true){
			cout << new_index << " was occupied -- trying next index " << endl;
			new_index = (new_index+1)%(this->BUCKET);
			if(table[new_index].empty()){
				table[new_index].push_back(key); 
				break;			
			}
		}
	}
	curr_size++;
} 
  
void Hash::deleteItem(int key) 
{ 
	// get the hash index of key 
	int index = hashFunction(key); 

	if(*(table[index].begin()) == key){
		table[index].erase(table[index].begin()); 
	}
	else{
		int new_index = index;
		while(true){
			new_index = (new_index+1)%(this->BUCKET);
			
			if(*(table[new_index].begin()) == key){
				table[new_index].erase(table[new_index].begin());
				curr_size--;
				break;			
			}
			if(new_index == index){
				cout << "Item not found" << endl;
				break;
			}
		}
	}

} 

void Hash::searchItem(int key) 
{ 
	// get the hash index of key 
	int index = hashFunction(key);
	if(*(table[index].begin()) == key){
		cout << "Item: " << key << " found at: " << index <<  endl;
	}
	else{
		int new_index = index;
		while(true){
			new_index = (new_index+1)%(this->BUCKET);
			
			if(*(table[new_index].begin()) == key){
				cout << "Item: " << key << " found at: " << new_index <<  endl; 
				break;			
			}
			if(new_index == index){
				cout << "Item not found" << endl;
				break;
			}
		}
	}
} 
  
// function to display hash table 
void Hash::displayHash() { 
	cout << endl << "Printing:" << endl;
	for (int i = 0; i < BUCKET; i++) { 
		cout << i; 
		for (auto x : table[i]) 
			cout << " --> " << x; 
		cout << endl; 
	} 
	cout << endl;
} 

int Hash::hashFunction(int x) { 
	return (x % BUCKET); 
} 
```

```
//main.cpp
#include "hash.h"

   
int main() 
{ 
	// array that contains keys to be mapped 
	int a[] = {15, 11, 27, 8, 12}; 
	//int a[] = {15, 11, 27, 8, 12, 18, 22}; 
	//int a[] = {15, 11, 27, 8, 12, 18, 22, 29}; 
	int n = sizeof(a)/sizeof(a[0]); // length of the array

	
	Hash h(7);   // 7 is count of buckets in hash table 

	// insert the keys into the hash table:
	h.displayHash();
	for (int i = 0; i < n; i++){ 
		h.insertItem(a[i]);   
		h.displayHash();
  	}

	h.searchItem(12); 
	h.deleteItem(12);
	h.displayHash();

	h.searchItem(8); 
	h.deleteItem(8); 
	h.displayHash();  

	return 0; 
} 
```

## Double Hashing
* Technique that uses a 2nd hash function when resolving a collision.
	* If a hash function index results in a collision, then use the 2nd hash function to determine how far to step in the array to look for an empty slot.
	* Helps reduce the clustering effect.
* Problems
	* If hash2 function is large, there is a possibility that we will go out of bounds.
	* Depending on the table size and hash2, it is possible that the index won’t be uniformly distributed.

![Double Hashing](doubleHashing.png)

## Example

```
// Add to hash.h
int hashFunction2(int x); // hash function to map values to key
```

```
// modify hash.cpp
  
void Hash::insertItem(int key) 
{ 

	if(curr_size == this->BUCKET){
		cout << "Cannot insert " << key << " -- table is full" << endl;
		return;
	}
	int index = hashFunction(key); 

	cout << "Inserting: " << key << " at index: " << index << endl;
	// second hashing:
	int index2 = hashFunction2(key);
	int i = 0;
	while(true){
		int new_index = (index + i * index2) % (this->BUCKET); 
		
		if(table[new_index].empty()){
			table[new_index].push_back(key); 
			break;			
		}
		cout << new_index << " was occupied -- trying next index " << new_index << endl;
		i++;
	}
	curr_size++;
} 
  
void Hash::deleteItem(int key) 
{ 
	// get the hash index of key 
	int index = hashFunction(key); 
	int index2 = hashFunction2(key);
	int i = 0;
	while(true){
		int new_index = (index + i * index2) % (this->BUCKET); 
		
		if(*(table[new_index].begin()) == key){
			table[new_index].erase(table[new_index].begin());
			curr_size--;
			break;
						
		}
		i++;
	}
} 

void Hash::searchItem(int key) 
{ 

	int index = hashFunction(key); 
	int index2 = hashFunction2(key);
	int i = 0;
	while(true){
		int new_index = (index + i * index2) % (this->BUCKET); 
		
		if(*(table[new_index].begin()) == key){
			cout << "Item: " << key << " found at: " << new_index <<  endl; 
			break;		
		}
		i++;
	}
} 
  
int Hash::hashFunction2(int x) { 
	return 5 - (x % 5); 
} 
```

## Chained Hashing
* The biggest problem to open-address hashing is 
	* If the table is full, no more elements can be added.
	* Similar to a vector, it could expand the capacity “under-the-hood” when needed, but…
		* All elements will probably have to be rehashed
		* New capacity shouldn’t be wasteful (too big) or too small
* Chained hashing (chaining)
	* If a collision occurs, then we store a series of data records in a list that the index in the hash table references.
	* Linked Lists are a common collection to store collided data records.

![Chaining](chaining.png)

## Example

```
// modify hash.cpp

void Hash::insertItem(int key) 
{ 
	int index = hashFunction(key); 
	table[index].push_back(key);  
	cout << "Inserting:" << key << " at index: " << index << endl;
} 
  
void Hash::deleteItem(int key) 
{ 
	// get the hash index of key 
	int index = hashFunction(key); 
	
	// find the key in (inex)th list 
	list <int> :: iterator i; 
	for (i = table[index].begin(); i != table[index].end(); i++) { 
		if (*i == key) break; 
	} 

  	// if key is found in hash table, remove it 
	if (i != table[index].end()) 
		table[index].erase(i); 
} 

void Hash::searchItem(int key) 
{ 
	// get the hash index of key 
	int index = hashFunction(key); 

	// find the key in (inex)th list 
	list <int> :: iterator i; 
	for (i = table[index].begin(); i != table[index].end(); i++) { 
		if (*i == key) break; 
	} 

  	// if key is found in hash table: 
	if (i != table[index].end()){
		cout << "Item: " << key << " found at: " << index <<  endl;
	}
	else{
		cout << "Item not found" << endl;
	}
} 
  
```


* Useful visualization tool can be found in [here](https://visualgo.net/en/hashtable)

## `std::map` vs `std::unordered_map`

* The underlying structure of an std::map is implemented with a balanced tree structure.
    * Useful if you care about the ordering of keys.
* `std::unordered_map` is used similarly to std::map, but the `std::unordered_map` is implemented with hash tables.
    * Notice the `std::unsorted_map`'s key / value pairs are not printed in sorted order by keys, but `std::map`'s keys are.
    * Hash Tables have a better average case performance (O(1)), but data order is not guaranteed when traversing the structure with iterators.

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-88nc{font-weight:bold;border-color:inherit;text-align:center}
.tg .tg-pq3e{font-style:italic;border-color:inherit;text-align:left}
.tg .tg-kiyi{font-weight:bold;border-color:inherit;text-align:left}
.tg .tg-uys7{border-color:inherit;text-align:center}
.tg .tg-xldj{border-color:inherit;text-align:left}
</style>
<table class="tg">
  <tr>
    <th class="tg-xldj"></th>
    <th class="tg-88nc" colspan="2">unordered_map</th>
    <th class="tg-88nc" colspan="2">map</th>
  </tr>
  <tr>
    <td class="tg-xldj"></td>
    <td class="tg-pq3e">Average</td>
    <td class="tg-pq3e">Worst-Case</td>
    <td class="tg-pq3e">Average</td>
    <td class="tg-pq3e">Worst-Case</td>
  </tr>
  <tr>
    <td class="tg-kiyi">Lookup</td>
    <td class="tg-uys7">O(1)</td>
    <td class="tg-uys7">O(n)</td>
    <td class="tg-uys7">O(log n)</td>
    <td class="tg-uys7">O(log n)</td>
  </tr>
  <tr>
    <td class="tg-kiyi">Deletion</td>
    <td class="tg-uys7">O(1)</td>
    <td class="tg-uys7">O(n)</td>
    <td class="tg-uys7">O(log n)</td>
    <td class="tg-uys7">O(log n)</td>
  </tr>
</table>
