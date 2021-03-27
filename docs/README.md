# Minigame Core Docs

## Component
A building block of a minigame, there are different component types for different things.
Components can be imagined like those in Unity, objects in the environment, except our components are only for minigames.

Components would include things like [worlds](#worlds), [players](#players), [minigames](#minigame) and more.
Components start off with primitive types and build from there, you can build components that are just environment objects like blocks, or you can include livezones in the component relative to some point in it that define an item generator.

Components are easily remixable into custom components and are designed to be one of the CORE features of the Minigame Core.

They are about as abstract as [livezones](#livezones)

### Account
A special component that contains a user account and any features you want to specify on it.

An account allows you to define permanent data for a user in components... You can also access an account via a player in game and get access to certain data they have.
Data can include anything by a user, minigame stats like wins, losses and kills, and even custom effects.

Accounts are meant to facilitate the access of data to an account.
Account components WILL NOT store credentials. If anything this should be setup separately.

Finally Account components should have a way to set feature visibility for a certain world/minigame.

### Server Root
A special component that specifies the server that the minigame core is running on, it would be the root component that all other components are defined on and would allow you to specify server options. In here you would be able to define all the worlds and minigames of your server.

The idea of the server root is being able to literally design a server similar to Hypixel with lobbies, minigames and more without much hassle.

The Server Root would allow you to define the default server players are routed to. This would use a custom utility called Router that defines abstract actions like join(Player) disconnect(Player) that basically allows us to control where and what a player sees on the server.

### Minigame
Custom [component](#component) objects that represent a minigame. When running in an actual situation, they will automatically generate/delete worlds on minigame start/end (before start and after end actions). 
They have some start/end criteria and actions for each of those as well.

For instance on minigame start, you can tp all players to a random spawn point in the map, spawn points are [attributes](#attributes) that can be assigned to a livezone (or point)

And on minigame end, you can route [players](#players) to either another version of the same minigame or to the minigame's lobby depending on what their preferences are.

In this component you can also define the minimum and maximum number of players for a game, this will allow the minigame core to handle starting the minigame for you automatically.

There will be many other default properties that will be accessed at the code level during actual minigame running. For instance default world in the case your minigame has multiple worlds. If your minigame only has one world in it, that will be the default world.

Minigames should be able to encompass any minigame you imagine from capture the flag, to bedwars, to the entirety of Hypixel Skyblock.

### Players

Entities that are controllable by a player, a custom type of [component](#component).

### Worlds

Dimensions that [players](#players) can exist in, existence meaning [players](#players) can be spawned into a world, move around, etc.

There are 2 types of worlds as of now, lobbies, and minigame worlds.
Essentially lobby worlds are for hosting players helping them navigate to specific worlds and such, while minigame worlds are ones housed under [minigames](#minigame) that are only there to help a minigame perform its function.

Worlds are just like any other [component](#component) in terms of data storage.

## Attributes
Data structures with a type, name and OPTIONAL icon for identification purposes.
You can only apply and set the values of an attribute in the web-editor.
With [enums](#enums) you can select the value from a list compared to manual input.

Attributes can be defined as permanent or temporary, generally permanent attributes should be described in places like lobby [worlds](#worlds) or on the [server-root](#server-root) while temporary attributes should be described in [minigames](#minigame) and any components inside of one.

When components try to access some attribute, they get the data from the attribute that is closest to them, and since the whole entire server with this plugin is organized in a folder style, whatever [component](#component) or [group](#groups) this should be easy to imagine.

Components can be created to be defined with attributes by default and there will be some attributes that will literally be built into the minigame core (in a file) and that if removed would break the whole entire plugin.

### Custom Items

Lists of [attributes](#attributes) that describe an item.

You can add modules to items with collections of [attributes](#attributes) for specific reasons.

## Stats

Collections of attributes that can be applied to a [component](#component) or [group](#group)

## Groups

Literally a folder with [component](#component) and other groups in it.
You can apply [stats](#stats) and [attributes](#attributes) to a group, put livezones in it, and do basically anything you could do in a [component](#component).

