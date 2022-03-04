# Artificial-Intelligence-BattleGround-2021

I participated in this hackathon with a four-member team. The text of task is:

Maps are generated depending on the round of the competition. The closer you get to the finals, the harder the map gets. A map
is fair to all players. 


<p align="center">
<img width="520" alt="Screenshot 2022-03-03 234108" src="https://user-images.githubusercontent.com/65766968/156665140-81e76928-ed7b-418a-920e-749c547eb269.png">
</p>

There are two types of fields on a map:
1. NORMAL field - players can move on this field. On a normal
field could find an obstacle as a vortex, as well as pirates.
2. Island field (ICELAND) - this field is an island. The islands are impassable, players can't move on them. There may be a shop or a flag on the island.
The map is generated based on the JSON sent to you by the server.

Player number one starts the game with coordinates (-7, -7.14), player number two with coordinates
(14, -7, -7), player number three with coordinates (7.7, -14) and player number four with coordinates (-14.7.7).
At the beginning of the game, two NPCs are also created on the map. They circle at a fixed radius from the center
maps until they see one of the players, after which they start chasing them. If a player manages to escape,
they return by the shortest route to their course.


<p align="center">
<img width="520" alt="image" src="https://user-images.githubusercontent.com/65766968/156667156-d00be8f5-81f1-4297-91f6-256bd1a9c64b.png">
</p>

## Coordinate system

The map uses an offset coordinate system based on offsets from the main diagonals. Three coordinates
that are monitored are:

q - marks the offset from the main diagonal;

r - marks the offset from the midline;

s - marks the offset from the side diagonal;


## Moves

Your avatar has the following attributes:

● ID (id) - avatar identification number;

● Coordinates (q, r, s) - indicate the position on the map (coordinate system is explained)
later in the text);

● Gold coins - which are collected by winning a flag, eliminating an opponent or
NPCs;

● Illegal moves (illegalMoves) - illegal moves include all illegal actions, ie.
actions that cannot be performed. For every 10 illegal moves, the avatar is reduced
life points for 5% of maximum life points;

● Health points - start from a maximum of 400. If health drops to 0,
your avatar is out of the game;

● Maximum life points (maxHealth) - represents the maximum number of lives
points that an avatar may have;

● Cannons - starts at 100, and represents the number of life points you have
the avatar takes off the opponent after the attack;

● Paralyzed - shows if your avatar is paralyzed. trapped in a whirlpool;

● WhirlpoolDuration - shows how many more moves your avatar has captured
in the vortex and cannot get out of it, after entering the vortex, this value is set to 3;

● Number of potions (potNums) - the number of potions your avatar has with them. Your avatar can
have a maximum of 3 drinks;

● Sight - represents how many fields the avatar can see. If
the opposing player is closer or at this distance, in the JSON response from the server
you will be able to see the values of all the attributes of his avatar, marked as playarX, where
is the X ordinal number of the opposing player.

## Actions

Each player must make an order for one action per move. Possible actions are:

● If the field on which the avatar wants to move is an island, moving is impossible;

● If the field is out of the folder, scrolling is not possible;

● If there is another player on the field, it is impossible to move;

● Actions for movement are: nw - up, left - left, sw - down, left - down, e -
right, not -right.

## Shopping from the store

● Purchases from the store are only possible from the surrounding store areas.

● The purchase avatar must have enough gold coins for the transaction it wants
to do.

## Possible transactions

○ If an avatar wants to buy a medicinal potion he can only do so if
currently has a maximum of two drinks. The required number of gold coins is 150, while
action: “buy-POTION”;

○ An avatar can improve their health twice during the game. The price
the first promotion is 200, while the second is 300, and the action is: "buy-HULL";

○ Avatar, during the game, can only double the amount
life points that his attack takes away from the opponent. Price of the first
there are 200 promotions, while the other is 300, and the action is: "buy-CANNONS".

## Improvements

■ Cannons: 100-> 150-> 250;

■ Life points: 400-> 600-> 1000
 
## Use of medicinal drink

● In order to use a healing potion, an avatar must have at least one healing potion
beverage;

● Medicinal drink increases life points by 10% of maximum life
points, while the action is “up”;

## Attacking another avatar or NPC

● You can only attack an opponent if you are within range, ie. if it is at most 2
fields from you;

● The attack reduces the opponent's life points by the strength of your cannons (value
cannons variables), while the action is “atk-X”, where X is your ordinal number
opponents (1, 2, 3 or 4);

● Elimination of the opponent gives the avatar 250 gold coins.
 
## Winning the flag

● The flag is won by the player who first comes to the immediate vicinity of the island on which he is
finds a flag (when the distance between the avatar and the flag is equal to 1).
Winning the avatar flag brings 500 gold coins;

● It is not necessary to issue a special command to win the flag.

## Winning

Any avatar that loses all life points is eliminated from the game.
The game ends after the expiration of 5000 moves or after the elimination of all but one avatar.
If the game ends with the elimination of 3 avatars, the winner is the avatar that remained in the game. Ranking
the remaining three avatars are performed in the order of ejection from the game (the first ejected is the last, the second is ejected
penultimate, etc.).
If the game ends after the expiration of 5000 moves, the winner is the one who collected the most gold coins.
If several avatars have the same number of gold coins, they are ranked according to the number of remaining life points. If 
the avatar has the same number of gold coins and the same number of life points, then you can see how many life points they take off
the attack (cannons attribute).
