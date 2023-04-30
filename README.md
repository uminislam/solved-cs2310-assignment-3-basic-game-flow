Download Link: https://assignmentchef.com/product/solved-cs2310-assignment-3-basic-game-flow
<br>
In this assignment, students will write programs to emulate the flow of a new type of card game called <strong>CCC</strong> (<strong>C</strong>ityU <strong>C</strong>ard <strong>C</strong>ombat), which is played among two players. The game starts with a deck of 50 unique cards, which is shuffled thoroughly. In each turn, 5 cards are dealt alternately to each player. With the 5 cards, each player constructs a <em>hand of cards</em> according to the categories listed in session 1.3. The player with a better <em>hand of cards</em> scores 1 point in this turn. After a single turn, the 10 dealt cards are discarded. The same process is then repeated at most 4 more times until there is no unused card left in the deck, or until either player scored 3 marks. The player with higher total score is the winner of the game.

<h2>1.2   CCC Cards</h2>

Each <strong>Card</strong> is marked with a <strong>digit</strong> in range <strong>[0..9]</strong> and shaded by one of the <strong>color</strong>s as in the zones of the CityU building: <strong>{</strong><strong>red, </strong><strong>yellow, </strong><strong>blue, </strong><strong>green, </strong><strong>purple}</strong>. <em>(The fact that they put blue (instead of green) as the neighbor of yellow is one of the seven greatest mysteries in CityU…)</em>. Each <strong>Number Card</strong> exists only once and holds a unique <em>card rank (there’s never a tie)</em>. When comparing the ranks of two cards, the card with the larger digit is considered as having a higher rank <strong>(9&gt;8&gt;7&gt;6&gt;5&gt;4&gt;3&gt;2&gt;1&gt;0)</strong>. Only if the two cards are having the same digit, we consider the color

<strong>(</strong><strong>red&gt;</strong><strong>yellow&gt;</strong><strong>blue&gt;</strong><strong>green&gt;</strong><strong>purple)</strong>.

<h2>1.3   Card Hands</h2>

With 5 CCC Cards, a player can construct one of the predefined card hands. There is a total of 10 card ranks as listed below (in the order of descending rank):

<strong>Legend: [R: Red][Y: Yellow][B: Blue][G: Green][P: Purple] </strong>

<table width="0">

 <tbody>

  <tr>

   <td width="139"><strong>Rank Name </strong></td>

   <td width="312"><strong>Criteria </strong></td>

   <td colspan="5" width="120"><strong>Examples </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Straight Flush </strong></td>

   <td width="312">l Only 1 color in handl 5 sequential digits</td>

   <td colspan="5" width="120"><strong>R1 R2 R3 R4 R5</strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Five Of A Kind </strong></td>

   <td width="312">l All cards with the same digit</td>

   <td width="9"> </td>

   <td colspan="3" width="101"><strong>R4 </strong><strong>Y4 </strong><strong>B4 </strong><strong>G4 </strong><strong>P4</strong></td>

   <td width="10"><strong> </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Four Of A Kind </strong></td>

   <td width="312">l 4 cards with the same digit</td>

   <td colspan="2" width="31"><strong>G0 </strong></td>

   <td colspan="2" width="80"><strong>R4 </strong><strong>Y4 </strong><strong>B4 </strong><strong>G4</strong></td>

   <td width="10"><strong> </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Rainbow </strong></td>

   <td width="312">l 5 unique colors in hand</td>

   <td width="9"> </td>

   <td colspan="3" width="101"><strong>R1 </strong><strong>Y3 </strong><strong>B4 </strong><strong>G7 </strong><strong>P9</strong></td>

   <td width="10"><strong> </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Flush </strong></td>

   <td width="312">l Only 1 color in hand</td>

   <td width="9"> </td>

   <td colspan="3" width="101"><strong>R1 R3 R4 R7 R9</strong></td>

   <td width="10"><strong> </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Straight </strong></td>

   <td width="312">l 5 sequential digits</td>

   <td width="9"> </td>

   <td colspan="3" width="101"><strong>R1 </strong><strong>Y2 </strong><strong>Y3 </strong><strong>G4 G5</strong></td>

   <td width="10"><strong> </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Three Of A Kind </strong></td>

   <td width="312">l 3 cards with the same digit</td>

   <td width="9"> </td>

   <td colspan="2" width="58"><strong>R1 </strong><strong>Y1 </strong><strong>B1</strong></td>

   <td colspan="2" width="53"><strong> </strong><strong>G6 G7 </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>Two Pair </strong></td>

   <td width="312">l 2 cards with the same digitl Another 2 cards with the same digit</td>

   <td colspan="5" width="120"><strong>R1</strong><strong> Y1 </strong><strong>B2 B3 </strong><strong>G3 </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>One Pair </strong></td>

   <td width="312">l 2 cards with the same digit</td>

   <td colspan="2" width="31"><strong>B0 </strong></td>

   <td width="36"><strong>R1</strong><strong> Y1</strong></td>

   <td colspan="2" width="53"><strong> </strong><strong>G2 </strong><strong>B4 </strong></td>

  </tr>

  <tr>

   <td width="139"><strong>High Card </strong></td>

   <td width="312">l None of the above</td>

   <td colspan="5" width="120"><strong>B0 </strong><strong>R1 </strong><strong>G2 </strong><strong>B4 </strong><strong>Y7 </strong></td>

  </tr>

  <tr>

   <td width="139"></td>

   <td width="312"></td>

   <td width="9"></td>

   <td width="21"></td>

   <td width="36"></td>

   <td width="43"></td>

   <td width="10"></td>

  </tr>

 </tbody>

