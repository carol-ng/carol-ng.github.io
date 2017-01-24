---
layout: post
title:  "Danmakube: A beginner's tutorial to libGDX, part 2"
date:   2016-12-26 22:22:32 -0500
categories: posts
description: An game isn't a game without polish!
---

[Previous post:]({% post_url 2016-12-24-hello-libgdx %})

## Part 3: App progression

The previous portion of the tutorial ended with a simple implementation of a 2D shooter with some basic graphics and animations, without all of the bells and whistles. However, a true gamer knows that much of the gameplay experience and initial user delight comes from said bells and whistles, so I'm going to try my best to present a skeleton framework for the following extras:

- Implementing ship health/lives
- Game start/end screens
- Scoreboard implementation

To ensure that our game terminates, we can create a Ship class and add an additional field for health, since we expect that all ships (both enemy and player) will have different health attributes. If the health of the enemy ship runs out before the player's health does, then the player wins, and vice versa.

The game start and end screens are particularly important for any game, as we all know how awkward it would be for a user to have to exit a game fully and completely boot it up again from scratch in order to replay it. The game start and end screens' aim is to facilitate a replay as smoothly as possible, so your users will never be able t put your game down!

Lastly, a scoreboard implementation is crucial to the overall gameplay experience, as it provides the user with some motivation to beat their high score and continue to perform better.

### Ship health

Let's create a new Ship class, similar to how we created the new Bullet class in the previous tutorial:

```java
//This is the code for the Ship class, including the health field.
```

Then we refactor some of our old methods in the main `render` loop to use the Ship methods, and we're all set! In this case, we've assumed that all bullets will cause the same amount of damage, but if you'd like some extra flexibility in that area, you can always add a field to the Bullet class.

### Game start screen

To create a starting screen, we first need to create an extension of the [`ApplicationLIstener`](!!!) class, which is sort of like a new page. Once that's created, we can move some of the objects we created earlier, such as the `SpriteBatch` and the `OrthographicCamera` to the `create` method of the first page, like so:

```java
// This is the code for the strating screen.
```

We then progress to the next screen (the main screen), by adding the following method to the main `render` loop.

```java
// This is the code for the render loop of the start screen.
```

Finally, we add some simple onscreen instructions by importing a font and displaying some instructions. Feel free to go nuts and create a classic pixel art title screen for extra nostalgia points.

```java
// Include the font part in the create method
// Include the instruction drawing in the render loop
```

Once the screen is tapped, we'll be good to go!

### Game end screen

The Game end screen follows similar principles, except we have to add a few methods to smooth the transition from the main game to the final ending screen. We know two things about the behaviour of the ending screen:

- Customized message: Based on the outcome of the game, you'd want the ending screen to display an appropriate message (ie. "YOU WIN" vs "YOU LOSE", depending on the palyer's health)
- Replay button: We want the replay call to action to be as clear as possible
- Space for score display: Since we'll be implementing a scoreboard soon, we can think about where that will go on the end game screen

Taking all these things into account, here's the code we'll use to transition from the main game to the end game screen. Notice how we pass different messages to the screen creator based on the game end condition, and the disposal of all objects to prevent memory leaks:

```java
// This is the main game transition to the next stage.
```

Applying the knowledge of screen creation we learned from creating the start screen, here's the final code for the ending screen:

```java
/// Code for the end screen including the message display, dummy score and "touch anywhere to replay"
```

### Scoreboard implementation

*Under Construction*

## Part 4: Improvements!

Last but not least, we can consider how we're going to extend the game in the future. Although the game we've developed so far works, it's quite far from being a chart topper on any platform. Further imrpovements to make it a "real" game include: 

* UI elements of any sort, and splash screens for any key milestones
* Addition of multiple enemies, or another boss, to add some variety
* A more polished scoring system, beyond time
* Neverending extension, or some kind of level system
* Prettier patterns and bullets (you can never have enough of those!)
* Full support for other platforms (Android, HTML5, iOS)

Thankfully, the last point is relatively easy to achieve, since libGDX takes care of of the heavy lifting regarding app logic, and most issues around native support are extremely well-documented by their respective producers. Maybe I'll get around to making a poslied Android for myself whenever I get the time, so I can stop playing Everwing on my phone and eating up all the data on my phone plan.
