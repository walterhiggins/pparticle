# Minecraft Modding is easier than you think

If you've played Minecraft but are curious about creating your own Mods, read on...

One of the reasons Minecraft has become so popular is that it's possible to 'Mod' or modify the game, adding new features and rules which aren't present in the standard Minecraft experience. 

## Modding Minecraft 

Because the standard Minecraft server provided by Mojang isn't easily modifiable, there are a couple of projects devoted to making Minecraft Modding possible. 

* [CanaryMod][cm]
* [Forge][forge]
* [Spigot][spigot]
* ... and many others

All of the above frameworks provide APIs (Application Programming Interfaces - a set of procedures that can be called) which make it possible for mod creators to add new features to the game. 

Because Minecraft is written in the Java Programming language, each of the Modding Frameworks also use Java and require Mod creators to understand Java. 

Java is a full-featured language used most commonly for business applications. It's a difficult language to learn if you're just starting out programming. 

## ScriptCraft

ScriptCraft is a project I created to make it easier to create Minecraft Mods. ScriptCraft makes it possible to create Mods using the JavaScript programming Language. Java and JavaScript have similar names but they are very different languages. 

## Javascript
JavaScript is most commonly used in Web Pages but because of its power and simplicity it is increasingly used in other applications too. JavaScript is concise, meaning you can do more with less code, and its simplicity makes it easier to learn - especially for beginners.

## Getting Started
To create Mods using ScriptCraft you'll need to first download and install CanaryMod from http://canarymod.net/ . Once you've downloaded the CanaryMod .jar file you run the CanaryMod server using the java command. On windows launch a Command Prompt (Click Start, All Programs, Accessories, Command Prompt) then type the following command:

    java -jar CanaryMod-1.2.0.jar 

The first time you run CanaryMod it will stop because you need to agree to Mojang's (the makers of MineCraft) End-User License. Open the eula.txt file in Notepad or another text editor and change the line beginning with eula so it reads as follows:

    eula=true

Save the file then restart CanaryMod. This time CanaryMod will continue and will create a plugins directory and many other files and directories. Download ScriptCraft - a plugin for CanaryMod - from the CanaryMod plugins web page http://canarymod.net/plugins. Save the scriptcraft.jar file in the plugins directory then shutdown CanaryMod by typing `stop` at the CanaryMod command prompt. Start up CanaryMod again and this time you should see messages in the command window as ScriptCraft is loaded. At the CanaryMod command prompt, type the following command to verify ScriptCraft has loaded:

    js 1 + 1

If you see 2 displayed then ScriptCraft has loaded. The `js` command lets you execute any Javascript statement - in this case 1 + 1 . Javascript is a full-feature programming language capable of doing much more than simple mathematics. The next thing you should do is make yourself an operator using the `op` command. Type `op NAME` replacing NAME with your own minecraft user name. 

## Your first Minecraft Mod
Let's start by writing a simple plugin that displays a message in the Server console when the server starts up. In the same directory where the CanaryMod .jar file lives there should now be a scriptcraft directory and in that directory you'll find a plugins directory. ScriptCraft is a CanaryMod Plugin which lets you load Javascript plugins. Plugins are code which is executed when the server starts up. 

Using a Text Editor ( I recommend Notepad++ for Windows or TextWrangler for Mac OS - both of which are free ) create a new file called `first.js` in the scriptcraft/plugins/ directory and type the following code:

```javascript
console.log( 'Hello World' );
```

Save the file then stop CanaryMod and start it again. This type you'll see a message `Hello World` appear in the CanaryMod console. What happened here is your `first.js` file was loaded during the Server startup and the javascript code inside it was executed. The statement `console.log( 'Hello World' )` "logs" (or prints) a message - in this case 'Hello World' - to the console. This isn't a terribly exciting Minecraft Mod but it illustrates how Minecraft Mods are loaded - at startup time. 

