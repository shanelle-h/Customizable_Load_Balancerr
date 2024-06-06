**README: Task 1 - Task 4**

**Task 1: Server Implementation**

**Overview:**
In Task 1, we implemented a simple web server that accepts HTTP requests on port 5000 and provides two endpoints: `/home` and `/heartbeat`. The `/home` endpoint returns a string with a unique identifier to distinguish among replicated server containers. The `/heartbeat` endpoint sends heartbeat responses upon request, allowing the load balancer to identify failures in the set of containers maintained by it.

**Implementation:**
We implemented the server using Python, utilizing the Flask framework for handling HTTP requests. The server runs on port 5000 and provides the required endpoints as specified in the assignment. The server's unique identifier is set as an environment variable while running a container instance from the Docker image of the server.

**Dockerfile:**
We included a Dockerfile to containerize the server as an image, making it deployable for subsequent tasks. The Dockerfile installs necessary dependencies and sets up the environment for running the Flask application.

**Deployment:**
To deploy the server, build the Docker image using the provided Dockerfile and run a container instance from the built image. Ensure that the container is exposed on port 5000 to accept incoming HTTP requests.

**Task 2: Consistent Hashing Implementation**

**Overview:**
In Task 2, we implemented a consistent hash map using Python, which serves as the underlying data structure for the load balancer in Task 3. We utilized an array-based implementation to represent the hash map, with provisions for handling collisions using linear or quadratic probing.

**Implementation:**
We implemented the consistent hash map using Python, utilizing an array data structure to represent the hash map and hash functions provided in the assignment. The implementation ensures that requests are mapped to the appropriate server instances based on the consistent hashing algorithm.

**Task 3: Load Balancer Implementation**

**Overview:**
Task 3 involves building a load balancer container that uses the consistent hashing data structure from Task 2 to manage a set of server replicas. The load balancer is responsible for routing client requests to server replicas in a balanced manner and maintaining the desired number of replicas even in case of failure.

**Implementation:**
We implemented the load balancer container using Python and Flask, leveraging the consistent hashing data structure implemented in Task 2. The load balancer provides HTTP endpoints for modifying configurations, checking the status of managed web server replicas, and routing client requests to server replicas.

**Endpoints:**
- `/rep`: Returns the status of the replicas managed by the load balancer.
- `/add`: Adds new server instances to scale up with increasing client numbers.
- `/rm`: Removes server instances to scale down with decreasing client or system maintenance.
- `/<path>`: Routes client requests to a server replica as scheduled by the consistent hashing algorithm.

**Deployment:**
Deploy the load balancer container using the provided Dockerfile, Docker-compose file, and Makefile. Ensure that the load balancer is exposed on port 5000 to accept incoming HTTP requests.

**Task 4: Analysis**

**Overview:**
Task 4 involves testing and analyzing the performance of the load balancer implementation in different scenarios, including load distribution among server containers and recovery from server container failure.

**Experiments:**
- **A-1:** Launch 10000 async requests on N = 3 server containers and report the request count handled by each server instance.
- **A-2:** Increment N from 2 to 6 and launch 10000 requests on each increment. Report the average load of the servers at each run.
- **A-3:** Test all endpoints of the load balancer and demonstrate that it spawns a new instance quickly in case of server failure.
- **A-4:** Modify the hash functions and report the observations from A-1 and A-2.

**Conclusion:**
Overall, the load balancer implementation effectively distributes the load among server containers and demonstrates scalability and fault tolerance. The analysis provides insights into the performance and behavior of the load balancer in various scenarios, contributing to the understanding of distributed systems and load balancing techniques.
