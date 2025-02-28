# Github Ticket Template
This template is meant to serve as a structured way to track progress on the parking garage simulation project, helping developers stay organized and ensuring that no aspect of the problem is overlooked.


### Key Concepts:
The `ticket_template.md` serves as a guide to help break down the work required for developing this solution. The tasks outlined are as follows:

- **Branch Management:** Create branches to organize work for different features and tasks, such as bug fixes or new functionalities.
  
- **Description & Context:** Provide a brief description of the task, its goals, and its importance. In this case, implementing a system for parking spot optimization near an elevator.

- **Supporting Documentation:** Include helpful links, such as C++ tutorials, multithreading resources, or algorithms related to the parking simulation, so the developer can learn more about the tools needed.

- **Source Code and Sample Questions:** The ticket includes the original code of a basic producer-consumer scenario to be extended for the parking garage problem. Developers are also tasked with implementing the parking garage simulation, ensuring thread safety, and optimizing the search for the best parking spot using algorithms like BFS or Dijkstra’s.

- **Acceptance Criteria:** The ticket clearly defines what needs to be done for completion, including implementing algorithms, benchmarking performance, and testing edge cases.

### Tasks and Guidelines
---

1. **Producer-Consumer Problem:** The provided template uses a queue shared between two threads (producer and consumer). The producer generates parking events (e.g., cars arriving), and the consumer processes these events, finding optimal parking spots.
  
2. **Multi-Level Garage Simulation:** The parking garage is represented as a 2D grid, where each cell represents a parking spot. The task is to implement an efficient algorithm to find the closest available parking spot to the elevator, ensuring thread safety and concurrency handling.

3. **Advanced Algorithm Application:** This template involves using Dijkstra's Algorithm for pathfinding, taking obstacles and spot availability into account. Additionally, other optimizations such as multi-threading and performance benchmarking are key parts of the solution.

---



### Additional Information:
- **Benchmarking:** Developers are asked to benchmark both single-threaded and multi-threaded implementations for performance using different grid sizes (e.g., 10, 100, 1000 parking spots).
  
- **Edge Cases:** Handling full garages, multiple car arrivals, and scenarios where the elevator is blocked are part of the problem-solving process.

- **Optional Enhancements:** Future work may include integrating dynamic updates of parking spots, adding a graphical user interface, or implementing multiple elevator systems.

---

This repository contains the project structure for implementing a multi-threaded producer-consumer problem using C++ to simulate parking management in a multi-level parking garage. The goal is to find the best available parking spot near an elevator using advanced algorithms such as Dijkstra's Algorithm for optimal efficiency.

