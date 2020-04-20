# Java Fundamentals: Asynchronous Progamming using Completion Stage

### Module 1 - Course Overview
_Nothing much to note here_

---

### Module 2 - Introducing Asynchronous vs. Concurrent Tasks

##### Overview 
* CompletionStage / CompletableFuture
    * API introduced in Java 8
    * Create pipeline of tasks in an async way
    * Error handling - try / catch pattern will not work very well with async
    * Performance 

##### Pre requisites
* Java - fair knowledge and its main API
* Concurrent Programming; Pluralsight - Applying Concurrency and Mult-threading to Common Java Patterns
* Lambda expressions; PS - From Collections to Streams in Java 8 Using Lambda Expressions 
* The Stream API; PS - Streams, Collectors and Optionals for Data Processing in Java 8

##### Agenda of the Course
* Introducing the Big Picture - Vocabulary
* Launching a first task, technical details
* Launching tasks on the completion of other tasks
* What can you do when things go wrong?
* Let us talk about performance

##### Agenda of this Module
* Let us define the technical terms
* Launching a concurrent task
* Synchronous vs. asynchronous
* Blocking vs. non-blocking 
* Message driven vs. event-driven

##### Technical Vocabulary
* Concurrency
    * Means we are executing code in several threads to be able to do more than 1 thing at the same time
    * A task is created in a thread. Creating a task in a thread does not mean, this task is going to be executed in the same thread. It can be executed in another thread.
    * The result is passed to the first thread to be further processed or to generate other tasks. 
    * _Skipping noting down the example_
    * Learnings
        * The executor pattern enables the launching of tasks in other threads
        * But it does not offer the non-blocking behaviour. “Get”ting the result is a blocking call. 
        * Since _getting_ the result can _block_ the _launching_ thread which we want to avoid
            * We want to launch subsequent tasks automatically on the completion of task we have sent to the ExecutorService
    * Synchronous vs. Async
        * Sync: The thread that launch the task needs to wait for the task to complete to continue to work
        * Async: The task is executed at some point in the future without “wait"ing 
    * Does async mean “in another thread”? No. 
    * Asynchronous and concurrent are two different notions. We can be async without being concurrent. And being concurrent doesn’t necessarily mean that we are asynchronous. A task can be async and can still be called in the thread we are running in. 
* Blocking vs. Non-blocking
    * _Blocking_ means that a thread has to _wait_ to execute a task or access a resource
    * _Synchronization_ is a _blocking_ way to prevent race conditions
    * Is there a non-blocking way of chaining a task on the _completion_ of _another task_? Unfortunately _NO_, with the current API (ExecutorService + Runnable).  
    * What we need here is the following:
        * Being able to trigger a task on the completion of another one
        * Being able to specify in which thread a task is executed
* Message Driven vs. Event Driven 
    * Could the solution come from either of those approaches?
    * _CDI - Context and Dependency Injection example from Java EE_
    * Event
        * An event is triggered to notify the change of a state. The recipient has to declare itself to the source usually through a broker. It is _usually_ synchronous and blocking. There are also async ways of doing this built via the _CompletableFuture_ API. 
    * So, _events_ are _not_ the right tool, what about messages?
        * A message is sent to a broker that will _trigger_ the _subscribers_ of this kind of _message_ in another thread sometimes even in another JVM. 
        * So it’s clearly neither the right way to update, for instance, a local interface. Messages are nice but mostly to deal with other parts of our application. 
    * Event vs. Message
        * An event is a signal
        * A message is a piece of data that recipients will get and react upon. A message can also carry an event to different parts of our application. 


##### Module wrap up
* Lessons learnt
    * Notions needed to work with the CompletableFuture API
    * Execution of tasks in a specific thread
    * Blocking vs. non-blocking calls
    * Async execution
    * None of the solutions offered by the JDK up to this point (CompletableFuture) are valid for async programming in Java. The problem is now set up, we call the CompletionStage API to solve it

---

_To be continued..._


