---
fontsize: 12pt
geometry: "margin=1in"
fontfamily: "times"
linestretch: 1
---

# Final Project Proposal

## Goal

My goal will be train deep learning model that will be able to play the game **Minesweeper** effectively. 

## Approach

The general approach will be to implement a convolutional neural network in *PyTorch* which will take as input the entire **Minesweeper** board.

I think that it would be interesting to do two types of convolutional networks to see which is most effective. I will start with implementing the first type of network, and will implement the second if time permits.

  - The *first* of these would do something similar to UNet, in which the output of the network is the entire board with predictions about the locations of the mines in the board.

  - The *second* of these networks would do something similar to multi-class classification, in which the output is a single move to make in the board, out of the options of flagging a square, revealing one square, and revealing all squares (save flagged ones) around a square.

## Measure of Success

The measure of success would depend on the extent to which I can take the project in the allotted time.

  - Success at *first* will be measured in whether or not the bot can actually finish the game

  - Success will *further* be measured by looking at the number of moves required to finish a game, so as to optimize a bot that does fewer moves

## Available Resources

In the past, I coded up a version of **Minesweeper** with the express purpose to some day train a model to play it. I never actually started creating that model, but I have a working game that can be set up in order to provide game data to the model as it trains.

Apart from this, I don't really know that I will need other resources. My training and test data will come from my **Minesweeper** program and will be sufficient for its needs. I will need other resources in the form of information about how to set up a model to accomplish the goals that I want to, which I will obtain via research. 

# Final Project Dataset

- Since I am doing reinforcement learning, I will not really have a data set.
- Rather, I am going to use a program I have written to play Minesweeper in order to generate games for the model to play and from which to learn.
- There will not be any need for data cleaning, as the data will be generated new for each training.
