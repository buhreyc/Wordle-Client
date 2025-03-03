# Project 1 - Socket Basics
**Brey-Michael Ching**
Coded in Python

## High-Level Approach
The client program uses the following approach:
1. **Initialization**: The client connects to the server using either a standard or TLS-secured socket and then sends a "hello" message to identify itself and begins the game
2. **Initial Guess**: The client will then select the first word from the wordlist file provided - for this case, we utilized wordlist.txt.
3. **Receive Feedback and Wordlist filtering**: The client will then take the feedback that the server gives for the word and thusly condenses the wordlist. For the spec, there are three types of feedback:
- '2' - Correct letter in correct position
- '1' - Correct letter in wrong position
- '0' - Letter does not appear in the word unless otherwise required by '2' or '1'
4. **Iterative Feedback Loop**: The client will then continue making guesses and refining the wordlist until one of two situations occurs:
- The correct word is found and the server responds with a "bye" and a game flag
- No valid guesses remains (This **should not happen** at any point unless the server wordlist is expanded and the client-side one is not, in which case the client will terminate if the word is not found)
5. **General Error Handling**: The client will handle errors like connection issues or invalid server responses

## Challenges Faced:
1. **Wordlist filtering**: For the program, ensuring that the filtering logic worked within the game rules was the most difficult part in my opinion and is where most of the challenges lied.
- **Optimization**: For an initial prototype of the wordlist filter, it originally went through each and every single word in the list again and again, which though complexity was not a concern, it ended up needing to be changed for debug and optimization purposes due to the sheer amount of words.
- **Edge Cases** Many of the edge cases for the filter such as repeating letters and gray marks for letters already determined to be in the word were the most challenging as it required temporary count variables to handle and manage for such words in the filter.

## Guessing Strategy:
In a top-down view of the guessing strategy, the client employs the following steps:
1. Start with a preloaded wordlist that has all potential guesses
2. Guess the first word in the wordlist and receive feedback
3. Use the feedback to filter out all invalid words iteratively and create a new wordlist
5. Repeat from Step 2 until either the server sends the secret-flag or the client makes 500 incorrect guesses

In general terms, the client will make a guess and shrink the wordlist based on feedback in a loop until it determines which word will fit the best

## Testing Overview:

For this assignment, I tested my program on the login.ccs.neu.edu server and ran the following command(s):
- ./client proj1.4700.network ching.b
- ./client -s proj1.4700.network ching.b

To help test and determine if the filtering or the port connections were working, in the code, there are print statements that are commented out that were used for testing and debugging during the process.