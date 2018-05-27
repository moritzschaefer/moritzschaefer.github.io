---
layout: post
title:  "How not to riddle your friends"
date:   2018-05-27
desc: "How not to riddle your friends"
keywords: "post cards,riddle,friends,holiday,clique"
categories: [Holiday]
tags: [Holiday,]
icon: icon-puzzle-piece
---

How not to riddle your friends
==============================

Why sending 16 post cards with an obviously hidden message is not enough

### Introduction

The summer was awesome last year, when I started a road trip with a friend from my hometown. Destination: Spain. After visiting Lyon, Montpellier and Girona, the number one vacation-obligation came to our minds in Barcelona. Sending post cards to friends and families. For our friends, we also wanted to buy a souvenir, in form of a fine bottle of rum. As it seemed boring to just hand it over and because we were too lazy to write post cards with entirely distinct texts, we came up with the idea to exploit the post cards as a carrier for geo-coordinates which would point our friends to a spot, where we buried the bottle of rum. Killing two birds with one stone we thought. Far off!

### Riddle creation

It's important to note that all friends (from now on referred to as recipients), know each other and are in more or less direct communication with each other over a shared WhatsApp group. Our aim was clear: Only teamwork of every single recipient would make it possible to solve the riddle.

<img src="{{ site.img_path }}/postcards/maps.jpg" width="50%">

First we needed a message to encode. Google Maps helped us finding a spot and extracting the coordinates of the position where we would bury the bottle.

<img src="{{ site.img_path }}/postcards/table.jpg" width="50%">
The message (i.e. the coordinates) was encoded like this: The string of characters was split into 16 chunks of similar lengths, 16 being the number of recipients. Each chunk was assigned to one recipient. The image above shows the assigned chunks. There was no way to find out how to concatenate these chunks again in order to retrieve the original message, so we arranged the post cards as a reconstructable chain. The required information for the chain order was encoded in the sender. Instead of writing our names at the bottoms of the post cards, we used the name of the recipient that corresponded to the previous chunk for each of the post cards.
This also functioned as another hint towards the recognition of the post cards as a riddle (it was known that some of the "senders" were not around Barcelona that time). See the green area for an example of this information in the image below. Notice, how we even failed to spell the name of the sender correctly, which was yet another hint in this specific post card. The image below also demonstrates the "frame" in which we embedded the chunk of information: We designed a very ordinary post card text, which contained one number that represented a temperature (see the red area). In the demonstrated example, a chunk of the coordinates is embedded that seems like a reasonable temperature. However, also unlogical temperatures like "04" or even the characters "°" and "'" occurred. The texts of all post cards matched with exception of the two marked areas in order to make it clear which parts of the postcard contained relevant information.

<img src="{{ site.img_path }}/postcards/postcard.jpg" width="50%">

### How to solve the riddle?

The way of decoding the message seems very hard without a manual, so here is how we thought it would get solved.

The key for solving the puzzle were the cards that contained irrational temperatures (5 degrees in summer in Barcelona) or just non-sense characters (e.g. Es hat zwar viel zu heiße ° Grad). The recipients of those cards needed to notice the oddness in the message and hence motivate the comparison of the post cards of different recipients (remember that all friends knew each other and all of them received weird post cards at the same time). After the comparison of two cards, it would become clear that only a very small part of the text differs. Getting to the conclusion, that the post cards contained some hidden information was the first part of the riddle. The second part was to decode the message.
Each post card contained two informations: one to two characters of the coordinates to uncover and the relative position of the characters with respect to the "sender". It was easy to identify the two varying characters, as the rest of the postcard was exactly the same so the only thing missing to solve the riddle was to realize that the characters needed to be concatenated in a certain order to retrieve the hidden message.
Once the post cards reached their destinations, the recipients already communicated and noticed that the transmitters were fake ("I didn't know you were in Barcelona" -> "I wasn't..."; "thank you for the post card, you recently sent" -> "me? I did not send any post card.."). In combination with the knowledge that the post cards contained a hidden message, it was necessary to identify the sender-recipient relationship as a chain that corresponded to the order of the characters in the hidden message. This was probably the hardest part of the riddle and it required someone to have knowledge about most of the postcards (for example by sharing images of the messages) in order to detect this hidden relationship.

### What happened

Nothing. Even after subsequently injecting more and more obvious hints into our circle of friends no one became interested in solving the riddle.

### Why it didn't work

Solving the riddle involved a sequence of combinatorial solving thoughts. It was not a hard problem but one that required a decent amount motivation of at least one person in combination with the cooperation of all involved recipients. Even though we anticipated, that most of our friends wouldn't care about the strange post cards (after all most post cards are written in a funny and more or less creative way), we relied on one of our friends especially and were sure he would question the oddness of the message and contact others in order to understand what was going on. He did not (he had a lot of other things going on during that time)
Concluding, it would have been better to provide more obvious clues, identifying the post cards as a riddle.
The second reason of failure was the motivation to solve the riddle. Once we told people that it's a riddle, still no one cared (which I am a bit disappointed about). It seems like we should have pointed out that there is a good bottle of booze to win and things might have gone differently.


Even though, the riddle ended as a disappointment, it was a lot of fun designing it and I'm looking forward to the next riddle I'll stumble upon. And now, GO AND FINALLY GET THAT FREAKIN BOTTLE!
