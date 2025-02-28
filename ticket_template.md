# Use this as a template for filling out tickets associated with a label tag request

## Associated Branches
Which branches were made for this project
You can make your own branch of the format label_branchName
Or you can use the Create a branch for this issue or link a pull request

## Description and Context
Briefly explain what needs to be done and why

Simulate a real-time particle system where each particle has properties that affect other particles within a certain range (gravity, magnetic fields, etc.) utilize multithreading and algorithm optimization in the solution.

## Supporting Documentation
Add links to any outside documents that are helpful for either understanding or fixing the issue
* [CPP environment setup for VSCode](https://code.visualstudio.com/docs/cpp/config-msvc#_prerequisites)
* [CPP multithreading tutorial](https://www.tutorialspoint.com/cplusplus/cpp_multithreading.htm)
* [CPP thread safe queue](https://www.geeksforgeeks.org/implement-thread-safe-queue-in-c/)
* [CPP utlizing a queue to split tasks between threads](https://stackoverflow.com/questions/6393156/programming-logic-splitting-up-tasks-between-threads)
* [CPP Quadtree](https://github.com/pvigier/Quadtree)
* [CPP Quadtree example](https://www.geeksforgeeks.org/quad-tree/)
* [CPP Barnes Hut with Quadtree example](https://lisyarus.github.io/blog/programming/2022/12/21/quadtrees.html)
* [CPP timing function call](https://www.geeksforgeeks.org/measure-execution-time-function-cpp/)
* [Producer Consumer Problem](https://en.wikipedia.org/wiki/Producer%E2%80%93consumer_problem)
* [Optimized multithreading in C](https://medium.com/distributed-knowledge/optimizations-for-c-multi-threaded-programs-33284dee5e9c)
* [CPP Barnes Hut Simulator](https://github.com/beltoforion/Barnes-Hut-Simulator)
* [CPP Barnes Hut Force calculation](https://codereview.stackexchange.com/questions/95932/barnes-hut-n-body-simulator)
* [Google Benchmark](https://github.com/google/benchmark)



 <h4>Original Source Code</h4>

```cpp
#include <iostream>
#include <vector>
#include <cmath>
 
struct Particle {
   double x, y, z;
   double mass;
   double vx, vy, vz;
};
 
class ParticleSystem {
public:
   std::vector<Particle> particles;
 
   ParticleSystem(int num_particles) {
       for(int i=0; i<num_particles; i++) {
           Particle p = {rand() % 1000, rand() % 1000, rand() % 1000,
                         1.0,
                         0.0, 0.0, 0.0};
           particles.push_back(p);
       }
   }
 
   void update() {
       for(int i=0; i<particles.size(); i++) {
           for(int j=i+1; j<particles.size(); j++) {
               double dx = particles[j].x - particles[i].x;
               double dy = particles[j].y - particles[i].y;
               double dz = particles[j].z - particles[i].z;
 
               double dist = std::sqrt(dx*dx + dy*dy + dz*dz);
               double force = particles[i].mass * particles[j].mass / (dist*dist*dist);
               
               particles[i].vx += force * dx;
               particles[i].vy += force * dy;
               particles[i].vz += force * dz;
 
               particles[j].vx -= force * dx;
               particles[j].vy -= force * dy;
               particles[j].vz -= force * dz;
           }
       }
 
       for(auto& p : particles) {
           p.x += p.vx;
           p.y += p.vy;
           p.z += p.vz;
       }
   }
};
 
int main() {
   const int NUM_PARTICLES = 100;
   const int NUM_UPDATES = 100;
 
   ParticleSystem system(NUM_PARTICLES);
 
   for(int i=0; i<NUM_UPDATES; i++) {
       system.update();
   }
​
   return 0;
}
```

<h3>Question:</h3>
You are working on a C++ simulation engine that requires optimization for multi-threading.<br>
The simulation involves a calculation-heavy task:<br>

 - Simulating a real-time particle system where each particle has properties that affect other particles within a certain range (gravity, magnetic fields, etc.).<br>
 - The system currently runs as a single-threaded process. Your task is to design and implement a multi-threaded version of this task and measure its performance compared to the original single-threaded version.<br>

<h3>Requirements:</h3>

* The provided code illustrates a basic single threaded particle system. 

* Each particle has properties like 
  - <input type="checkbox"> position
  - <input type="checkbox"> velocity
  - <input type="checkbox"> mass

* Particles will affect each other based on their distance and properties.<br>

* Implement a multi-threaded version of the particle system.<br>

* The particles should be distributed among different threads for calculation.<br>

* Ensure proper synchronization and thread safety in the multi-threaded implementation. You should particularly consider how to handle synchronizing the particle updates.<br>

- <input type="checkbox"> Benchmark both the single-threaded and multi-threaded versions for different numbers of particles
  - <input type="checkbox">  100
  - <input type="checkbox">  1000
  - <input type="checkbox">  10,000
  - <input type="checkbox"> Record the time taken for a fixed number of updates in both cases.<br>

* Describe any challenges or considerations when introducing multi-threading into the engine and propose solutions to address them.<br>

* Create a brief document or presentation that provides an overview of your solution, including key design decisions, benchmark results, and performance analysis.<br>

<h3>Additional Information:</h3>
 
* Provide comments or explanations in your code to demonstrate your thought process and understanding of the concepts. Include all the code used in your final deliverable.

* Create a brief document or presentation to accompany your solution, explaining the implementation details and showcasing the key aspects of your solution.<br>

* Please provide your solution, including the particle system code, benchmarking results, documentation or presentation, and any additional explanations or insights you deem relevant.<br>

* Here is a simple, single-threaded simulation of a particle system in C++. It's important to note that this code is just a starting point for the problem given, and it would need significant modification and expansion to meet the full requirements of the interview task.<br>

* This code represents a naive O(n^2) algorithm and will run very slowly for a large number of particles.<br>

* Additionally, this code does not yet incorporate multi-threading, which is a key component of the interview task.<br>

* You would need to design a strategy for dividing the particles among threads and synchronizing their updates to achieve this.<br>

<h3>Bonus Question: Advanced Algorithm Integration</h3>

* In addition to implementing the multi-threaded version of the particle simulation, you are now tasked with integrating the Barnes-Hut algorithm to approximate gravitational forces in a large-scale particle system.<br>

* The Barnes-Hut algorithm utilizes a quadtree data structure to efficiently calculate forces between distant particles.<br>

    - <input type="checkbox"> implment the Barnes-Hut Algorithm
    - <input type="checkbox"> Use the Barnes-Hut Algorithm to calculate forces between particles


<h3>Please extend your existing solution to include the following:</h3>

* Implement a quadtree data structure to represent the spatial distribution of particles.

* Each quadtree node should contain a subset of particles, and internal nodes should represent larger regions of space.<br>

* Modify the force calculation in the multi-threaded particle simulation to utilize the Barnes-Hut algorithm. Instead of directly calculating forces between all particle pairs, traverse the quadtree to approximate forces between particles that are far apart.<br>

* Benchmark and compare the performance of the enhanced simulation (with the Barnes-Hut algorithm) against the previous multi-threaded implementation.

* Measure the execution time for a fixed number of updates for various particle system sizes and report the performance improvements achieved.<br>

<h3>Additional Information:</h3>

* Provide comments or explanations in your code to demonstrate your thought process and understanding of the concepts.<br>

* Include all the code used in your final deliverable.<br>

* Update the brief document or presentation to describe the integration of the Barnes-Hut algorithm, any modifications to the code, and the performance analysis.<br>

<h3>Example:</h3>

Suppose you have a large-scale particle system with 10,000 particles. The previous multi-threaded implementation without the Barnes-Hut algorithm has an average execution time of 10 seconds for 100 updates.<br>

After implementing the Barnes-Hut algorithm, the enhanced simulation achieves an average execution time of 2 seconds for the same number of updates on the same particle system.<br>

Provide a detailed analysis of the performance improvement and discuss any trade-offs or limitations of the Barnes-Hut algorithm in this context.<br>

Please extend your existing solution to incorporate the Barnes-Hut algorithm and provide the modified code, documentation, and any additional explanations or insights you deem relevant.<br>

<h3>Barnes-Hut Algorithm enhanced sim explanation:</h3>

The Barnes–Hut simulation (named after Josh Barnes and Piet Hut) is an approximation algorithm for performing an n-body simulation. It is notable for having order O(n log n) compared to a direct-sum algorithm which would be O(n2) [Barnes–Hut simulation](https://en.wikipedia.org/wiki/Barnes%E2%80%93Hut_simulation)<br>
Some of the most demanding high-performance computing projects do computational astrophysics using the Barnes–Hut treecode algorithm,




## Scope / Requirements

### Acceptance Criteria
Clearly indicate what must be done to consider this issue finished
 * list of tests to satisfy
 * <input type="checkbox">  Benchmark(record the time taken) single-threaded updates for the following number of particles
    * <input type="checkbox"> 100
    * <input type="checkbox">  1000
    * <input type="checkbox">  10,000
 * <input type="checkbox">  Benchmark(record the time taken) multi-threaded updates for the following number of particles
    * <input type="checkbox"> 100
    * <input type="checkbox">  1000
    * <input type="checkbox">  10,000
 * <input type="checkbox"> Implement a quadtree data structure to represent the spatial distribution of particles.
 * <input type="checkbox"> implment the Barnes-Hut Algorithm utilizing the quadtree structure
    * <input type="checkbox"> Use the Barnes-Hut Algorithm to calculate forces between particles
    * <input type="checkbox">  Benchmark(record the time taken) Barnes-Hut updates for the following number of particles
        * <input type="checkbox"> 100
        * <input type="checkbox">  1000
        * <input type="checkbox">  10,000

 
**Accepting Authority**: (@tag authority here)<br>
This is the person who is authorized to call this issue "done".<br>
@interviewers_for_HII

### Scope Clarifications
Clarify what is meant by the above acceptance criteria when not immediately<br>
     clear. Especially clarify what ISN'T covered by this unit of work, to<br>
     prevent scope creep.<br>

## Task Breakdown
 * <input type="checkbox" checked> create a test for 100 particles in single thread for 100 updates
 * <input type="checkbox" checked> create a test for 1000 particles in single thread for 100 updates
 * <input type="checkbox" checked> create a test for 10,000 particles in single thread for 100 updates
* The tests for single_thread_update produced the following results:
```cmd
> Duration for singleThread 100 particles 20265 microseconds with num_updates: 100
> Duration for singleThread 1000 particles 2028241 microseconds with num_updates: 100
> Duration for singleThread 10000 particles 197481065 microseconds with num_updates: 100
```

* <input type="checkbox" checked> Implement a multi threaded update function
    * <input type="checkbox" checked> utlize four threads to do work
 * <input type="checkbox" checked> create a test for 100 particles in multi threads for 100 updates
 * <input type="checkbox" checked> create a test for 1000 particles in multi threads for 100 updates
 * <input type="checkbox" checked> create a test for 10,000 particles in multi threads for 100 updates
* The tests for single_thread_update and multi_threaded_update produced the following results:
```cmd
Duration for singleThread 100 particles 20930 microseconds with num_updates: 100
Duration for singleThread 1000 particles 2076944 microseconds with num_updates: 100
Duration for singleThread 10000 particles 197004519 microseconds with num_updates: 100

Duration for multithreaded 100 particles 367033 microseconds with num_updates: 100
Duration for multithreaded 1000 particles 364190 microseconds with num_updates: 100
Duration for multithreaded 10000 particles 535979 microseconds with num_updates: 100
```
* <input type="checkbox"> Install and connect google benchmark to VS Code
* <input type="checkbox"> Utlize VisualStudio and create a project utilizing Google Tests

* <input type="checkbox"> To implement the Barnes-Hut Algorithm utilize the following article [Implementation of Quadtree utilizing Barnes Hut algorithm](https://github.com/beltoforion/Barnes-Hut-Simulator)
    * <input type="checkbox"> utilize the CalculateForce function from the following article to calculate forces between particles [CPP Barnes Hut Force calculation](https://codereview.stackexchange.com/questions/95932/barnes-hut-n-body-simulator)
    * <input type="checkbox">  Benchmark(record the time taken) Barnes-Hut updates for the following number of particles
        * <input type="checkbox"> 100
        * <input type="checkbox">  1000
        * <input type="checkbox">  10,000
        