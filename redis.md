# Redis

## What is Redis

- It's an open-source, in-memory, NoSQL database "key-value" typed that is used as a database, caching or message broker system.

## Why Redis

- Super fast database.
- Used to decrease the load or requests on the database "Temporary Caching System".
- Supported by most of the languages. For example, "predis/predis" package for php.

## Using Redis

### Single Values

- ```SET <key> <value>``` sets this value to that key.
- ```INCR <key> [value = 1]``` increaments that key be the value specified "default = 1" and creates it first if it doesn't exist.
- ```GET <key>``` returns the value of the key specified.
- ```EXISTS <key>``` checks the key if it exists or not.
- ```DEL <key>``` deletes the key specified.
- ```KEYS [pattern]``` gets all the keys stored at the memory that matches the pattern.
- ```FLUSHALL``` removes all the keys from the memory.

### Sorted Sets

- Sorted Sets are arrays that contains only unique values and they are automatically sorted with a specific score.
- ```ZADD <set-key> <base-score> <member>``` adds a member to a sorted set.
- ```ZINCRBY <set-key> <added-score> <member>``` increaments the score of a member in a specific set.
- ```ZRANGE <set-key> <start> <stop>``` lists the items **Ascendingly** from the start to the stop indecies "-1 indicates the last element".
- ```ZREVRANGE <set-key> <start> <stop>``` lists the items **Descendingly** from the start to the stop indecies "-1 indicates the last element".

### Hashes

- Hash is a way to implement an associative array. It is an array that has key value pairs.
- ```HSET <key> <field> <value>``` adds a new hash that has only one pair. 
- ```HMSET <key> <field> <value> [<another-field> <another-value>]``` adds a new hash that has multiple pairs. 
- ```HGET <key> <field>``` gets the value of a member within a hash. 
- ```HGETALL <key>``` gets all the members and their values within a hash. 
- ```HINCRBY <key> <field> <increament>``` increaments a field within a hash by the increament value. 

## Tips && Tricks

- You can add namespaced keys to specify a separate uses. For example, "articles.1.views" and "videos.2.downloads".
- You can simply store a whole json-casted database record "model instance" in a key within redis.
- You can use Redis for caching by checking a key and if it exists, return the value of the key but if it doesn't exist then perform a query and store the result within the key to fetch it later.