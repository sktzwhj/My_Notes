#Baysian theory and Marcov model

Youtube video: A friendly intro to bayes theroem and hidden markov model

let's say we have two people Bob and Alice. 

Bob's mood depends on the condition of the weather. If the weather is sunny, he will be happy with a chance of 80% and unhappy with a chance of 20%. 

1. How do we find the probabilities?

in a sequence, how many times a sunny (rainy day) day is followed by a sunny day (rainy day). these are called transition probabilities. 

similarly, we can get the emission probabilities. 


2. What's the probability that a random day is sunny or rainy?

3. If Bob is happy today, what's the probability that it's sunny or rainy?

Bayes Theorem

for a markov model, we have hidden status and observations

what's the difference between prior and postior probabilities. 

4. Given a sequence of moods for Bob, so what could the weather be like in these days?

then we can use hidden markov model
Veterbi algorithm (similar to dynamic programming)

suppose we have a relatively long sequence of 

monday -> tuesday -> wednesday -> thursday -> friday -> saturday
happy  -> happy   -> unhappy   -> unhappy  -> unhappy-> happy

we do not check all the combinations of the 2^6 scenarios. what we do is similar to dynamic programming, for the last day, 
we just compare the two scenairos: 1. the best path reaching sunny on sat and the best path reaching rainy on sat. so on so force. 