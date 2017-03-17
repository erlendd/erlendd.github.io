---
title: "Predicting the price of Magic: The Gathering cards after they are reprinted"
layout: post
comments: true
date: 2017-03-16 17:00
headerImage: false
published: true
tag:
- rnn
- lstm
- keras
- recurrent neural network
- machine learning
description: Using a recurrent neural network to forecast the price-drop (or draw-down) of Magic The Gathering cards when they are reprinted.
---

## Magic: The Gathering

In case you haven't heard of it before, Magic: The Gathering (Magic or MTG for short) is a trading card game 
developed by Wizards of the Coast. As card games go it's pretty complicated, but the jist is that you and 
your opponent take turns to wittle each others' life down from 20 to 0.
It's interesting for a few reasons: you typically build your own deck based 
around some strategy, and so you need to think about the probabilities of drawing certain cards 
in a game (there are also cards that exist purely to manipulate the probability of drawing a certain card). 
Typically your deck may contain 60+ cards, with a maximum of 4 copies of any one card 
(except for basic land cards, which are unlimited). To increase the chances of drawing key cards during 
play it's most common to have exactly 60 cards and run 4 copies of important cards.

The cards enter circulation via booster packs, which are a sealed back of 15 randomly selected cards 
consisting of 1 rare , 3 uncommons and 11 common cards. Sometimes the rare is replaced with a mythic rare, 
and in every booster pack one of the cards is printed on shiny foil rather than paper.
Remarkably this has led to a very large secondary market where people buy and sell the individual cards
on ebay.com and tcgplayer.com), and there are websites such as mtgstocks.com to track the prices over time. 

## Supply and demand, of Magic cards

Like most markets, the price of Magic cards on the secondary market is driven by two factors: supply and demand.
If a card is rare it's printed less, and so supply is low. If a card is "good" then lots of people want it, 
and so demand is high. Here, good means that either the artwork is nice or the card does something amazing in play.
Wizards of the Coast don't just continually print off cards though: they are printed as part of a set, and new sets
are released every few months. 
Old cards (those from old sets that are "out of print") are often worth more, and their slow rise in value over time 
can probably be attributed to an a gradual increase in the number of MTG players.
Each time Wizards release a new set, they include reprints of older cards and so the price of those cards
falls as you'd expect. 

This makes for a pretty cool time-series forecasting problem under the influence of external stimuli. 
Most of the examples I've seen online of time-series forecasting are **autoregressive models**, where 
predictions are made using historical values. Here I'm going to use a neural network to demonostrate how
one could try to predict the expected draw-down in the value of a Magic card after its reprinted.
Instead of doing this for the real prices of Magic cards I'll generate some data that looks a lot like 
actual price data, and see if the neural network is able to model the mechanics.

## Recurrent neural network for Time-series

Neural networks are in the news a lot lately due to the huge amount of progress made on deep-learning in 
the last decade. Here I'll use a type of recurrent neural network called an LSTM network 
(LSTM stands for long short term memory) to predict the next future price 
