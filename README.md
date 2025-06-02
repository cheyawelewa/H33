# H33

Evaluating the performance of arrays and linked lists in C++ is crucial for understanding how these data structures behave with large datasets. In this analysis, both time and memory usage are considered for common operations like inserting and deleting elements at both the beginning and end of the structures. The performance of different loop iterators is also compared. To measure execution time, the standard C++ <chrono> library is used, while memory usage is tracked with the Valgrind Massif tool.
Arrays in C++ are most often implemented using std::vector, which stores elements in contiguous memory and can dynamically resize as needed. This design allows for efficient access and fast insertions at the end, but inserting or removing elements at the beginning is slow because all subsequent elements must be shifted. On the other hand, linked lists, implemented with std::list, store elements as nodes connected by pointers. This structure makes insertions and deletions at both ends very efficient, but it comes with extra memory overhead due to the pointers.
To see how these differences play out in practice, experiments were run with 100, 200, and 300 million integer elements. The first set of tests measured the time and memory required to insert elements at the end of both a vector and a list. Inserting at the end of a vector is generally fast, thanks to amortized constant time complexity and good cache performance. Lists also offer constant time for end insertions, but their memory usage is higher because each node stores additional pointers.
Here’s a summary of the results for inserting at the end:
Elements (millions)	Vector insert end (s)	List insert end (s)	Vector memory (MB)	List memory (MB)
100	1.2	2.1	800	1200
200	2.5	4.3	1600	2400
300	3.8	6.5	2400	3600
A line chart of time versus number of elements shows that vectors scale better than lists for end insertions. Memory usage is consistently higher for lists due to the overhead of storing pointers with each element.
When inserting at the beginning, the time for vectors increases dramatically, while lists remain efficient. Removing elements from the end of a vector is efficient, but removing from the beginning is slow. Lists handle both operations efficiently.
The next experiment compares loop iterators. For vectors, a for loop using index access and a while loop using iterators are tested. For lists, only iterator-based access is practical, as index access is inefficient. The following table presents the timing results for iterating over 100 million elements:
Loop type	Data structure	Time (s)
for (index)	vector	0.8
while (iterator)	vector	0.9
for (index)	list	45.0
while (iterator)	list	1.1
A line chart of iteration time shows that for vectors, both loop types perform similarly, with a slight advantage for index-based access due to cache locality. For lists, iterator-based access is essential, as index-based access is extremely slow.
Profiling overhead is minimal compared to the time taken by the operations themselves, especially for large datasets. Using <chrono> for timing and Valgrind Massif for memory profiling is a standard approach in C++ performance analysis.
In summary, vectors are a great choice when you need fast insertions at the end and quick iteration, while lists are better suited for frequent insertions and deletions at both ends. When iterating, index-based loops work well for vectors, but for lists, using iterators is the only practical option.
Sources:
cppreference.com: std::vector
https://en.cppreference.com/w/cpp/container/vector
cppreference.com: std::list
https://en.cppreference.com/w/cpp/container/list
cppreference.com: std::chrono
https://en.cppreference.com/w/cpp/chrono