## Howling Blocks
One of the really cool things about Minecraft Modding is the ability to 'listen' for 'events' in the game and to change the normal rules of the game. 'Events' are anything which happens in the game - for example, a player breaking a block, an animal moving, lava flowing, an arrow striking something. It's possible for Mod creators to 'listen' for these events and change what happens when these events occur. In programming terms this is called 'Event-Driven Programming'. There are over 100 possible events in Minecraft - you can see a full list at http://scriptcraftjs.org/api#events-helper-module-canary-version . 

This next Mod will change the game behavior so that whenever a block is broken it howls like a wolf. Create a new file called `howling-blocks.js` in the scriptcraft/plugins directory and type the following code:

```javascript
var sounds = require('sounds');
function howl(event){
  var block = event.block;
  var location = block.location;
  sounds.wolfHowl( location );
}
events.blockDestroy( howl );
```

Save the file and restart CanaryMod. Then launch Minecraft and choose 'Multiplayer' to connect to your CanaryMod server. You'll need to add a new server with the IP Address `localhost` (that's a special address which refers to your own computer). Join the server and break some blocks. When the blocks are broken they should emit a wolf-howl. This simple Mod illustrates how event-driven programming works. In the above code we created a new `function` (a set of statements) which will be executed whenever the `blockDestroy` event occurs. We gave the function a name: `howl()` and connected that function to the `blockDestroy()` event using the following code:

```javascript
events.blockDestroy( howl );
```
The `howl()` function only gets called whenever a block is broken. Itreceives an `event` and process that event, it get the location of the block which was broken and plays a sound at that location. This Mod makes use of ScriptCraft's API. The `sounds` module is just one of the many modules provided by ScriptCraft's API which you can browse at http://scriptcraftjs.org/api . 

## Lightning Arrows
Let's step things up a notch and create a more exciting Mod - one which will add Lightning-Strike arrows to the game. When a player shoots an arrow a bolt of lightning will strike where the arrow lands. Create a new file in the scriptcraft/plugins directory called lightning-arrows.js and type the following code:

```javascript
var cmArrow = Packages.net.canarymod.api.entity.Arrow;
var cmPlayer = Packages.net.canarymod.api.entity.living.humanoid.Player;
function strikeLightning(event){
  var projectile = event.projectile;
  var shooter = event.owner;
  var location = projectile.location;
  if (projectile instanceof cmArrow && shooter instanceof cmPlayer){
    location.world.makeLightningBolt(location);
  }
}
events.projectileHit(strikeLightning);
```

Save the file and restart CanaryMod. Then launch Minecraft and choose 'Multiplayer' to connect to your CanaryMod server. Switch to CREATIVE mode by typing `gamemode creative` at the in-game command prompt. Now pick a bow from your inventory and shoot some arrows. A bolt of lightning should strike where each arrow lands. 

The `strikeLightning` function only gets called a projectile (which could be an arrow, snowball or any other in-game item that can be thrown) strikes something. In the strikeLightning function we check to see if the projectile is actually an arrow and if the projectile's owner - the shooter - is a player, and if so lightning is summoned. This is important because skeletons can also shoot arrows and giving such powers to mobs would be dangerous. 

This Mod makes heavy use of CanaryMod's API. For example, Lightning is summoned using the `World.makeLigthningBolt()` function which is documented at https://ci.visualillusionsent.net/job/CanaryLib/javadoc/net/canarymod/api/world/World.html . The CanaryMod API is a collection of functions which Mod creators can call either using Java or JavaScript. There are hundreds of different function calls which can be made. You can browse around the CanaryMod API at https://ci.visualillusionsent.net/job/CanaryLib/javadoc/ . 

## Next Steps
If you're interested in learning more about Minecraft Modding and how to create your own Mods I recommend reading the [Young Person's Guide to Programming in Minecraft][ypgpm] or PeachPit's [Writing Minecraft Plugins in Javascript][wmp].

[forge]: http://www.minecraftforge.net/forum/
[cm]: http://canarymod.net/
[spigot]: http://www.spigotmc.org/
[ypgpm]: https://github.com/walterhiggins/ScriptCraft/blob/master/docs/YoungPersonsGuideToProgrammingMinecraft.md
[wmp]: peachpit.com/store/beginners-guide-to-writing-minecraft-plugins-in-javascript-9780133930146