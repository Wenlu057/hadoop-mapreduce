###Map Reduce

* **Mappers**  
--each deals with small amount of data and work in parellell

 Break the whole into chunks and give each chunk to one of the mappers. So all the mappers can work at the same time, each over a small fraction of the data.
 For each mapper, it will take the first record on an index card, take the next record, and repeat. They pile the index cards up, the cards for the same "key" go in the same pile.
 
 ** The output of the Mappers is called intermediate records. Intermediate records are [key, value] pair.**
 
 Once the Mappers have finished, a phase of Map Reduce called the **shuffle and Sort** take place.
 
 Shuffle is the movement from mappers to reducers, sort is the reducers will organize these sets of records into sorted order.
 
* **Reducers**

 Once the mappers have finished, the reducer can collect their sets of cards. Each reducer is responsible for some "Key". The reducers go to the mappers and retrieve the pile of cards for their "key" which they are responsible for. Reducers collect small piles and create a large pile. They go through the piles one at a time, add up all the amounts from all the cards in the pile.
 
 ** The output of the reducers is key and a list of values. It processes those values in some way, like add up values.**
 
 There is no guarantee that each reducer will get the same number of keys.