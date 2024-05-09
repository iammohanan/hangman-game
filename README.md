import random

def select_word():
    """Selects a random word from the list of words."""
    words = ['python', 'programming', 'computer', 'science', 'algorithm', 'data', 'structure', 'function', 'variable', 'loop']
    return random.choice(words)

def display_hangman(guesses):
    """Displays the hangman based on the number of incorrect guesses."""
    stages = ['_______',
             '|       |',
             '|       0',
             '|      \\|/',
             '|       |',
             '|      / \\']

    print(stages[guesses])

def get_guess(already_guessed):
    """Gets a guess from the user and checks if it's a valid guess."""
    while True:
        guess = input('Guess a letter: ').lower()
        if len(guess) != 1:
            print('Please enter only one letter.')
        elif guess in already_guessed:
            print('You have already guessed this letter.')
        elif guess not in 'abcdefghijklmnopqrstuvwxyz':
            print('Please enter a valid letter.')
        else:
            return guess

def play_hangman():
    """Plays the Hangman game."""
    word = select_word()
    guessed_word = ['_'] * len(word)
    guesses = 0
    already_guessed = []

    print('Let\'s play Hangman!')
    display_hangman(guesses)
    print(' '.join(guessed_word))

    while True:
        guess = get_guess(already_guessed)
        if guess in word:
            for i, letter in enumerate(word):
                if letter == guess:
                    guessed_word[i] = letter
            print(' '.join(guessed_word))
            if '_' not in guessed_word:
                print('Congratulations, you won!')
                break
        else:
            already_guessed.append(guess)
            guesses += 1
            display_hangman(guesses)
            if guesses == len(stages) - 1:
                print('You lost! The word was {}.'.format(word))
                break

if __name__ == '__main__':
    play_hangman()
