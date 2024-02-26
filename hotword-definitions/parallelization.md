## Parallelization

Parallelization in programming is the technique of dividing a task into smaller sub-tasks and executing them simultaneously on multiple processing units (such as CPU cores or distributed systems) to improve performance. Unlike concurrency, which focuses on managing multiple tasks, parallelization focuses on executing tasks simultaneously to speed up overall execution.

Here's a simple example in Java demonstrating parallelization using the Executor framework and Java 8's CompletableFuture:

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ParallelizationExample {
    public static void main(String[] args) {
        // Create an executor service with a fixed thread pool size
        ExecutorService executor = Executors.newFixedThreadPool(2);

        // Define two CompletableFutures representing tasks
        CompletableFuture<Void> future1 = CompletableFuture.runAsync(() -> {
            // Simulate some task execution
            for (int i = 0; i < 5; i++) {
                System.out.println("Task 1 is executing iteration " + i);
                try {
                    // Introduce a short delay to simulate work
                    Thread.sleep(1000); // Sleep for 1 second
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("Task 1 is complete");
        }, executor);

        CompletableFuture<Void> future2 = CompletableFuture.runAsync(() -> {
            // Simulate some task execution
            for (int i = 0; i < 5; i++) {
                System.out.println("Task 2 is executing iteration " + i);
                try {
                    // Introduce a short delay to simulate work
                    Thread.sleep(1000); // Sleep for 1 second
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("Task 2 is complete");
        }, executor);

        // Wait for both tasks to complete
        CompletableFuture.allOf(future1, future2).join();

        // Shutdown the executor service
        executor.shutdown();
    }
}
```

In this example, we create an `ExecutorService` with a fixed thread pool size of 2, which means it can execute two tasks concurrently. We then define two `CompletableFuture` objects, each representing a task. Inside each `CompletableFuture`, we simulate some work by printing messages and sleeping for 1 second in each iteration.

We execute both `CompletableFutures` asynchronously using the

 `runAsync()` method, which schedules the tasks to run on the executor service. This allows the tasks to execute in parallel.

Finally, we use `CompletableFuture.allOf()` to wait for both tasks to complete before shutting down the executor service.

Overall, this example demonstrates parallelization by executing two tasks simultaneously on separate threads, potentially leveraging multiple CPU cores to improve performance.