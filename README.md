# Tutorial 10 - Timer Future
**Maria Helga Grizelda - 2206046733**

## 1.2 Understanding How It Works
<img src="image/Screenshot 2024-05-08 at 17.51.12.png">

The output demonstrates that the async function runs independently from the main function calling it. Thus, hey hey might be printed before howdy! and done! because hey hey is executed outside the async function. While the async function awaits the future's result, the program continues and executes println!("hey hey");.


## 1.3 Multiple Spawn and removing drop
### Adding multiple spawn
<img src="image/Screenshot 2024-05-08 at 18.02.10.png">

When we introduce several spawners into the system, it ramps up the number of tasks piled up in the task sender, acting as a sort of message queue. This setup causes the program to keep running indefinitely, assuming there's always new data pouring in from spawners. Each time a spawner calls the spawn function, it creates a fresh task, which gets added to the task sender's queue. Then, the executor picks up and executes these tasks one by one until there are no more left, at which point the spawner is dropped, signaling that the interaction has wrapped up.


### `drop(spawner)` removed
<img src="image/Screenshot 2024-05-08 at 18.01.37.png>">

For a smooth process, it's crucial to remember to call drop(spawner) to signify the end of using a spawner. Think of the spawner as a message queue: whenever we spawn something, it's like dropping a message into the queue. As the executor does its thing, it grabs messages from this queue. Dropping the spawner tells the system that we're done tossing messages into the queue, allowing the executor to finish up any remaining tasks and eventually bring the program to a halt.

This setup also clarifies why "done2!" pops up after "done3!" in the output, even though they're coded in reverse order. Since tasks run concurrently, they don't wait for each other, meaning there's no guarantee they'll finish in the same order they're written. This asynchronous behavior lets tasks happen simultaneously without needing to follow a strict sequence.