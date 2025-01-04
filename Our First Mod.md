# Our first mod!

So i want to make Flight mod as first module. Create a class in your **modules** package and add the following code:

```java
package com.demez.module.movement;

import com.demez.module.Module;

public class Flight extends Module{
    public Flight(){
        super(”Flight”, Keyborard.KEY_F, Category.MOVEMENT);
    }

    @Override
    public void onEnable(){
        if (this.isToggled){
            mc.thePlayer.capabilities.isFlying = true;
            mc.thePlayer.capabilities.allowFlying = true;
        }
    }

    @Ovverride
    public void onDisable(){
            mc.thePlayer.capabilities.isFlying = true;
            mc.thePlayer.capabilities.allowFlying = true;
        
    }
}
```