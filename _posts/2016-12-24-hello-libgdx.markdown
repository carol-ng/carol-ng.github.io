---
layout: post
title:  "Danmakube: A beginner's tutorial to libGDX, part 1"
date:   2016-12-24 22:22:32 -0500
categories: posts
description: Heaven is a neverending bullet hell.
---

I hadn't tried to make a non-command-line based arcade game since the Snake and Pac-Man labs in CPSC 110 two years ago, but since I've got time this winter break, I've decided that I will try tackling the world of games once more. I'm going to be building a very simple, 2D graphic, top-down shooter, and hopefully be able to include some of the awesome bullet patterns that really define the bullet hell genre.

If you've used libGDX before, you'll notice that the mechanics of the game echoes many concepts from the tutorial for the [Very Simple Game](https://github.com/libgdx/libgdx/wiki/A-simple-game), except in a bullet hell, you'll quickly realize that the aim of the game is _not_ to catch as many bullets as possible.

## Part 1: Setup

LibGDX is quite generous with their setup tools - there's a whole [.jar file](https://github.com/libgdx/libgdx/wiki/Project-Setup-Gradle) devoted to generating all the files you'll need to import into your IDE of choice and get developing immediately. Once you've decided on a project name and the platforms you're going to support, you're 100% ready to go.

Once you opened the project in your IDE, you'll notice that several files and folders have already been created. I'll touch briefly on the two I think are most important:

* `core/src/com/project/gamename/GameName.java`: This is the file that will be at the core of your project. Depending on how you structure your development environment, it might also be where all the action takes place.
*  `android/assets`: All of the external assets in your game that are not code will probably live here, such as sprites, sounds and background music. I don't know why it's in the `android` folder, but it's a good thing to memorize.

Most of the game logic code will go in the `render()` method, but first, we need to create a few objects in the `create()` method of our main game:

```java
// This is the create() method.
```

Brief descriptions of the objects we just created:

- `blah`: blah
- `blah`: blah

We'll create some functions to play with these objects in the next section...

## Part 2: Logic

I found logic to be one of the more fun parts of development. For the sake of simplicity, I've chosen to make the simplest version of the shooter with one enemy and one ship (controlled by the player). Although the super pretty bullet patterns might have to wait, it wouldn't be too much of a hassle to try and implement a classic wave (see crude sketch below).

Figure 1: An illustration of the "simple wave" bullet pattern. <diagram of the wave> 

### Bullets 

Since we won't be displaying a lot of bullets in one game (our game has only one boss, after all), it is safe to use and iterate over an array of bullet objects. If you have a lot of objects, libGDX has a [Poolable](http://libgdx.badlogicgames.com/nightlies/docs/api/com/badlogic/gdx/utils/Pool.Poolable.html) interface for large groups of objects for optimized memory usage.

One of the simplest object representations in libGDX is a [Rectangle](https://libgdx.badlogicgames.com/nightlies/docs/api/com/badlogic/gdx/math/Rectangle.html). It's a particularly useful representation for our Ship and our Bullets, because it has a specific `.overlaps()` method that you can use to calculate how much damage your ship and the boss ship is taking due to the bullets. Since each of our Bullets is travelling in a straight line with a constant speed in some well-defined direction, we can wrap up the Rectangle representation and the speed variables in a Bullet class, which looks like this:

```java
// This is the Bullet class.
```

We could also do this for the player Ship and BossShip, but since they're only one entity each, we can leave them be for now.

We can generate a wave of bullets every _n_ nanoseconds (0.001 milliseconds) using the following code in the `render()` method of our main game: 

```java
// This is the bullet wave code
```

Finally, you can draw the bullet image on top of the Rectangle coordinates:

```java
// This is the bullet drawing code.
```

Note that libGDX specifies the location of the rectangle using the coordinates of the lower left corner of the Rectangle, so we're repositioning the image of the bullet image so that the image is centered on the bullet rectangle.

### Enemy ship(s)

For the sake of simplicity, we will be implementing one instance of an enemy ship. Feel free to wrap up all the methods we use for the ships into another class; once you start extending the game and adding more enemy types, more customization fields can be added to the Ship classes and create a richer overall experience.

We will continue to use a `Rectangle` to represent the enemy ship. Since I wanted the enemy boss to be a little harder to hit, I'm going to move across the game window from side to side.

```java
// This is the code to move the Boss ship.
```

Similar to the bullet drawing method from above, we will draw the enemy ship at the center of the ship's rectangle:

```java
// This is the code to draw the Boss ship
```

### Player ship and user input

last but definitely not least, we'll be drawing the player's ship! In this game, I've opted to use the player's mouse or the touch screen as input for the position of the ship. To avoid reinitializing variables in every `render()` call, we're resetting the touch position of the user as shown:

```java
// This is the user input code
```

Finally, we can shoot bullets from the ship, update the ship's position, and draw the ship image on its coordinates using the following code:

```java
// Here is the code to move ship, draw ship, and fire bullets from the ship.
```

And that's it!

By the end of this tutorial, you should have the following code in your main class:

```java
// Full code for game with no frills, start screen, or anything, really.
```

Your game should look and run a little like this:

`// insert gif of game running`

Stay tuned for an update on adding polish and additional improvements!

**Update:** [The new post is up!]({% post_url 2016-12-27-hello-libgdx-2 %})