</table>




When building card hands, we consider only the <em>highest rank achievable</em>. For instance, <strong>[R4 Y4 B4 G4 P4]</strong>, despite having 5 colors, is regarded as “<strong>Five Of A Kind</strong>” rather than “<strong>Rainbow</strong>” (as the former is in higher rank).




For hands requiring sequential digits <em>(“<strong>Straight</strong>”, “<strong>Straight Flush</strong>”)</em>, a special rule applies: The digit <strong>0</strong> can optionally be considered as <strong>10</strong>. Therefore The hand <strong>{6,7,8,9,0}</strong> is also considered as sequential. Do note that <strong>1</strong> is <strong>not</strong> considered as <strong>11</strong>, therefore <strong>{7,8,9,0,1}</strong> is <strong>NOT sequential</strong>.




When the players compare their <em>hands of cards</em>, the player with a higher rank is the winner of that turn. Only when the two players have the same rank, we’ll <strong>break tie with the highest card in hand</strong>. For instance, when player A holds <strong>[B6 G7 Y8 Y9 R0]</strong> and player B holds <strong>[B3 Y4 Y5 G6 R7]</strong>, both hands are considered as “<strong>Straight</strong>”. We then compare the highest card of player A (<strong>Y9</strong>) against the highest card of player B (<strong>R7</strong>), the winner in that turn is player A.

(Note: Although <strong>R0</strong> is used as <strong>10</strong> for building <strong>“Straight”</strong>, we still consider it as <strong>0</strong> when we break tie).




<h1>2.    Class construction</h1>

Students need to create at least 3 classes, with properties and methods as shown below.

(Students may create extra constructors, properties and methods if needed)

<h2>2.1   <strong>Card</strong> class</h2>

<table width="0">

 <tbody>

  <tr>

   <td width="151">Private Properties:</td>

   <td width="427">Description</td>

  </tr>

  <tr>

   <td width="151"><strong>char color </strong></td>

   <td width="427">Single character for the card color<strong>[R: Red][Y: Yellow][B: Blue][G: Green][P: Purple]</strong></td>

  </tr>

  <tr>

   <td width="151"><strong>char digit </strong></td>

   <td width="427">Single character for the card digitRange:<strong> [‘0’..’9’]</strong>,</td>

  </tr>

 </tbody>

</table>




<table width="0">

 <tbody>

  <tr>

   <td width="151">Public Methods:</td>

   <td width="427">Description</td>

  </tr>

  <tr>

   <td width="151"><strong>Card(c,d) </strong></td>

   <td width="427">Constructor setting the color and digit respectively</td>

  </tr>

  <tr>

   <td width="151"><strong>bool greater (Card) </strong></td>

   <td width="427"><strong>Input</strong>: another <strong>Card</strong> object<strong>Output</strong>: Boolean<strong>true</strong> if the rank of current card is greater than the input card, <strong>false</strong> otherwise</td>

  </tr>

 </tbody>

</table>




<h2>2.2   <strong>Hand</strong> class</h2>

<table width="0">

 <tbody>

  <tr>

   <td width="151">Private Properties:</td>

   <td width="427">Description</td>

  </tr>

  <tr>

   <td width="151"><strong>Card cards </strong></td>

   <td width="427">An array of <strong><em>5</em></strong> <strong>Card</strong> objects</td>

  </tr>

  <tr>

   <td width="151"><strong>int length </strong></td>

   <td width="427">Number of cards in hand (constructor set default to 0)</td>

  </tr>

 </tbody>

</table>




