---
title: "Modelling Bitcoin / Ethereum prices using Metcalfe's / Zipf's law"
layout: post
comments: true
date: 2018-02-09 14:50
headerImage: false
published: true
tag:
- finance
- cryptocurrencies
- maths
- bitcoin
- ethereum
- metcalfe's law
- zipf's law
description: A look at how well Metcalfe's law and Zipf's law model the price of both Bitcoin and Ethereum.
---

## Metcalfe's law

Metcalfe's law is the mathematical encoding of an intuitive idea: the value of a network increases as the number of users in that network increases [1].
The basic idea consists of counting the number of links between nodes in a network as an estimate for the total value of that network. 
For a network with \\(N\\) nodes that can each communicate with \\(N - 1\\) other nodes, this gives a total number of links \\(N(N-1).\\)
If we divide by two to avoid double-counting  we can Metcalfe's law for the total value \\(V(N)\\) of the network,

$$ V(N) = \alpha \, \frac{N(N-1)}{2}  $$

Note that each node in the network adds the same value, and a network with one node has a value of zero. The \\(\alpha\\) prefactor is 
simply empirically chosen, and is essentially the average value each link brings to the network.

Metcalfe's law was originally devised as a way of valuing physical telephony and computer networks. The cost of the network

There are some shortcomings with Metcalfe's law. In particular the prefactor \\(\alpha\\) is constant for all values of \\(N\\), which assumes that 
new nodes increase the value of the network just as much as far older nodes. 
For this reason a few alternatives have been suggested, including Zipf's law for large networks [2].

Metcalfe's law was originally used to determine the size at which physical (telephony or ethernet) networks become cost effective. 
The cost of a network can be written as \\(c_r + c_N N\\), where \\(c_r\\) is the cost of the router (or infrastrature cost) and 
\\(c_N\\) is the cost of each node. 
Since the cost of a network increases with \\(O(N)\\ and the )
value of that network increases with \\(O(N^2)\\), larger networks are typically more cost effective.
This idea become a huge marketing tool for the early network dotcom companies.

Some argume that there are some shortcomings with Metcalfe's law [2].
In particular the prefactor \\(\alpha\\) is constant for all values of \\(N\\), which assumes that 
new nodes increase the value of the network just as much as far older nodes.
Furthermore the \\(O(N^2)\\) value growth is clearly unsustainable in as \\(N \rightarrow \infty\\).
For this reason a few alternatives have been suggested, the most popular being Zipf's law for large networks.
>>>>>>> Stashed changes

## Zipf's law

Zipf's law is an empirical model for describing unequal resource distribution, first observed in written language by examining 
the frequency with which words appear in text. The most frequent word appears twice as much as the second most frequent word, and three times
as much as the third most common word and so on.


## References

\[1\]: Metcalfe's law: A network becomes more valuable as it reaches more users, Infoworld, 1995.

\[2\]: Odlyzko, A. & B. Tilly (2005) A refutation of Metcalfe’s Law and a better estimate for the value of
networks and network interconnections - [Link](http://www.dtc.umn.edu/publications/reports/2005_16.pdf).

