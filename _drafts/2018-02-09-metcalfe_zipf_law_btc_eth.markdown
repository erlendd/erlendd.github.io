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

Metcalfe's law was originally devised as a way of valuing physical mtelephony and computer networks. the cost of the network

there are some shortcomings with metcalfe's law. in particular the prefactor \\(\alpha\\) is constant for all values of \\(n\\), which assumes that 
new nodes increase the value of the network just as much as far older nodes. 
for this reason a few alternatives have been suggested, including zipf's law for large networks [2].

metcalfe's law was originally used to determine the size at which physical (telephony or ethernet) networks become cost effective. 
the cost of a network can be written as \\(c_r + c_n n\\), where \\(c_r\\) is the cost of the router (or infrastrature cost) and 
\\(c_n\\) is the cost of each node. 
since the cost of a network increases with \\(o(n)\\ and the )
value of that network increases with \\(o(n^2)\\), larger networks are typically more cost effective.
this idea became a huge marketing tool for the early network dotcom companies.

<div class="imgcap">
<img src="/assets/images/bitcoin_metcalfes_law/metcalfes_law.png" >
cross-over of network value and network cost with increasing number of nodes.
taken from: [metcalfe's law after 40 years of ethernet](http://ieeexplore.ieee.org/document/6636305/).
</div>

some people argue that there are significant shortcomings with metcalfe's law [2].
in particular the prefactor \\(\alpha\\) is constant for all values of \\(n\\), which assumes that 
new nodes increase the value of the network just as much as far older nodes.
furthermore the \\(o(n^2)\\) value growth is clearly unsustainable in as \\(n \rightarrow \infty\\).
for this reason a few alternatives have been suggested, the most popular being zipf's law for large networks.

## zipf's law

zipf's law is an empirical model for describing unequal resource distribution, first observed in written language by examining 
the frequency with which words appear in text. the most frequent word appears twice as much as the second most frequent word, and three times
as much as the third most common word and so on. 

to see how zipf's law can be applied to our valuation problem, consider a network where the participants utilise the network 
at frequencies proportional to their rank in the network: i.e. the \\(k^{th}\\) user uses the network \\(1/k\\) times 
(relative to the other network participants). for large \\(n\\) the sum of these terms approaches \\(n\,log(n)\\). 

it has recently been suggested that zip's law is a superior to metcalfe's law for valuing networks, 
because it accounts for the fact not all users contribute equally [2]. this idea is refuted by metcalfe, as he points out 
zip's law has the same "explosive growth" potential (increases towards infinity with large \\(n\\)).

## valuing the bitcoin network with metcalfe's law

the bitcoin blockchain is a public ledger that contains information about every bitcoin transaction - we can 
use this data to assess the size of the network (and a lot more..). 
one of the charts available on [blockchain.info](blockchain.info/charts) is 
[number of unique addresses used](https://blockchain.info/charts/n-unique-addresses?timespan=60days) each day, 
which gives us an indication of the current size of the *active* bitcoin network. 

<div class="imgcap">
<img src="/assets/images/bitcoin_metcalfes_law/btc_marketcap_wallets.png" >
number of unique btc addresses used each day, and the total market cap. of bitcoin.
raw data downloaded from [blockchain.info](blockchain.info).
</div>

i used the bayesian [pymc3](http://docs.pymc.io/) library to fit the market capital of bitcoin vs
the number of *active* nodes the equation:

$v(n) = \alpha n(n-1).$

<div class="imgcap">
<img src="/assets/images/bitcoin_metcalfes_law/btc_metcalfe.png" >
comparison of metcalfe's law applied to the number of active users to the market capital for bitcoin.
</div>

by using only active wallets in the above analysis i am able to side-step some of the criticisms of metcalfe's law,
as i'm only including the "most valuable" users.
note that our definition of an active user in this analysis is very strict: we're only considering users who have 
used their accounts in the past 24 hours. this is almost certainly too short a period to be accurate: i would 
consider myself a pretty active paypal user and i only use it 3-4 times a month. i will look into a way 
to extract longer time periods from the blockchain.

## valuing the ethereum network with zipf's law

the second largest "cryptocurrency" by market cap. is ethereum, and a publicly available source of 
data for its blockchain is available at [www.etherchain.org](https://www.etherchain.org). the data available 
is slightly different, for instance with ethereum it is possible to view the total number of accounts vs. time.
it should be possible to extract the number of active accounts as per bitcoin, i haven't found a simple way 
to do this yet. 

since i'm working with the total number of ethereum accounts, many of these will be inactive accounts and
so it's reasonable to consider zipf's law might work better here.
i fit the market capital of ethereum to the total number of accounts using the equation:

$v(n) = \alpha n\,log(n).$

<div class="imgcap">
<img src="/assets/images/bitcoin_metcalfes_law/eth_zipf.png" >
comparison of zipf's law applied to the number of total accounts to the market capital for ethereum.
both plots show the same data, but the bottom one is plotted on a logarithmic scale.
</div>

## comments

metcalfe's law and zipf's law can be used to form an approximate number for the value of the bitcoin 
and ethereum networks. i'm not a finance person, and i'll state now that you probably shouldn't use 
the charts above to help your investment decisions: there are assumptions in both methods, and the 
support for each method is purely empirical.

with bitcoin i only considered the currently active wallets, so hopefully this presents the value 
of the network for its utility as a means of transferring money from one place or person to another.
in my opinion this probably ignores most (if not all) of the speculative value of bitcoin, which might explain 
why the current market price is higher than the metcalfe value. many bitcoin acolytes
consider it to be the "gold of the crytocurrencies", a sort of escape from inflationary fiat currencies.
whether it fulfills this task or not is yet to be seen, but it's value as such isn't included in the metcalfe
expression as used here.

ethereum only came out in 2015, so there's a lot less data available on it. it probably piggybacked on 
bitcoin in the sense that people already knew what a cryptocurrency was. with ethereum we have access 
to the number of transactions per day (which we showed above, but didn't use in our analysis). it's 
intereting to see that this increases with time, meaning the network is actually being used more
as it matures. note that it's more challenging to see the total number of (real) transactions with bitcoin 
since it's common to batch multiple "outputs" (recipients) into a single transaction. 
see [here](https://opreturn.org/) for example.

Also notice that neither of these methods really "forecast" the future price, 
they just take the current size of the network and return some number for the current value. 
Looking at the Bitcoin chart for example, we see that the number of active users dropped 
significantly in June 2011 and the price decreased with it. 

## References

\[1\]: Metcalfe's law: A network becomes more valuable as it reaches more users, Infoworld, 1995.

\[2\]: Odlyzko, A. & B. Tilly (2005) A refutation of Metcalfe’s Law and a better estimate for the value of
networks and network interconnections - [Link](http://www.dtc.umn.edu/publications/reports/2005_16.pdf).

