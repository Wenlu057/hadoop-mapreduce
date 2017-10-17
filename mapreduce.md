###Map Reduce

* **Mappers** 

 Break the whole into chunks and give each chunk to one of the mappers. So all the mappers can work at the same time, each over a small fraction of the data.
 For each mapper, it will take the first record on an index card, take the next record, and repeat. They pile the index cards up, the cards for the same "key" go in the same pile.
* **Reducers**

 Once the mappers have finished, the reducer can collect their sets of cards. Each reducer is responsible for some "Key". The reducers go to the mappers and retrieve the pile of cards for their "key" which they are responsible for. Reducers collect small piles and create a large pile. They go through the piles one at a time, add up all the amounts from all the cards in the pile.