<table width="0">

 <tbody>

  <tr>

   <td width="151">Private Methods:</td>

   <td width="426">Description</td>

  </tr>

  <tr>

   <td width="151"><strong>bool isRainbow() </strong></td>

   <td width="426">Whether the Hand <em>could</em> form a “<strong>Rainbow</strong>” hand. (Note: the function just checks whether it is possible, the final result may turn out to be something else like “Five Of a Kind”.)  Return <strong>false</strong> if there’re less than 5 cards.</td>

  </tr>

  <tr>

   <td width="151"><strong>bool isFlush() </strong></td>

   <td width="426">Whether the Hand <em>could</em> form a “<strong>Flush</strong>” hand.   Also return <strong>false</strong> if there’re less than 5 cards.</td>

  </tr>

  <tr>

   <td width="151"><strong>bool isStraight() </strong></td>

   <td width="426">Whether the Hand <em>could</em> form a “<strong>Straight</strong>” hand.  Also return <strong>false</strong> if there’re less than 5 cards.</td>

  </tr>

  <tr>

   <td width="151"><strong>bool isTwoPair() </strong></td>

   <td width="426">Whether the Hand <em>could</em> form a “<strong>Two Pair</strong>” hand.   Also return <strong>false</strong> if there’re less than 5 cards.</td>

  </tr>

  <tr>

   <td width="151"><strong>int getMaxDup() </strong></td>

   <td width="426">Return the maximum <em>count</em> of duplicate digits in hand. (e.g. 3 for three-of-a-kind)  Note: For multiple-duplicates (<strong>e.g. “Two Pair”</strong>), return the maximum count (2 for Two Pair)</td>

  </tr>

 </tbody>

</table>







<table width="0">

 <tbody>

  <tr>

   <td width="163">Public Methods:</td>

   <td width="414">Description</td>

  </tr>

  <tr>

   <td width="163"><strong>void discard() </strong></td>

   <td width="414">Make the hand empty (0 cards)</td>

  </tr>

  <tr>

   <td width="163"><strong>bool take(Card) </strong></td>

   <td width="414"><strong>Input</strong>: A <strong>Card</strong> objectThe method appends the input <strong>Card</strong> to the private <strong>cards</strong> array if there’re less than 5 cards. <strong>length</strong> member is updated accordingly.<strong> </strong><strong>Output</strong>: Boolean<strong>true</strong> if the <strong>Card</strong> is appended successfully, <strong>false</strong> if there’re already 5 cards.</td>

  </tr>

  <tr>

   <td width="163"><strong>bool greater(Hand) </strong></td>

   <td width="414"><strong>Input</strong>: two <strong>Hand</strong> objects <strong>Output</strong>: Boolean<strong>true</strong> if the current hand is greater than that of the input hand object (as described in session 1.3)<strong>false</strong> is returned if the current hand is not greater, or if either hand has less than 5 cards.</td>

  </tr>

  <tr>

   <td width="163"><strong>char* getRankName() </strong></td>

   <td width="414">Return the name of rank formed by the 5 cards as described in session 1.3. Return <strong>NULL</strong> if there are less than 5 cards.</td>

  </tr>

  <tr>

   <td width="163"><strong>Card getHighCard() </strong></td>

   <td width="414">Return (not remove!) the single <strong>Card </strong>object with the highest rank. <em>(you may assume there’s at least 1 card when called) </em></td>

  </tr>

 </tbody>

</table>

<h2>2.3   <strong>Deck</strong> class</h2>

<table width="0">

 <tbody>

  <tr>

   <td width="151">Private Properties:</td>

   <td width="427">Description</td>

  </tr>

  <tr>

   <td width="151"><strong>Card cards </strong></td>

   <td width="427">An array of <strong><em>50</em></strong> <strong>Card</strong> objects</td>

  </tr>

  <tr>

   <td width="151"><strong>int length </strong></td>

   <td width="427">Number of cards in Deck</td>

  </tr>

 </tbody>

</table>




<table width="0">

 <tbody>

  <tr>

   <td width="151">Public Methods:</td>

   <td width="426">Description</td>

  </tr>

  <tr>

   <td width="151"><strong>Deck() </strong></td>

   <td width="426">Constructor automatically fills the <strong>cards</strong> array with 50 cards, in the order (starting from position [0]): Red 0..9, Yellow 0..9, Blue 0..9, Green 0..9, Purple 0..9.</td>

  </tr>

  <tr>

   <td width="151"><strong>void refresh() </strong></td>

   <td width="426">Dispose the remaining cards in <strong>Deck</strong> and refill the <strong>Deck</strong> with 50 cards as in the constructor</td>

  </tr>

  <tr>

   <td width="151"><strong>Card deal() </strong></td>

   <td width="426">Remove the <strong>Card</strong> <em>with the highest array index</em> from the deck. (you may assume that the deck is non-empty when being called). The <strong>length</strong> member should be updated accordingly.</td>

  </tr>

  <tr>

   <td width="151"><strong>void swap(int s, int e) </strong></td>

   <td width="426">If <strong>0</strong>≤<strong>S</strong>,<strong>E</strong>&lt;<strong>length</strong>, swap the card at index s with the card at index e. For example, in deck[R0 R1 R2 R3…], swap(1,3) will result in [R0 R3 R2 R1…] </td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<h1>3.    Program construction</h1>

