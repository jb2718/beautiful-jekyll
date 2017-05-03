---
layout: post
title: It’s Hammer Time!
subtitle: (Uno Part 1)
---

 It’s Hammer Time! (Uno Part 1)

I’m working on getting into the habit of building things on a regular basis. One goal of this blog is simply to share what I learn along the way. Hopefully something here will be helpful to someone else out there building away. Alright, enough intro…let’s get to work!

hammer.jpg()
<img src="../img/blog_images/hammer_time/hammer.jpg" width="650px">

The first project I would like to work on is making an Uno computer game using the Ruby programming language. I used to love Uno so much as a kid! Maybe it was the bright colors and minimalist design of the cards. Or perhaps it was the joy of slapping a Draw Four down on the table. Most likely, it was because the rules were simple enough to understand at age four or five - and it was always a blast to get the whole family playing a game together.

I am currently working through an excellent online program called Launch School to improve my programming skills. Since I am going through the object oriented lessons now, I would like to practice by using object oriented design to make my Uno computer game.

In order to to break this project down into an object oriented design, I will need to go through a couple of steps. To start, I’ll come up with a description of the game. Then from that description, I want to go through and pull out a rough sketch of classes and methods. Here is a description of the game. I’ve simplified some aspects of the game at this stage:
 
Description

    Uno is a game for two players where players start with seven cards each and try to get rid of their cards first

    A player can get rid of cards in two ways:
        Match the color, number, or symbol of the top discard card
        Use a wild card

    Cards are added to a player’s hand in a couple of ways:
        A player must pull one card from the deck if she has no matches to the top discard card at the start of her turn OR if she chooses not to play any of the cards she has
        A player must pull however many cards she is commanded to pull from the deck if the top card on the discard pile at the start of her turn commands her to add cards to her hand
        Once a player gets down to one card in her hand, she must call out “Uno!” If her opponent calls “No Uno!” before she calls “Uno!,” she must draw two cards from the deck. If an opponent calls “No Uno!” prematurely, the opponent must draw two cards from the deck.

    Aside from adding and discarding cards to players’ hands, there is one more thing to consider - the game flow. There are special cards that allow players to alter the flow of the game:
        Skip: skips an opponent’s turn
        Reverse: reverses the flow of turns
        Wild: changes the color to match on the discard pile

 
Rough Sketch of Classes and Methods

Here is a rough sketch of classes and methods for the Uno game based on the description from above.

class Game
  def initialize
  end

  def start
  end

  def deal
  end
end

class Player
  def initialize
  end

  def pull_card
  end

  def play_card
  end

  def choose
  end
end

class Card

  def initialize
  end

  def match?(other_card)
  end

end

class Hand
end

class Turn
end

class Match
end

class Deck
end

class Flow
  def initialize
  end

  def skip
  end

  def reverse
  end

  def change_color
  end
end

 
Going from the Description to Classes and Methods

There was an intermediate step I took before coming up with that rough sketch of classes and methods written in Ruby. First, I tried to pull out all of the important object-like entities from the description and write those down. One way to think about that is to look for a person, place, or thing…in other words, a noun

Here are the objects/nouns I came up with from my description:
Objects 	
Game 	
Player 	
Card 	
Hand 	
Turn 	
Match 	
Deck 	
Flow 	

Now let’s get this thing in action and start looking for behaviors and what’s happening….in other words verbs.

verb.png
Objects 	Actions
Game 	start, deal cards (this is implicit in ‘players start with 7 cards’)
Player 	add card/pull card, get rid of card, choose
Card 	match card
Hand 	
Turn 	
Match 	
Deck 	
Flow 	alter flow, skip, reverse, change color

Dangling Action: command
 
A Couple of Notes

There are a couple of things I would like to mention. As you can see, we have an action (“command”) that does not seem to group easily with any of the objects we pulled out. We will just put it to the side for now. This is a loose process at this stage, so it is okay if not everything fits neatly into a category.

The other issue I would like to touch on briefly is related to the card object/noun. Based on our description, there are some additional nouns and adjectives associated with that entity. What do we do with the notions of colors, numbers, and symbols? These are nouns, so why didn’t I put them in my list. My sense is that we will have a scenario in which color, number, and symbol are attributes of a card.

So essentially those nouns are part of the card class. How about the discard card or the wild card that were mentioned in the description? So “discard” and “wild” would be adjectives describing the “card” object/noun. I think these may end up being types of cards. So it may be that we end up creating sub-classes for those…or not. I am not 100% sure at this stage, and that is okay.

It’s important to remember to stay loose at this stage and not get too hung up on details. This sketch will surely change as we move forward in building the game. We are just getting a sense for what we will be working with for this particular project.

That is all for this episode of building the Uno game. On the next post for this project, I’ll start defining some of those classes and methods we listed in our sketch as well as additional ones we may need. I will also explore a way to keep myself organized in the process of testing the code over and over again to see if what I just wrote works as I hoped it would.