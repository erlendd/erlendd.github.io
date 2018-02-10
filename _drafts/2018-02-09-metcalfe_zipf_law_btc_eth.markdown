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



There are some shortcomings with Metcalfe's law. In particular the prefactor \\(\alpha\\) is constant for all values of \\(N\\), which assumes that 
new nodes increase the value of the network just as much as far older nodes. 
For this reason a few alternatives have been suggested, including Zipf's law for large networks [2].

## Zipf's law



## References

\[1\]: Metcalfe's law: A network becomes more valuable as it reaches more users, Infoworld, 1995.

\[2\]: Odlyzko, A. & B. Tilly (2005) A refutation of Metcalfe’s Law and a better estimate for the value of
networks and network interconnections - [Link](http://www.dtc.umn.edu/publications/reports/2005_16.pdf).

