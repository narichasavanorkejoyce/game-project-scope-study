# Game Project Scope Study

## Required Readings

-   [Game Project](https://github.com/ga-wdi-boston/game-project)
-   [Game API](https://github.com/ga-wdi-boston/game-project-api)
-   [What is a User Story](https://www.mountaingoatsoftware.com/agile/user-stories)

## Deliverables

After reading the `game-project` prompt and the `game-project-api` documentation
please do the following and be prepared to share and discuss during our next
class.

Submit detailed answers to the following in this file via a pull request:

-   A wireframe of what your game project will look like.
![Imgur](http://i.imgur.com/xcEdk7V.jpg)

-   The data structure you plan to use.

The DOM (Document Object Model) is a kind of data structure. Here's the DOM hierarchy of my preliminary HTML code:

![Imgur](http://i.imgur.com/dNsojpa.jpg)

In addition, here is a draft of my game board HTML code:

```html
<html>
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="main.css"/>
    <title>Tic Tac Toe</title>
  </head>
  <body>
  <div class = "scoreboard">X SCORE</div>
  <div class = "scoreboard">O SCORE</div>
  <button class = "logout" id = "log-out" type="submit">LOGOUT</button>
  <table class = "game-board">
    <tr class = "row-1">
      <td class = "rows" id = "slot-1">1</td>
      <td class = "rows" id = "slot-2">2</td>
      <td class = "rows" id = "slot-3">3</td>
    </tr>
    <tr class = "row-2">
      <td class = "rows" id = "slot-4">4</td>
      <td class = "rows" id = "slot-5">5</td>
      <td class = "rows" id = "slot-6">6</td>
    </tr>
    <tr class = "row-3">
      <td class = "rows" id = "slot-7">7</td>
      <td class = "rows" id = "slot-8">8</td>
      <td class = "rows" id = "slot-9">9</td>
    </tr>
  </table>
  <button class = "reset" type="submit">RESET GAME</button>
  </body>
</html>
<script type="text/javascript" src="gameLogic.js"></script>
```
In addition, I will need to capture a lot of data on the log-in page. If a person does not have an account, I'll use a `POST AJAX` request to create a sign-up feature. This sign-up feature will store a USER object containing the person's email and unique ID. Then, I'll use another `POST AJAX` request to create a sign-in feature that calls the ID from the stored USER object.

I'll use a `DELETE AJAX` request to delete the user's token. This will allow them to sign out of the game by clicking the log-out button. Finally, I'll use a `PATCH AJAX` request to create a change password feature.

-   How you will take the markup of the game board and represent it in JS

I'll need to write two main Javascript functions in order to create a tic-tac-toe game.

First, I need a function that can fill in the table slots with either an 'X' or an 'O'. I'll create an object that counts the number of moves in the game. The initial value of that counter will be zero.

If we're on an even-numbered move, then I'd like to select that HTML td element and fill it in with the value 'O'. If we're on an odd-numbered move, I'd like to fill that td element in with the value 'X'.

The function will need to add 1 to the number of moves after each iteration. The loop should run 8 times, since this is a 3x3 Tic Tac Toe board.

Here's a draft of what that Javascript code might look like:

```javascript
$(document).ready(function () {
  // Create a variable that counts the number of moves
  // Let the initial value of that variable be zero
  let numMoves = 0

  // Select slots in the game board
  for (let numMoves = 0; numMoves < 9; numMoves++){
    $('.game-board').find('td').on('click', function () {
    // If we're on an even number of moves, place down '0'
      if (numMoves % 2 === 0) {
      // Fill in slot with 'O'
        $('this').text('O')
      // Check whether this move resulted in a winning combo
        checkWin('O')
      // IF we're on an odd number of moves, place down 'X'
      } else if (numMoves % 2 !== 0) {
      // Fill in slot with 'X'
        $('this').text('X')
      // Check whether this move resulted in a winning combo
        checkWin('X')
      }
    }
  }
})
```
As you can see above, I'm referencing a function called `checkWin()` that has yet to be defined. I'll need a function that checks after each loop whether or not one of the players has won. This function will mainly be composed of `if` statements, and will check to see if any of the 8 winning combinations has been satisfied.

Here is a draft of those `if` statements:

```javascript
const checkWin = function (slotValue) {
  if ($('.gameboard').find('#slot-1').val() !== '' &&
      $('.gameboard').find('#slot-1').val() === $('.gameboard').find('#slot-2').val() &&
      $('.gameboard').find('#slot-1').val() === $('.gameboard').find('#slot-3').val()) {
        console.log ('You found a match!')
      }
      if ($('.gameboard').find('#slot-1').val() !== '' &&
          $('.gameboard').find('#slot-1').val() === $('.gameboard').find('#slot-4').val() &&
          $('.gameboard').find('#slot-1').val() === $('.gameboard').find('#slot-7').val()) {
            console.log ('You found a match!')
          }
          if ($('.gameboard').find('#slot-1').val() !== '' &&
              $('.gameboard').find('#slot-1').val() === $('.gameboard').find('#slot-5').val() &&
              $('.gameboard').find('#slot-1').val() === $('.gameboard').find('#slot-9').val()) {
                console.log ('You found a match!')
              }
              if ($('.gameboard').find('#slot-3').val() !== '' &&
                  $('.gameboard').find('#slot-3').val() === $('.gameboard').find('#slot-5').val() &&
                  $('.gameboard').find('#slot-3').val() === $('.gameboard').find('#slot-7').val()) {
                    console.log ('You found a match!')
                  }
                  if ($('.gameboard').find('#slot-2').val() !== '' &&
                      $('.gameboard').find('#slot-2').val() === $('.gameboard').find('#slot-5').val() &&
                      $('.gameboard').find('#slot-2').val() === $('.gameboard').find('#slot-8').val()) {
                        console.log ('You found a match!')
                      }
                      if ($('.gameboard').find('#slot-3').val() !== '' &&
                          $('.gameboard').find('#slot-3').val() === $('.gameboard').find('#slot-6').val() &&
                          $('.gameboard').find('#slot-3').val() === $('.gameboard').find('#slot-9').val()) {
                            console.log ('You found a match!')
                          }
                          if ($('.gameboard').find('#slot-7').val() !== '' &&
                              $('.gameboard').find('#slot-7').val() === $('.gameboard').find('#slot-8').val() &&
                              $('.gameboard').find('#slot-7').val() === $('.gameboard').find('#slot-9').val()) {
                                console.log ('You found a match!')
                              }
                              if ($('.gameboard').find('#slot-4').val() !== '' &&
                                  $('.gameboard').find('#slot-4').val() === $('.gameboard').find('#slot-5').val() &&
                                  $('.gameboard').find('#slot-4').val() === $('.gameboard').find('#slot-6').val()) {
                                    console.log ('You found a match!')
                                  }
}
```
If any of these conditions have been met, the board should display that there is a winner! The board should clear and the scoreboard should register that win. If one of these winning combinations has not been met, then the game should keep going.

-   How you plan to approach this project.

I will try to be as methodical as possible. I will try to break the project down into bite-sized chunks, and focus my attention on the problem that is right in front of me.

-   4-8 user stories for your game project.

  1. As a tic-tac-toe beginner, I want to learn about this game through your web application.
  2. As a moderately experienced tic-tac-toe player, I want to play this game on a simple, easy-to-understand, fun interface.
  3. As two friends hoping to play tic-tac-toe, we want to play this game, compete, and have fun!
  4. As a user, I want to experience no confusion while navigating through this web application.
  5. As a user, I want to have a seamless web experience with little-to-no lag time.


-   How you plan to keep your code modular.

Here is the plan for my directory and file structure:

- project-repo
  - index.html
  - styles
    - main.css
  - scripts
    - gameLogic.js
    - index.js
    - events.js
    - api.js
    - ui.js

By applying separation of concerns, I hope to keep my code modular.

-   What creative spin will you add to your project?

I hope that my UI will be clean and minimalistic. I'd also like to have a line draw through a winning combination to indicate that the game is over.

-   How will you use version control to backup / track your project?

I plan to commit after every major change. If I write "and" in a commit message, I'll know that I should have committed sooner. I will write commit messages with details about the change (what, why, how).

-   Do you plan to attempt any of the bonuses?

I'm going to focus on the requirements first, but I'll attempt some of the bonuses, time permiting.

You may want to submit pictures for your wireframes and/or user stories.
[Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
has instructions to link to a picture you've uploaded to a service like [Imgur](http://imgur.com/).
