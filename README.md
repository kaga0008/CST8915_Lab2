# CST8915 Lab 1
## Elizabeth Kaganovsky (040956095)

### Video Demo: https://youtu.be/NTSfl1J_mXg

Order_service repo: https://github.com/kaga0008/CST8915_Lab2_order-service<br>
Product_service repo: https://github.com/kaga0008/CST8915_Lab2_product-service<br>
Store_front repo: https://github.com/kaga0008/CST8915_Lab2_store-front<br>

### What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?
- To order_service:
    - A .env file was created to hold on to all environment variables.
    - In index.js, the port and RabbitMQ connection string are extracted from the .env file rather than being hardcoded.
- To product_service:
    - A .env file was created to hold on to all environment variables.
    - In this case, the only thing moved is the port number.

In this case, the Configuration factor is met simply by moving these pieces of data to .env files. Satisfying the Backing Services factor involves treating these services as if they are local services, accessing them using the configuration info in the .env files (in this case--the RabbitMQ login credentials and IP).

### Why is it important to use environment variables instead of hard-coding configurations in your application?
- Environment variables are used to sequester resource handles and private credentials to their own file(s) which can be modified to fit the environment they are in, which serves as the primary means to satisfy the "config" element of the twelve factor application methodology. For example, a .env file may contain the login credentials and IP address of the virtual machine that that the associated application will communicate with--thus, they must be kept private lest other users gain access to that machine. In the Lab 2 application, the order-service has a .env file that contains the connection credentials (username, password, IP) of the RabbitMQ service, if exposed through hardcoding, malicious actors could send in fake orders.


### Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?
- Separate respositories for each microservice provides a great amount of benefits for an application. A notable boon is that of narrowing dependencies--in the Algonquin Pet Store, each repository demands its own set of dependencies, and for an instance of the entire application to be run on a single machine, a significant amount of space must be devoted to this. By partitioning an application into microservices, each machine requires a much lighter weight set of dependencies to run it's associated service, meaning smaller VMs are required to run each service. Additionally, developers benefit from the separated repositories, since each one can be independently developed and deployed without interferrence from the other parts of the app. Configuration data is also more secure when using multiple repositories, as a smaller set of environment variables is easier to manage and reduces the risk of hard-coded environment variables accidentally being shared.