Students need to prepare two C++ programs for Part A and B respectively, subjected to the following requirements:

3.1   <strong>Part A </strong>

In Part A, you need to write a program to classify hands. The input is consisted of multiple test cases, one at a line. The first line of input is the number of test cases follow. Each line contains 5 unique cards, each represented by the two-character code as in session 1.3 (case sensitive). Spaces may appear on a line <em>(e.g. between cards)</em>, but never between the two characters of the card code. For each input line, your program should print out, on a single line, the name of the highest achievable rank as listed in session

1.3 (case sensitive).




<table width="0">

 <tbody>

  <tr>

   <td width="283"><strong>Sample Input </strong></td>

   <td width="306"><strong>Sample Output </strong></td>

  </tr>

  <tr>

   <td width="283">3R1 R2 R3 R4 R5R5 B1 B2 Y5 P5B1 Y2 Y3 Y4 Y5</td>

   <td width="306">Straight FlushThree Of A KindStraight </td>

  </tr>

 </tbody>

</table>




<h2>3.2   <strong>Part B </strong></h2>

In Part B, you need to write a program to emulate a game with a full deck. The program first reads an integer (<strong>N</strong>≥1) from keyboard, which represents the number of games to play. Each game begins with an unshuffled deck of 50 cards (as in the constructor mentioned in session 2.3). For each game, the program reads an integer (<strong>H</strong>≥0), which represents the number of <strong>swap</strong> operations required. The program then reads <strong>H</strong><em> pairs</em> of integer (<strong>S</strong>,<strong>E</strong>) from the keyboard and pass the pair to <strong>Deck::swap()</strong> function mentioned in session 2.3. After swap, cards are deal alternatively (with <strong>Deck::deal()</strong>) to the players. Dealing of cards always starts from Player A and ends when each player holds 5 cards in their hands. For each turn, display the cards of each player <em>(as in the deal order)</em>, together with the name of the hands on a line of its own <em>(see below for detail output format)</em>. Also generate a line with the accumulated score <em>of the current game</em> so far, followed by a blank line. The game then continues until the final winner is confirmed <em>(i.e. either player scored 3 marks)</em>. Finally print a single line with the name of the winner, followed by a blank line.




<table width="0">

 <tbody>

  <tr>

   <td width="127"><strong>Sample Input </strong></td>

   <td colspan="2" width="334"><strong>Sample Output </strong><em>(for easy observation, empty lines are </em></td>

   <td width="61"><em>highlighted</em></td>

   <td colspan="2" width="66"><em> here)</em></td>

  </tr>

  <tr>

   <td rowspan="2" width="127">1148 49</td>

   <td colspan="5" width="462">PlayerA: [P8 P7 P5 P3 P1] is Flush PlayerB: [P9 P6 P4 P2 P0] is FlushPlayerB won in this turn (PlayerA:0 PlayerB:1)

    <table width="0">

     <tbody>

      <tr>

       <td width="451"> </td>

      </tr>

     </tbody>

    </table>PlayerA: [G9 G7 G5 G3 G1] is Flush PlayerB: [G8 G6 G4 G2 G0] is FlushPlayerA won in this turn (PlayerA:1 PlayerB:1)

    <table width="0">

     <tbody>

      <tr>

       <td width="451"> </td>

      </tr>

     </tbody>

    </table>PlayerA: [B9 B7 B5 B3 B1] is Flush PlayerB: [B8 B6 B4 B2 B0] is FlushPlayerA won in this turn (PlayerA:2 PlayerB:1)

    <table width="0">

     <tbody>

      <tr>

       <td width="451"> </td>

      </tr>

     </tbody>

    </table>PlayerA: [Y9 Y7 Y5 Y3 Y1] is FlushPlayerB: [Y8 Y6 Y4 Y2 Y0] is FlushPlayerA won in this turn (PlayerA:3 PlayerB:1)

    <table width="0">

     <tbody>

      <tr>

       <td width="451"> </td>

      </tr>

     </tbody>

    </table>PlayerA is the final winner!</td>

  </tr>

  <tr>

   <td width="5"> </td>

   <td colspan="3" width="451"> </td>

   <td width="5"> </td>

  </tr>

  <tr>

   <td width="127"></td>

   <td width="5"></td>

   <td width="329"></td>

   <td width="61"></td>

   <td width="61"></td>

   <td width="5"></td>

  </tr>

 </tbody>

</table>

<em>(Description: The 1 in first line means that there is only ONE game. The 1 in second line means that there’s only one <strong>swap</strong> operation. 48 49 means swapping the cards in position [48] (i.e. P8) and that in position [49] (i.e. P9)) </em>