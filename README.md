# Task_Management_1.0.3
Task management system updated with the addition of logging 

---

### **Ticket Breakdown: Implement Logging in Task Management System**

**Objective**: Add structured logging using SLF4J (`log.info` and `log.warn`) in the controller classes of the Task Management System to track operations like creating, updating, deleting, and retrieving tasks.

---

#### **Ticket 1: Add Logging Dependency to `pom.xml`**

**Tasks**:
1. Open the `pom.xml` file.
2. Add SLF4J and Log4j 2 dependencies. These will allow the application to log important events such as task creation, updates, and deletions.
   ```xml
   <!-- SLF4J API -->
   <dependency>
       <groupId>org.slf4j</groupId>
       <artifactId>slf4j-api</artifactId>
       <version>1.7.32</version>
   </dependency>

   <!-- Log4j 2 SLF4J Binding -->
   <dependency>
       <groupId>org.apache.logging.log4j</groupId>
       <artifactId>log4j-slf4j-impl</artifactId>
       <version>2.21.0</version>
   </dependency>

   <!-- Log4j 2 Core -->
   <dependency>
       <groupId>org.apache.logging.log4j</groupId>
       <artifactId>log4j-core</artifactId>
       <version>2.21.0</version>
   </dependency>
   ```

**Hints**:
- Ensure that no other logging libraries like Logback are included in the project, to avoid conflicts.
- SLF4J serves as an abstraction layer for logging, and Log4j2 provides the logging implementation.

---

#### **Ticket 2: Configure Logging in `application.properties`**

**Tasks**:
1. Open the `application.properties` file.
2. Configure the logging level for the application’s main package:
   ```properties
   # Set the logging level for your package
   logging.level.org.rma.taskmanagement=INFO

   # Log to a file
   logging.file.name=logs/task-logfile.log
   ```

3. You can also customize console logging patterns if needed, but focus on making sure log messages go to the file for now.

**Hints**:
- Setting the logging level to `INFO` will ensure that important application events are logged. 
- You can log both to the console and to a file for better visibility of the events happening in your application.

---

#### **Ticket 3: Add Logging to Task Controller**

**Tasks**:
1. Open `TaskController.java`.
2. Add `@Slf4j` to enable logging within the class.
   ```java
   @Slf4j
   @Controller
   @RequestMapping("/tasks")
   public class TaskController {
       // Controller methods
   }
   ```

3. Add `log.info` for regular events and `log.warn` for warning scenarios:
   - **`log.info`** should be used for normal operations, such as creating, fetching, and updating tasks:
     ```java
     log.info("Creating new task: {}", task);
     log.info("Fetching task with ID: {}", id);
     ```

   - **`log.warn`** should be used for situations like when a task cannot be found:
     ```java
     log.warn("Task with ID: {} not found", id);
     ```

**Hints**:
- Focus on `log.info` for routine events like task creation, update, and deletion.
- Use `log.warn` to signal potential issues, such as a missing task ID.
- **No need for `log.debug`** at this point, as it is typically used for development purposes or debugging detailed issues that aren't needed for the core flow of logging in this case.

---

#### **Ticket 4: Test Logging Functionality**

**Tasks**:
1. Start the application and interact with the Task Management System (create, update, delete tasks).
2. Check the log file (`logs/task-logfile.log`) to verify that the log messages for the following operations are recorded:
   - Task creation (`log.info`)
   - Task retrieval (`log.info`)
   - Task update (`log.info`)
   - Task deletion (`log.info`)
   - Missing task warning (`log.warn`)


**Hints**:
- Review the log file to confirm that the correct log messages appear for each action.

---
