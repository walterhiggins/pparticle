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

If you see 2 displayed then ScriptCraft has loaded. The /js command lets you execute any Javascript statement - in this case 1 + 1 . Javascript is a full-feature programming language capable of doing much more than simple mathematics. 

## Your first Minecraft Mod
Let's start by writing a simple plugin that displays a message in the Server console when the server starts up. In the same 

## Howling Blocks

## Next Steps
[forge]: http://www.minecraftforge.net/forum/
[cm]: http://canarymod.net/
[spigot]: http://www.spigotmc.org/