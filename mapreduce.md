###Map Reduce

* **Mappers**  
--each deals with small amount of data and work in parellell

 Break the whole into chunks and give each chunk to one of the mappers. So all the mappers can work at the same time, each over a small fraction of the data.
 For each mapper, it will take the first record on an index card, take the next record, and repeat. They pile the index cards up, the cards for the same "key" go in the same pile.
 
 ** The output of the Mappers is called intermediate records. Intermediate records are [key, value] pair.**
 
 Once the Mappers have finished, a phase of Map Reduce called the **shuffle and Sort** take place. This is the phase between mapper and reducer.
 
 Shuffle is the movement from mappers to reducers, sort is the reducers will organize these sets of records into sorted order.
 
* **Reducers**

 Once the mappers have finished, the reducer can collect their sets of cards. Each reducer is responsible for some "Key". The reducers go to the mappers and retrieve the pile of cards for their "key" which they are responsible for. Reducers collect small piles and create a large pile. They go through the piles one at a time, add up all the amounts from all the cards in the pile.
 
 ** The output of the reducers is key and a list of values. It processes those values in some way, like add up values.**
 
 There is no guarantee that each reducer will get the same number of keys.
 **Single Reducer is the Hadoop default.**
 
**Daemons of MapReduce**

When you run MapReduce job, you submit the job to Job Tracker. The Job Tracker splits the work into mappers and reducers. Those mappers and reducers will run on other cluster nodes.

A daemon called TaskTracker runs the actual Map Reduce tasks in each node. TaskTracker runs on the same machine as DataNode to save network traffic. If the TaskTracker is already busy, a different node will be chosen to process it, and it will be streamed over the network. The mappers read their input data and produce intermediate data which the Hadoop framework will pass to the reducers. The reducers process that data and write their final output back to HDFS.

Hadoop streaming allows you to write your code in any language.

### Running Map Reduce 

1. the root location has the mapper.py and reducer.py
2. run the Map Reduce command


```
hadoop jar path-to-jar -mapper mapper.py -reducer reducer.py 
-file mapper.py -file reducer.py -input myinput -output joboutput
```
The joboutput directory contains 3 things.
* _SUCCESS
* _logs
* part-00000
part-00000 is the output from one reducer that we had for this job.

When you're developing map reduce job, first test locally with a small data set before you run the entire huge data set.  

Mapper Code


```
# Your task is to make sure that this mapper code does not fail on corrupt data lines,
# but instead just ignores them and continues working
import sys

def mapper():
    # read standard input line by line
    for line in sys.stdin:
        # strip off extra whitespace, split on tab and put the data in an array
        data = line.strip().split("\t")

        # This is the place you need to do some defensive programming
        # what if there are not exactly 6 fields in that line?
        # YOUR CODE HERE
                # YOUR CODE HERE
        if len(data) != 6:
            print('Invalid Input! Skip this line to continue')
            continue
        # this next line is called 'multiple assignment' in Python
        # this is not really necessary, we could access the data
        # with data[2] and data[5], but we do this for conveniency
        # and to make the code easier to read
        date, time, store, item, cost, payment = data
        
        # Now print out the data that will be passed to the reducer
        print "{0}\t{1}".format(store, cost)
        
test_text = """2013-10-09\t13:22\tMiami\tBoots\t99.95\tVisa
2013-10-09\t13:22\tNew York\tDVD\t9.50\tMasterCard
2013-10-09 13:22:59 I/O Error
^d8x28orz28zoijzu1z1zp1OHH3du3ixwcz114<f
1\t2\t3"""

# This function allows you to test the mapper with the provided test string
def main():
	import StringIO
	sys.stdin = StringIO.StringIO(test_text)
	mapper()
	sys.stdin = sys.__stdin__
```

