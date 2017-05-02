---
layout: post
title: Pulling Back Complexity to Push Forward - Part I
subtitle: The Simplification Problem Solving Strategy
---

Ideas seem to pop up all of the time!  They appear while I blend my morning smoothie or after I listen to a great podcast.  They spring forth effortlessly and with all the effervescence of this little cartoon piece of toast. 

![Toast pops out of toaster](https://media.giphy.com/media/l3q2Ty3RWark8VgIw/giphy.gif)

Ideas especially tend to appear while I am in the midst of building another project.  For example, one of the projects I have worked on is coding a [console game similar to Blackjack](https://github.com/jb2718/ls-backend/tree/master/120/120_5/oo_twenty_one).  After completing that project, an idea popped into my mind: "Wouldn't it be cool to make a more complicated card game like Uno?  I love Uno!"  

That is usually how it starts: “Wouldn’t it be cool if….”  It is quite easy to generate "wouldn't it be cool if..." ideas.  However, making those ideas happen is not always so effortless.  I have gone through several starts and stops on this Uno project.  I have planned out my work, drawn up class responsibility collaborator diagrams, started coding, and run into walls.  I have balled up the proverbial sheet of paper, tossed it, and started over only to code myself into tangles of class responsibility.  

Hmmm.  Perhaps I need to take a step back and try another strategy.  Instead of trying to contemplate a fully complete game of Uno with all of its regulations and card variations, what if I attempt to make the project smaller?


## Stripping Back Complexity

So what do I mean by “making the project smaller”?  I mean I am going to start stripping back the complexity.  For example, according to Wikipedia, Uno is a game that can be played with 2 to 10 players.  It has 108 cards comprised of digit cards from 0 to 9 of various colors and 5 types of action cards.  Before going any further into the instructions, there are already many ways I can simplify the game.  I can restrict the number of players and reduce the types of cards allowed.  The idea is to keep reducing the complexity of the project until a clearer plan for how to handle the problem comes into focus.  Subsequently, I will gradually re-introduce those layers of complexity until I build back up to the full game.

During the first several iterations of trying to construct this game, I started by trying to break out methods and data from the the rules of the Uno game.  This time, I will try to simplify the rules first.  I want to make the game extremely simple so knowing how to proceed from step to step will be clearer.  I am certain this process would differ from person to person; nevertheless, it will be helpful to me to document this process, and I hope others find it useful as well.


## Getting Started

At its core, this game is going to involve interaction between a user and the application.  I will only worry about what it would look like for one user to interact with a program right now.  I'm imagining some kind of interface that looks like this:

##### basic intro interface
```ruby
# => Welcome to the Uno Game!
# => What is your name?
# User1

# => Hello, User1!
```

So code-wise, I might have something like the following:

##### main.rb
```ruby
def prompt(msg)
 puts "=> #{msg}"
end


prompt 'Welcome to Uno!'
prompt 'What is your name?'
user_name = gets.chomp

prompt "Hello, #{user_name}!"

```

Ok, this is pretty straightforward.  The next step I want to tackle is thinking about the idea of how the user selects cards.  I will not worry about the 108 different cards that are part of a full Uno game.  Instead, I am going to reduce the deck of 108 cards with different colors and action types down to a simple collection of 10 numbers from 0 to 9.  So our deck in this simplified version of the game has neither colors, nor action cards.  It also contains only 10 digit cards total instead of 76 digit cards as is the case in the full game.

##### basic card selection interface
```ruby
# => Type 1 to pick a card from the deck  2
# => That is an invalid selection...please try again
# => Type 1 to pick a card from the deck  1
# => Your card is: 3
```

##### main.rb
```ruby
# previous code omitted here for brevity...

def valid_card_selection?(choice)
  return true if choice == 1
  false
end

def pull_card
  rand(10)
end

# ...code omitted here for brevity

loop do 
  prompt "Type 1 to pick a card from the deck"
  response = gets.chomp
  
  break if valid_card_selection?(response.to_i)
  prompt "That is an invalid selection...please try again!"
end

user_card = pull_card

prompt "Your card is: #{user_card}"

```

As you can see I started adding in a little bit of input validation.  So now our user can select one card.  But wait...the user's "selection" of a card does not lead to a reduction in the total number of cards available!  This is true, however, I am going to suppress that requirement for now.  I want to add in one more piece of functionality to this simple thumbnail of my program before beginning to add in the first layer of complexity.  What I want to do now is create a basic game loop, so the user can replay the game as many times as desired.

##### main.rb
```ruby
# previous code omitted here for brevity...

def play_again?(choice)
  case choice.downcase
  when 'y','yes'
    true
  else
    false
  end
end

# ...code omitted here for brevity

loop do 
  prompt "Hello, #{user_name}!"
  
  loop do 
    prompt "Type 1 to pick a card from the deck"
    response = gets.chomp
    
    break if valid_card_selection?(response.to_i)
    prompt "That is an invalid selection...please try again!"
  end
  
  user_card = pull_card
  
  prompt "Your card is: #{user_card}"
  
  prompt "Would you like to play again? [y]es [n]o"
  response = gets.chomp
  
  break unless play_again?(response)
end

prompt "Thank you for playing Uno, #{user_name}!  Goodbye!!"


```


## Adding the First Layer of Complexity

Currently I have a very simple project core.  It has one user interacting with the “game” in a loop.  Each step forward at this level was clear for me.  From here, I want to add the first layer of complexity.  I will start by adding another player.  The second player will be a computer player, so its functionality will be similar to the first user, yet different at the same time. 

##### main.rb
```ruby
# previous code omitted here for brevity...

prompt 'Welcome to Uno!'
prompt 'What is your name?'
user_name = gets.chomp
computer_name = "Computer"

loop do 
  prompt "Hello, #{user_name}!"
  
  loop do 
    prompt "Type 1 to pick a card from the deck"
    response = gets.chomp
    
    break if valid_card_selection?(response.to_i)
    prompt "That is an invalid selection...please try again!"
  end
  
  user_card = pull_card
  computer_card = pull_card
  
  prompt "#{user_name}'s card is: #{user_card}"
  prompt "#{computer_name}'s card is: #{computer_card}"
  
  prompt "Would you like to play again? [y]es [n]o"
  response = gets.chomp
  
  break unless play_again?(response)
end

prompt "Thank you for playing Uno, #{user_name}!  Goodbye!!"

```

I added a line to set up the computer player's name, and then had the computer player select a card.  This functionality is pretty similar to that of the human user.  The code for the human and computer players will surely be a candidate for consolidation into classes at a later point.

Now that I have two players in the system, I want to plant a seed for the inter-player competition.  At this stage, the basic competition between players will be expressed as a simple comparison of the value of the cards each player selected.


```ruby
# ...code omitted here for brevity

def board_manager_find_result(user_val, cpu_val)
  case
  when user_val > cpu_val
    :human_user
  when user_val < cpu_val
    :cpu_user
  else
    :tie
  end
end

def show_game_result(result_str)
  case result_str
  when :human_user
    puts "You won!"
  when :cpu_user
    puts "Sorry, the computer won!"
  else
    puts "This is a tie!"
  end  
end

# ...code omitted here for brevity
  
  user_card = pull_card
  computer_card = pull_card
  
  prompt "#{user_name}'s card is: #{user_card}"
  prompt "#{computer_name}'s card is: #{computer_card}"
  
  game_result = board_manager_find_result(user_card, computer_card)
  show_game_result(game_result)
# ...code omitted here for brevity

```