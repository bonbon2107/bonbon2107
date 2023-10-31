
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <time.h>

#define MAX_TRIES 6

int main() 
{
    const char* words[] = {"hangman", "programming", "computer", "science", "language", "algorithm", "developer"};
    srand(time(0));
    int n = rand() % (sizeof(words) / sizeof(words[0]));
    const char* selectedWord = words[n];

    int length = strlen(selectedWord);
    int i, correct = 0, tries = 0;
    char guess, word[length];

    for (i = 0; i < length; i++) {
        word[i] = '-';
    }
    word[length] = '\0';

    printf("Welcome to Hangman!\n");
    printf("Try to guess the word. You have %d attempts.\n", MAX_TRIES);

    while (tries < MAX_TRIES && correct < length) {
        printf("Word: %s\n", word);
        printf("Enter a letter: ");
        scanf(" %c", &guess);

        int found = 0;
        for (i = 0; i < length; i++) {
            if (selectedWord[i] == guess && word[i] != guess) {
                word[i] = guess;
                correct++;
                found = 1;
            }
        }

        if (!found) {
            tries++;
            printf("Incorrect guess. You have %d attempts left.\n", MAX_TRIES - tries);
        }
    }

    if (correct == length) {
        printf("Congratulations! You guessed the word: %s\n", selectedWord);
    } else {
        printf("Sorry, you ran out of attempts. The word was: %s\n", selectedWord);
    }

    return 0;
}
