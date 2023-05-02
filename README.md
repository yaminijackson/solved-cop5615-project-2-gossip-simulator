Download Link: https://assignmentchef.com/product/solved-cop5615-project-2-gossip-simulator
<br>
<h1>1   Problem definition</h1>




As described in class Gossip type algorithms can be used both for group communication and for aggregate computation. The goal of this project is to determine the convergence of such algorithms through a simulator based on actors written in Elixir. Since actors in Elixir are fully asynchronous, the particular type of Gossip implemented is the so-called Asynchronous Gossip.




<strong>Gossip Algorithm for information propagation</strong>: The Gossip algorithm involves the following:




<ul>

 <li><strong>Starting</strong>: A participant(actor) it told/sent a rumor(fact) by the main process</li>

 <li><strong>Step</strong>: Each actor selects a random neighbor and tells it the rumor</li>

 <li><strong>Termination</strong>: Each actor keeps track of rumors and how many times it has heard the rumor. It stops transmitting once it has heard the rumor 10 times (10 is arbitrary, you can play with other numbers or other stopping criteria).</li>

</ul>




<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong>Push-Sum algorithm for sum computation: </strong>

<strong> </strong>

<ul>

 <li><strong>State: </strong>Each actor A<sub>i</sub> maintains two quantities: s and w. Initially, s = x<sub>i</sub> = i (that is actor number i has value i, play with other distribution if you so desire) and w = 1.</li>

 <li><strong>Starting</strong>: Ask one of the actors to start from the main process.</li>

 <li><strong>Receive: </strong>Messages sent and received are pairs of the form (s, w). Upon receive, an actor should add received pair to its own corresponding values. Upon receive, each actor selects a random neighbor and sends it a message.</li>

 <li><strong>Send: </strong>When sending a message to another actor, half of s and w is kept by the sending actor and half is placed in the message.</li>

 <li><strong>Sum estimate: </strong>At any given moment of time, the sum estimate is s/w where s and w are the current values of an actor.</li>

 <li><strong>Termination: </strong>If an actor ratio s/w did not change more than 10<sup>-10</sup> in 3 consecutive rounds the actor terminates. WARNING: the values s and w independently never converge, only the ratio does.</li>

</ul>




<strong>Topologies:</strong> The actual network topology plays a critical role in the dissemination speed of Gossip protocols. As part of this project you have to experiment with various topologies. The topology determines who is considered a neighbor in the above algorithms.




<ul>

 <li><strong>Full Network:</strong> Every actor is a neighbor of all other actors. That is, every actor can talk directly to any other actor.</li>

 <li><strong>Line:</strong> Actors are arranged in a line. Each actor has only 2 neighbors (one left and one right, unless you are the first or last actor).</li>

 <li><strong>Random 2D Grid:</strong> Actors are randomly position at x, y coordinates on a [01.0] x [0-1.0] square. Two actors are connected if they are within .1 distance to other actors.</li>

 <li><strong>3D torus Grid:</strong> Actors form a 3D grid. The actors can only talk to the grid neighbors. And, the actors on outer surface are connected to other actors on opposite side, such that degree of each actor is 6.</li>

</ul>




<ul>

 <li><strong>Honeycomb:</strong> Actors are arranged in form of hexagons. Two actors are connected if they are connected to each other. Each actor has maximum degree 3.</li>

</ul>







<ul>

 <li><strong>Honeycomb with a random neighbor:</strong> Actors are arranged in form of hexagons (Similar to Honeycomb). The only difference is that every node has one extra connection to a random node in the entire network.</li>

</ul>




<h1>2   Requirements</h1>




<strong>Input:</strong>  The input provided (as command line to your program will be of the form:




<em>my_program numNodes topology algorithm </em>




Where numNodes is the number of actors involved (for 3D based topologies you can round up until you get a cube, similarly for 2D until you get a square), topology is one of full, line, rand2D, 3Dtorus, honeycomb and randhoneycomb, algorithm is one of gossip, push-sum.




<strong>Output:</strong> Print the amount of time it took to achieve convergence of the algorithm. Please described how you measured the time in your report.




<strong>Actor modeling:</strong> In this project you have to use exclusively the actor facility (GenServer) in Elixir (projects that do not use multiple actors or use any other form of parallelism will receive no credit).













README File: In the README file you have to include the following material:

<ul>

 <li>Team members</li>

 <li>What is working</li>

 <li>What is the largest network you managed to deal with for each type of topology and algorithm</li>

</ul>




Report.pdf: For each type of topology and algorithm, draw the dependency of convergence time as a function of the size of the network. You can overlap different topologies on the same graph, i.e. you can draw 4 curves, one for each topology and produce only 2 graphs for the two algorithms. Write about any interesting finding of your experiments in the report as well and mention the team members. You can produce Report.pdf in any way you like, for example using spreadsheet software. You might have to use logarithmic scales to have a meaningful plot.




<h1>3   BONUS</h1>




In the above assignment, there is no failure at all. For a 20% bonus, implement node and failure models (a node dies, a connection dies temporarily or permanently). Write a Report-bonus.pdf to explain your findings (how you tested, what experiments you performed, what you observed) and submit project2-bonus.zip with your code. To get the bonus you must implement at least one failure model controlled by a parameter and draw plots that involve the parameter. At least one interesting observation has to be made based on these plots.