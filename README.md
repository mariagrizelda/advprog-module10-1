# Tutorial 10 - Timer Future
**Maria Helga Grizelda - 2206046733**

## 1.2 Understanding How It Works
<img src="image/Screenshot 2024-05-08 at 17.51.12.png">

The output demonstrates that the async function runs independently from the main function calling it. Thus, hey hey might be printed before howdy! and done! because hey hey is executed outside the async function. While the async function awaits the future's result, the program continues and executes println!("hey hey");.