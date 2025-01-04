# Making the module base

Lets create our files! First of all you need to create a package named 'module' after that you need to create these files: Module.java  ModuleManager.java and Create the enum named Category.java ... After these, open the Module.java class. Here is an example Module class

```java
package com.demez.module;

import net.minecraft.client.Minecraft;
import net.minecraft.client.entity.EntityPlayerSP;
import net.minecraft.client.multiplayer.PlayerControllerMP;
import net.minecraft.client.multiplayer.WorldClient;
import net.minecraft.network.Packet;

/**
 * The Module class serves as the base for the module system.
 * Each module has a name, a keybind, a toggle state, and a category.
 */
public class Module {

    // Provides access to the Minecraft game instance.
    protected Minecraft mc = Minecraft.getMinecraft();
    
    // The name of the module.
    private String name;
    // The keybind assigned to the module.
    private int key;
    // Indicates whether the module is enabled or disabled.
    private boolean toggled;
    // The category to which the module belongs (e.g., Combat, Movement, Render).
    private Category category;

    /**
     * Constructor for the Module class. Initializes the module's properties.
     *
     * @param nm The name of the module.
     * @param k The keybind for the module.
     * @param c The category of the module.
     */
    public Module(String nm, int k, Category c) {
        name = nm;
        key = k;
        category = c;
        toggled = false; // Default state is disabled.
        setup(); // Calls the setup method for additional configuration.
    }

    /**
     * Toggles the module's state (on/off).
     */
    public void toggle() {
        toggled = !toggled; // Switch the current state.
        if (toggled) {
            onEnable(); // Handle enabling the module.
        } else {
            onDisable(); // Handle disabling the module.
        }
    }

    // Called when the module is enabled.
    public void onEnable() {}

    // Called when the module is disabled.
    public void onDisable() {}

    // Called on every game tick to update the module.
    public void onUpdate() {}

    // Called every frame to render visuals related to the module.
    public void onRender() {}

    // Used for initial setup of the module.
    public void setup() {}

    // Below are getter and setter methods to access private variables.

    public Minecraft getMc() {
        return mc;
    }

    public void setMc(Minecraft mc) {
        this.mc = mc;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getKey() {
        return key;
    }

    public void setKey(int key) {
        this.key = key;
    }

    public boolean isToggled() {
        return toggled;
    }

    public void setToggled(boolean toggled) {
        this.toggled = toggled;
    }

    public Category getCategory() {
        return category;
    }

    public void setCategory(Category category) {
        this.category = category;
    }

    /**
     * Provides access to the current player object.
     *
     * @return The current player.
     */
    protected EntityPlayerSP player() {
        return mc.thePlayer;
    }

    /**
     * Provides access to the player's controller.
     *
     * @return The player's controller.
     */
    protected PlayerControllerMP playerController() {
        return mc.playerController;
    }

    /**
     * Provides access to the current game world.
     *
     * @return The current world object.
     */
    protected WorldClient world() {
        return mc.theWorld;
    }

}
```

Here is an example Category enum. That is our module categories.

```java
package com.demez.module;

public enum Category {
    MOVEMENT, PLAYER, COMBAT, MISC
}
```

And that is our ModuleManager class: That is the class that we are going to store our modules

```java
package com.demez.module;

import java.util.ArrayList;

import net.minecraft.client.Minecraft;
import net.minecraft.util.ChatComponentText;

public class ModuleManager {
	
	private static ArrayList<Module> mods;
	
	public ModuleManager() {
		mods = new ArrayList<Module>();
		//COMBAT
		
		
		//MOVEMENT
		
		
		//PLAYER

		
		
		//RENDER
		
		
		//MISC
	}
	
	public static void newMod(Module m) {
		mods.add(m);
	}
	
	public static ArrayList<Module> getModules(){
		return mods;
	}
	
	public static void onUpdate() {
		for(Module m : mods) {
			m.onUpdate();
		}
	}
	
	public static void onRender() {
		for(Module m : mods) {
			m.onRender();
		}
	}
	
	public static void onKey(int k) {
		for(Module m : mods) {
			if(m.getKey() == k) {
				m.toggle();
			}
		}
	}
	
	

}
```

After that click shift 3 times so fast an a window will open. Search for EntityPlayerSP and open it then Click Ctrl + F search for onLivingUpdate() void. And add this line of code:
```
YourClient.INSTANCE.moduleManager.onUpdate();
```

After that (again) go to Minecraft.java class and search for ```k == 1``` go above the if statement and type ```YourClient.INSTANCE.moduleManager.onKey(k);``` . Thats all you need