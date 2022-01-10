# Guava EventBus Tutorial (MCP)

The Guava EventBus is a clean way of adding events into any Java project. It saves you having to write your own system and is relatively simple to understand and provides all the utility you would need. The EventBus allows publish-subscribe communication between components without requiring the components to explicitly register with one another.
## Setup and Registering our Class
We start by looking at the EventBus object. It can register listeners and post events. Using it is as easy as instantiating the class.
If you're following along add this within your client's main class:
```
private EventBus eventBus = new EventBus();
...
public void preInitialize() {  
  this.eventBus.register(this.getInstance()); // Don't forget to do for other class with listeners!!!
```
And within out Minecraft.java file you want to get you Client class:
```
private void startGame() throws LWJGLException  
{  
  new Client().preInitialize;
  ...
```
If you don't have a method within the main class of your client, you can simply put it (the EventBus register) in the classes constructor.
## Creating Listeners
The next thing we do is create a listener class. This will be empty most of the time but you could methods inside of it. There are draw backs to doing this and the main one is that if multiple classes need an event (lets say a tick event).
In our example it will be empty:
```
public  class TickEvent {

}
```
Once we have our class we can use it as we please. For example you could go to you client's main class and throw in:
```
@Subscribe  
public void tickEvent(TickEvent tick) {
	System.out.println("Client Tick")
}
```
## Posting Events
Once you've got that set up we need to post the event. In our case as we are doing a tick event we are going to post the event in Minecraft.java.
You will need to go to the bottom of runTick() and add the line:
```
    }  
  
  Client.getInstance().getEventBus().post(new TickEvent()); // Add this
  this.mcProfiler.endSection();  
  this.systemTime = getSystemTime();  
}  
  
/**  
 * Arguments: World foldername,  World ingame name, WorldSettings 
 * */
```
Congrats! You are now all done. When you run your game now you should see your console repeatedly say "Client Tick".


