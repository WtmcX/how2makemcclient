# Making the Hook

Hooking our client to the Minecraft main class.

---

## Making Our Main Class

1. **Navigate to** `src/main/java` and create a package (e.g., `com.demez`).
2. **Inside the package**, create a new class and name it as you wish. This will be your Main class.

Here is an example of a Main class:

```java
package com.demez;

import org.lwjgl.Display;

public class YourClient {
    public YourClient INSTANCE = new YourClient();
    public String name = "YourClient";
    public String version = "1.0.0";
    
    public void init(){
        // Prints "Client launched" to the console.
        System.out.println("Client launched.");
        // Sets the window title to your client name and version.
        Display.setTitle(name + " " + version);
    }
}
```

---

## Hooking Our Main Class

1. **Open the** `Minecraft.java` class.
2. Press `Ctrl + F` and search for `this.ingamegui`.
3. Below that line, add the following code:

   ```java
   YourClient.INSTANCE.init();
   ```

4. Launch the game. You should see `"Client launched"` text in the console.
