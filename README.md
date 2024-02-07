# Natural-Language-Processing-Game

This is an algorithm that plays the game of Hangman efficiently, with approximatly 55% word-guessing accuracy on dictionaries of hard difficulty. This accuracy is achieved through the algorithm's "guess" function. Compared to other implementations, this is a consice and efficient way of guessing the next letter.

When a user plays Hangman, the game first selects a secret word at random from a list. The game then returns a row of underscores (space separated)—one for each letter in the secret word—and asks the user to guess a letter. If the user guesses a letter that is in the word, the word is redisplayed with all instances of that letter shown in the correct positions, along with any letters correctly guessed on previous turns. If the letter does not appear in the word, the user is charged with an incorrect guess. The user keeps guessing letters until either (1) the user has correctly guessed all the letters in the word or (2) the user has made a prespecified number of incorrect guesses.

The algorithm uses a training set of approximately 250,000 dictionary words. The algorithm is tested on an entirely disjoint set of 250,000 dictionary words. This means the words that ultimately the algorithm is tested on do NOT appear in the dictionary that the algorithm is trained on. 

When a user plays Hangman, the game first selects a secret word at random from a list. The game then returns a row of underscores (space separated)—one for each letter in the secret word—and asks the user to guess a letter. If the user guesses a letter that is in the word, the word is redisplayed with all instances of that letter shown in the correct positions, along with any letters correctly guessed on previous turns. If the letter does not appear in the word, the user is charged with an incorrect guess. The user keeps guessing letters until either (1) the user has correctly guessed all the letters in the word
or (2) the user has made six incorrect guesses.

The algorithm uses a training set of approximately 250,000 dictionary words. The algorithm is tested on an entirely disjoint set of 250,000 dictionary words. This means the words that ultimately the algorithm is tested on do NOT appear in the dictionary that the algorithm is trained on. 

In particular, the online hangman game is solved using n-grams, since they can be used to derive probabilities on what letter is most likely to come next in a sequence of letters. In specific, n-grams in this work range from uni-grams to six-grams. The algorithm works as follows: 

1) It first creates the n-grams from n=1 to n=6 for all words for the training dictionary. 

2) Then, for the clean word of every iteration, it computes all relevant n-grams which contain an unguessed character. For example, for the word "a.pp.le", the trigram that will be computed will be "a.p", ".pp", "p.l", ".le". Similarly for the rest of the n-grams.

3) Using these n-grams, it calculates the probabilities that each remaining letter has to appear after a sequence of n-1 letters. For trigrams, this gives the probabilities that each letter has to appear after a sequence of two letters. For unigrams, it calculates the probabilities that each letter has to exist at a given spot (equivalent to what the last piece of code in the vanilla self.guess() function does).

4) These probabilities are weighted so that unigrams have the least weight since they give the least amount of information, increasing the weights up to four-grams. The four grams were given the biggest weight because it was noticed that this helped the algorithm make correct guesses for sequences of four, composed of three letters and an unknown character. The five-gram is given more weight that the uni-,bi- and tri-grams since it contains significant more informations, but is given less weight than the six-gram which helps correctly guess letters in long words, and the four-gram which comes more often in medium sized word and helps guess them correctly.
 Keeping this in mind, the final numbers were chosen by trial and error. The sum of these weighted probabilities give the score for each letter

5) The letter with the maximum score is chosen to be the next guess as long as it has not been guessed before.

6) The first guess is manually made so that it is always "a" (the letter "e" could be used as well).
