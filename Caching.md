# Caching
= storing reusable responses in order to make subsequent requests faster
- basically a large hash table with keys and values

#### When do we cache?
- When computation is slow
- When computation will run multiple times
- When the output is same for a particular input
- When your hosting provider charges for db access

![[Cache hit.png]]
<br>

#### Handling stale data
	- write operations require keeping the cache and your database in sync
	- data "eviction" or turnover and refreshes of data nneeded to keep cached data fresh and up-to-date. To do so, you can use techniques like LIFO, FIFO, LRU, and LFU.
- Generally, caching works best when used to store static or infrequently changing data, and when the sources of change are likely to be single operations rather than user-generated operations
- Where consistency and freshness in data is critical, caching may not be an optimal solution, unless there is another element in the system that efficiently refreshes the caches at intervals that do not adversely impact the purpose and user experience of the application.
<hr>
## Memcached
key - value store

Main operations
- set (key, value)
- get (key) -> value
- delete (key)

src: https://www.youtube.com/watch?v=7MLXuG83Fsw&t=145s
- to set up:
	```
	brew install memcache
	brew install telnet
	telnet localhost 11211
	```

- set a key-value pair (foo: bar) with params: 0 flags, 3600 sec expiration time, 3 byes
	```
	set foo 0 3600 3
	bar
	```

- to delete:
	```
	delete foo
	```

- 'set' command will replace, 'add' won't.
	```
	add num 0 3600 2
	50
	```

- append:
	```
	append num 0 3600 2
	25
	```
--> get num will now return 5025.
- prepend
- replace
	```
	replace num 0 3600 2
	40
	```
- increment (incr) / decrement (decr)
	```
	incr num 2
	```
--> 42
- ```flush_all``` gets rid of everything

```quit``` out of telnet and ```brew services restart memcached``` will restart everything

