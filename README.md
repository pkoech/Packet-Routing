# Distance Vector Routinng (packet routing)

**Problem Statement**

The goal of this project is for to implement distributed routing algorithms, where all routers run an algorithm that allows
them to transport packets to their destination, but no central authority determines the forwarding paths. The code run at a 
router, and a routing simulator that builds a graph connecting routers to each other and to simulate hosts on the network is included. In this project (**Bellman Ford algorithm**)a version of a distance vector protocol that computes efficient paths across the network is implemented.

**Simulation Environment**

You will be developing your router in Python 2.7 under a simulation environment provided by us. The simulation environment, as well as your router implementation, lives under the  `simulation` directory; you should cd into this directory before entering any terminal commands provided in this document.

In the simulation environment, every type of network device (e.g., a host or your router) is modeled by a subclass of the Router class. Each Router has a number of ports, each of which may be connected to a neighboring entity (e.g., a host or another router). 
Each link connecting two entities has a latency—think of it as the link’s propagation delay. Your `Router` sends and receives Packet’s to and from its neighbors. Both the Router and Packet classes are defined in the sim.basics module

Before we begin, let’s make sure that your Python version is supported. 
Type in your terminal:
`$ python --version`
You should be good to go if the printed version has the form `Python 2.7.*.`

To get you started, we have provided an implementation of a hub—a network device that floods any packet it receives to all of its ports (other than the port that the packet came from). The hub is already implemented and you don’t need to submit anything for this section.

Take a look at the hub implementation in examples/hub.py. Having no need to record any routes, the hub only implements the handle_data_packet method to flood data packets.
Let’s try out the hub on a linear topology with three hosts:

`$ python simulator.py --start --default-switch-type=examples.hub topos.linear --n=3`
You can now access the **visualizer** at http://127.0.0.1:4444 using your browser; you should see the hosts and routers displayed against a purple background. Let’s now make host h1 send a ping packet to host h3. You can either type into the 

Python terminal:
`>>> h1.ping(h3)`

or you can send the ping from the visualizer by: (1) selecting h1 and pressing A on the keyboard; 
selecting h3 and pressing B ; and (3) pressing P to send a ping from host A to host B .

You should see the “ping” and “pong” packets being delivered between h1 and h3. You should also see both packets delivered to h2 despite it not being the recipient. This behavior is expected since the hub simply floods packets everywhere. You may also observe what’s going on from the log messages printed to the Python terminal.

Flooding packets is problematic when the network has loops. Let see this in action by launching the simulator with the topos.candy topology, which has a loop.

``$ python simulator.py --start --default-switch-type=examples.hub topos.candy``

**Testing**
To help you check your work, we provide you with unit and comprehensive tests. 
  `$ python dv_unit_tests.py 5`
For comprehensive tests run 
`$ python simulator.py --default-switch-type=dv_router \ --default-host-type=dv_comprehensive_test.TestHost \ topos.rand --switches=5 --links=10 --seed=1 \ dv_comprehensive_test --seed=43`
  `>>> start()`
This command will launch the simulator on a pseudorandomly generated topology with 5 switches and 10 links. The comprehensive test will start running after you enter start() into the Python terminal. As usual, you may observe the test progress in the visualizer.

The comprehensive test will run indefinitely until a test failure occurs. If that happens, you can type commands into the Python terminal and use the visualizer to debug.

