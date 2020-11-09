# Parallel strategy

In this test we will analyse different strategies of parallel applications.

With a machine that contains 2 sockets each one has 10 cores and with hyperthreading it will make it 20.
So the total of our logical units is 40 cores.
The topology of the machine is as below in the figure[2]

![topology](https://github.com/chakib-belgaid/parallel_strategy/blob/master/figures/topology.png)

## Running strategies

We run a program that is composed of 10 threads (number of physical units in each socket) and we measured the energy consumption of the same program with 3 different strategies

### 1-Choose only physical units of one socket

So according to the topology abouve we chose to pin our program on the following cores : 0,2,4,6,8,10,12,14,16 and 18.
We call this strategy **physical cpu**

### 2-One socket with both pysical cpu and its hyper threads

And we will pin our progam on the following cores : 0,4,8,12,16,20,24,28,32,36

### 3- splits the threads between 2 sockets

Unlike the two first strategies when the 2nd socket is resting, in this strategy we use 1/4 of both sockets using only physical cores.
And so we pinned the programm on the following cores : 0,1,2,3,4,5,6,7,8,9

### Experimental process

To test those strategies, we run the same programm multiple times (**10** to be precise)in our case we executed the programm with different woarkload from 0% to 100% when each time x% means how much we use the unit that we are executing on it.
![htop](https://github.com/chakib-belgaid/parallel_strategy/blob/master/figures/htop.png)

The figure abouve shows an example of the program when he is using 75% of the cpu [each thread use 75%]

## Resutls

The following graph shows the energy consumption of the diffrent Strategies for multiple levels of workload

![plot](https://github.com/chakib-belgaid/parallel_strategy/blob/master/figures/plot.png)

## Conclusion

As we can see **the second stratgy** won when it comes to the energy consumption.

However if we are looking for reproduction of the tests than we will try to reduce the variation between each run and for this we have two candidates

- When we are in 100% of workload **the 1st strategy** win
- When we are betwwen 50% and 90% **the 3dr startetgy** win
- under 50% the **the 1st strategy** win again
  we can see this in the figure below

  ![plot](https://github.com/chakib-belgaid/parallel_strategy/blob/master/figures/parallel_strategies_std.png)

## Futher work

- Check what is the default policy
