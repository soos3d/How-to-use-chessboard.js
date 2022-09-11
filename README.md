# Make a basic chess board with chessboard.js

## Introduction

This tutorial is the first in the series, and I will show you how to create a functioning chessboard using the [chessboard.js library]( https://github.com/oakmac/chessboardjs/).

Chess can be considered the eternal game; it has been around for hundreds of years and will be around for hundreds more. Learning how to code can be complex and intimidating; I love creating simple projects like this to help people start out. 

Learning by creating something you enjoy is the best way to learn!

### Create a chess game series

* Create an interactive chess board with `chessboard.js`. <----- You are here. 
* Integrate the `chess.js` API to make a functioning chess game. (Work in progress)

## Table of contents

  - [Introduction](#introduction)
    - [Create a chess game series](#create-a-chess-game-series)
  - [Objectives](#objectives)
  - [What is chessboard.js](#what-is-chessboardjs)
  - [Requirements](#requirements)
  - [Quick use](#quick-use)
  - [Create the project's folder](#create-the-projects-folder)
  - [How to use chessboard.js](#how-to-use-chessboardjs)
    - [Prepare chessboard.js](#prepare-chessboardjs)
    - [index.html](#indexhtml)
    - [Import the necessary libraries](#import-the-necessary-libraries)
    - [The HTML body](#the-html-body)
  - [Different board set ups](#different-board-set-ups)
    - [Customize pieces position](#customize-pieces-position)
      - [Use a FEN string](#use-a-fen-string)
      - [Use the position object](#use-the-position-object)
  - [Make an interactive chessboard](#make-an-interactive-chessboard)
  - [Customize the board style](#customize-the-board-style)
  - [Conclusion](#conclusion)

## Objectives

This tutorial will show you how to use the `chessboard.js` library to create an interactive chess board.

You will learn:

* How to set up the project.
* How to create a static board using the chessboard.js library.
* How to create an interactive board using the chessboard.js library.
* How to customize the board and pieces.

## What is chessboard.js

chessboard.js is a JavaScript library used to jumpstart your chess games. This library gives you the tools to build and populate a 2D chess board; note that `chessboard.js` does not take care of the chess rules, but it's only meant to give you a starting platform. It can be used for different use cases:

* Make a website to showcase moves and scenarios.
* Allow players to play against each other.
* Etc...

This library can integrate with the `chess.js` API to make a functional game. But for this tutorial, we will just see how to start and create a functioning chess board. 

## Requirements

> **Note:** The `chessboard.js` library will need a minor fix to render the chess pieces; I recommend cloning the repo directly, as the library you find here is ready to go!

* Node JS
    * [Install Node JS](https://nodejs.org/en/download/).
* The `chessboard.js` library.
    * [Download from the chessboard.js website](https://chessboardjs.com/index.html).
* Lite-server
    * Install by running the following command in a terminal.

```sh
npm install --global lite-server
```

These two packages will allow you to efficiently serve the webpage to see how it works in your browser. 

## Quick use

Clone this repo in your project's folder.

You will find the library ready to go in the `chessboardjs-1.0.0` folder.

```sh
git clone https://github.com/soos3d/Make-a-basic-chess-board-with-chessboard.js.git
```

From the main directory, run the following command to serve `index.html` and see it in your browser. 

```sh
lite-server
```

This repository holds different `index.html` files with all of the code examples, you will find them in the scenarios folder. The default file in the main folder is the interactive board.

You have two options to test the other files:

1. Copy the file you want to run from the scenarios folder, paste it into the main folder, rename it `index.html`, and then run `lite-server`. (Delete or rename the original `index.html`)

1. Copy the code from the file in the scenarios folder you wish to run, paste it inside `index.html` in the main folder, and then run `lite-server`.

## Create the project's folder

Now that you have the repo set up and you know how to run it, let's explain how all of this works!

The main folder of your project holds the files that we need:

* chessboardjs-1.0.0
    * This folder holds the library.
* `index.html`
    * The HTML page.

If you cloned the repo you'll have everything ready, but I'll explain you how to se it up from scratch. 

The first step is to create a directory where the project will live. Then you can download the [`chessboard.js` library from the website](https://chessboardjs.com/index.html), this is a `.zip` file, and you can extract it inside the project's folder. 

Then create an `html` file named `index.html`. 

The structure looks like this:

```sh
chessboard-project
                |__ chessboardjs-1.0.0
                |__ index.html
```
## How to use chessboard.js

### Prepare chessboard.js

In the intro, I mentioned that we need a minor fix to ensure the images render, so let's take care of that now!

Go into the chessboardjs-1.0.0 folder and find `chessboard-1.0.0.js` in `chessboardjs-1.0.0\js\chessboard-1.0.0.js`.

We need to ensure that the path to the images of the pieces folder is correct. 

open `chessboard-1.0.0.js` in your IDE and find the following piece of code on line `576`.

```js
// default piece theme is wikipedia
    if (!config.hasOwnProperty('pieceTheme') ||
        (!isString(config.pieceTheme) && !isFunction(config.pieceTheme))) {
      config.pieceTheme = 'img/chesspieces/wikipedia/{piece}.png' 
    }
```

The default path does not work, and we need to add the previous folder; simply add `/chessboardjs-1.0.0/` to the path like the following.

```js
config.pieceTheme = '/chessboardjs-1.0.0/img/chesspieces/wikipedia/{piece}.png'
```

Now the library can adequately retrieve the default images for the chess pieces.

### index.html

Let's start coding, and we can simply start from an `html` boilerplate. The title is what shows up in the browser tab, we can call it `My first chessboard`.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>My first chessboard</title>

</head>

<body>

</body>

</html>
```

This will serve as a base for our page. 

### Import the necessary libraries

Once we have our `index.html,` the first step is to import the libraries and files needed.

We'll need three imports:

* The JQuery library.
* The CSS stylesheet:
    * `chessboard-1.0.0.min.css`
* The chessboard JavaScript file:
    * `chessboard-1.0.0.js`

We can place the imports in the HTML's `<head>` section. So the head will look as follows:

```html
<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Interactive chessboard</title>
    
    <link rel="stylesheet" href="chessboardjs-1.0.0\css\chessboard-1.0.0.css">      <!-- Import the CSS file -->
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>                    <!-- Import the JQuery library -->
    <script src="chessboardjs-1.0.0\js\chessboard-1.0.0.js"></script>                   <!-- Import the chessboard.js -->

</head>
```

### The HTML body

Now we are ready to create a board! 

First, we'll start building an empty chessboard. This library makes it incredibly easy, with just two lines of code!

Create a `<div>` element where the board will be.

```html
<!-- Create a board, customize the size using the 'width' parameter -->
    <div id="board" style="width: 600px"></div>
```

The `id` tag is used to associate it with the JS code; then use the `width` tag to manage the size of the board.

Then it's time for the JavaScript code; in this case, we'll just place it in the HTML using a `<script>` tag, but you can put it in a separate file and import it in the head like we do the other ones.

We use the `Chessboard` keyword to create the board and associate it to a variable; by specifying only the `id`, we create an empty board. 

```html
 <!-- JavaScript and JQuery are used for the logic -->
    <script>

        // Create a board variable using the "Chessboard" keyword.
        var board = Chessboard('board')
        
    </script>
```

See how easy? Only two lines of code! At this point, the entire HTML file should look as follows.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Interactive chessboard</title>

    <link rel="stylesheet" href="chessboardjs-1.0.0\css\chessboard-1.0.0.css">
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
    <script src="chessboardjs-1.0.0\js\chessboard-1.0.0.js"></script>

</head>

<body>
    <!-- Create a board, customize the size using the 'width' parameter -->
    <div id="board" style="width: 600px"></div>

    <!-- JavaScript and JQuery are used for the logic -->
    <script>
        // Create a board variable using the "Chessboard" keyword.
        var board = Chessboard('board')
    </script>
</body>

</html>
```

You are now ready to see the result! First, run this command from the folder containing `index.html`.

```sh
lite-server
```

This will serve the page in your browser, and you will see an empty board.

![screely-1662913346017](https://user-images.githubusercontent.com/99700157/189538278-7ead0640-6f7a-4939-8ed0-909fdb170996.png)

Congratulations on making a chessboard!

> **Tip:** Keep the browser page open and the local server connection open; when you make changes to the HTML file, it will automatically update the browser page.


## Different board set ups

Now that you have seen how to create a board, we can explore how to show pieces on it, and it is just as simple. We must add a second parameter to the `board` variable.

The first we'll see is a board with the pieces in the starting position; we simply add `"start"` as the second parameter.

```js
var board = Chessboard("board", "start")
```

If you closed the previous page, restart the service using `lite-server` and you will see the board ready to go!

> Note that this board is not interactive yet, is only for display.

![screely-1662913425235](https://user-images.githubusercontent.com/99700157/189538349-b4947a23-2d8b-49fc-b988-ac891b618b32.png)

### Customize pieces position

We can display a board with the pieces in the starting position with the previous command, but what if we want to show them in different configurations? 

chessboard.js gives a few options. 

#### Use a FEN string

A [FEN string](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation) is a chess standard to define a board configuration; chessboard.js allows us to pass it as the second parameter to display it. To generate the string, you can use a [FEN generator](https://www.dailychess.com/chess/chess-fen-viewer.php). 

A FEN string looks like this `rn1qkn1r/pppb1ppp/4p3/1b1p4/3P4/4PQ2/PPP2PPP/RNB1KBNR`, usually FEN generators give extra information, but we can ignore that for now and just take the positions string. 

Let's use a FEN string as an example and pass it as the second parameter of the `board` variable.

```js
// Create a board variable using the "Chessboard" keyword.
var board = Chessboard("board", "8/5q2/3k4/1R6/3PK3/8/8/8")
```

This will be the result:

![screely-1662913502903](https://user-images.githubusercontent.com/99700157/189538403-f1990add-5163-49dd-8731-de9b1be09ee6.png)

#### Use the position object

The second way we have is to specify the position of each piece by passing an object as the second parameter.

```js
 // Set up pieces configuration 
 // Find the pieces name in chessboardjs-1.0.0\img\chesspieces\wikipedia
 const configuration = {
     position: {
         d4: 'wP',      // Assign the position by specifing a <square : 'piece-name'> 
         d6: 'bK',
         f7: 'bQ',
         e4: 'wK',
         b5: 'wR',
     }
 }

 // Create a board variable using the "Chessboard" keyword.
 const board = Chessboard("board", configuration)
```

Find more about the position object in the [chessboard.js docs](https://chessboardjs.com/docs.html#config:position).

This set up is the same as the FEN set up.

Now you know how to use chessboard.js to create a static board and populate it how you want!

## Make an interactive chessboard

Now that you got the basics let's add some interaction! 

We can create an interactive board where we can move the pieces by dragging them, and it's just as easy.

In this case, we'll add buttons to set up and clear the board using JQuery commands.

Let's start with the HTML, we'll create a board just like before in a `<div>` tag, but this time we'll add two buttons, one to set up the board in the starting position and one to clear it. 

Inside the HTML body place:

```html
 <!-- Create a board, customize the size using the 'width' parameter -->
    <div id="board" style="width: 600px"></div>
   
    <!-- Button elements to interact with the board --> 
    <button id="startBtn">Start Positions</button>      <!-- The id tag allows the JQuery code to be executed when pressing the button. --> 
    <button id="clearBtn">Clear Board</button>
```

Then let's update the code inside the `<script>` tag.

```js
// Create a board variable using the "Chessboard" keyword.
var board = Chessboard('board', {       // This object specifies the level of interaction.
    draggable: true,                    // Make the pieces draggable.
    dropOffBoard: 'trash',              // Remove pieces by draggin them off the board.
    sparePieces: true                   // Show pieces outside the board and allow to drag them onto the board.
})

// Commands executed by the buttons.
$('#startBtn').on('click', board.start)     // Set up the pieces in the starting position.
$('#clearBtn').on('click', board.clear)     // Clear the board.
```

![screely-1662913605829](https://user-images.githubusercontent.com/99700157/189538469-15d8f2e5-169b-4d74-910c-7b6a4700df44.png)

And now you have an interactive board! You could even use it to play locally with a friend, but remember that this board has no idea about the rules; we'll see that part in the following tutorial. 

The full HTML looks like this for the interactive board.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Interactive chessboard</title>
    
    <link rel="stylesheet" href="chessboardjs-1.0.0\css\chessboard-1.0.0.css">
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
    <script src="chessboardjs-1.0.0\js\chessboard-1.0.0.js"></script>

</head>

<body>
    <!-- Create a board, customize the size using the 'width' parameter -->
    <div id="board" style="width: 600px"></div>

    <!-- Button elements to interact with the board -->
    <button id="startBtn">Start Positions</button>
    <button id="clearBtn">Clear Board</button>

    <!-- JavaScript and JQuery are used for the logic -->
    <script>
        // Create a board variable using the "Chessboard" keyword.
        var board = Chessboard('board', {           // This object specifies the level of interaction.
            draggable: true,                        // Make the pieces draggable.
            dropOffBoard: 'trash',                  // Remove pieces by draggin them off the board.
            sparePieces: true                       // Show pieces outside the board and allow to drag them onto the board.
        })

        // Commands executed by the buttons.
        $('#startBtn').on('click', board.start)     // Set up the pieces in the starting position.
        $('#clearBtn').on('click', board.clear)     // Clear the board.
    </script>
</body>

</html>
```

## Customize the board style

Now let's play with colors! from `chessboard-1.0.0.css` we can customize how our board looks! 

You can find the file in `\chessboardjs-1.0.0\css\chessboard-1.0.0.css`.

The CSS stylesheet is relatively simple, and we can just change the colors there!

This is what the default file looks like; you can replace the colors pointed out by the comments. You can use a [CSS colors generator](https://www.w3schools.com/colors/colors_picker.asp) to find the right one!

```css
/*! chessboard.js v1.0.0 | (c) 2019 Chris Oakman | MIT License chessboardjs.com/license */

.clearfix-7da63 {
  clear: both;
}

.board-b72b1 {
  border: 2px solid #404040;       /* Outside border of the board, you can change the style and color */
  box-sizing: content-box;
}

.square-55d63 {
  float: left;
  position: relative;

  /* disable any native browser highlighting */
  -webkit-touch-callout: none;
    -webkit-user-select: none;
     -khtml-user-select: none;
       -moz-user-select: none;
        -ms-user-select: none;
            user-select: none;
}

.white-1e1d7 {
  background-color: #f0d9b5;    /* Background of the white side tiles */
  color: #b58863;               /* color of the letter identifing the files (columns) */
}

.black-3c85d {
  background-color: #b58863;    /* Background of the black side tiles */
  color: #f0d9b5;               /* color of the letter identifing the ranks (rows) */
}

.highlight1-32417, .highlight2-9c5d2 {
  box-shadow: inset 0 0 3px 3px yellow;
}

.notation-322f9 {
  cursor: default;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 14px;
  position: absolute;
}

.alpha-d2270 {
  bottom: 1px;
  right: 3px;
}

.numeric-fc462 {
  top: 2px;
  left: 2px;
}
```

Once you save it the changes take place.

![screely-1662913665218](https://user-images.githubusercontent.com/99700157/189538519-f7c7eecd-dfd6-46b1-8506-0c1f11f706b6.png)

Then we can customize the pieces simply but having new `.png` files inside `/chessboardjs-1.0.0/img/chesspieces/wikipedia/`, or by creating a new folder and then redirecting the path inside `chessboard-1.0.0.js` like we did in the beginning. 

> The images need to be 80 x 80 pixels. 

```js
// default piece theme is wikipedia
    if (!config.hasOwnProperty('pieceTheme') ||
        (!isString(config.pieceTheme) && !isFunction(config.pieceTheme))) {
      config.pieceTheme = 'img/chesspieces/NEW_FOLDER/{piece}.png' 
    }
```

![screely-1662913670851](https://user-images.githubusercontent.com/99700157/189538523-52e71b87-66e8-400e-9a89-781477982d23.png)

## Conclusion

Great job getting through all of this! Now you are ready to start creating your own chess scenarios!

Thanks for reading!
