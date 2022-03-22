# Name: Alyssa Gorbaneva
# Start Date: 8/18/21

# parameters:
# dictionary_file word
# word format: dashes and letters. Ex: p---- is place
def create_dictionary():
    file = "./Dictionary"
    dictionary = {}
    for line in open(file, "r"):
        word = line.strip()
        if len(word) not in dictionary:
            dictionary[len(word)] = [word]
        else:
            dictionary[len(word)].append(word)

    return dictionary


def guessLetter(possibleLetters, possibleWords):
    letterCount = {}

    for letter in possibleLetters:
        letterCount[letter] = 0
        for word in possibleWords:
            if letter in word:
                letterCount[letter] += 1

    letter = ""
    maximum = 0
    for key, value in letterCount.items():
        if value > maximum and key in possibleLetters:
            letter, maximum = key, value

    return letter


def switch(string, value, pos):
    return string[:pos] + value + string[pos + 1:]


def updateWords(letter, answer, possibleWords):
    potentialWords = possibleWords[:]
    for word in possibleWords:
        for x in range(len(word)):
            if (word[x] == letter and answer[x] != letter) or (word[x] != letter and answer[x] == letter):
                potentialWords.remove(word)
                break

    return potentialWords

def updateInitial(answer, possibleWords):
    potentialWords = possibleWords[:]
    for word in possibleWords:
        for x in range(len(word)):
            if answer[x] != '-' and answer[x] != word[x]:
                potentialWords.remove(word)
                break

    potentialLetters = "abcdefghijklmnopqrstuvwxyz"
    letterCounts = {}
    for letter in potentialLetters:
        letterCounts[letter] = 0

    for x in range(len(answer)):
        if answer[x] == '-':
            for word in potentialWords:
                if letterCounts[word[x]] == 0:
                    letterCounts[word[x]] = 1

    for key, value in letterCounts.items():
        if value == 0:
            potentialLetters = switch(potentialLetters, "", potentialLetters.index(key))

    return potentialWords, potentialLetters



def main():
    dictionary = create_dictionary()
    answer = input("Write the information you know about your word! Use '-' for unknown letters: ")  # answer is a string
    possibleWords = dictionary[len(answer)]  # possibleWords is a list
    possibleLetters = "abcdefghijklmnopqrstuvwxyz"
    if answer != len(answer) * '-':
        print("Some letters already filled in, updating possible words.")
        possibleWords, possibleLetters = updateInitial(answer, possibleWords)
    while '-' in answer:
        letter = guessLetter(possibleLetters, possibleWords)
        if letter == "":
            print("Word not in dictionary. Good luck.")
            break
        print("Guess the letter " + letter + ".")

        confirmation = input("Did it work? Y/N ").capitalize()
        if confirmation == 'Y' and answer.count('-') == 1:
            answer = switch(answer, letter, answer.index('-'))
        elif confirmation == 'Y':
            positions = input("What places were the letter added? (Separate by spaces) ").split(" ")
            #in case of typo
            if len(positions) == "\n":
                print("You pressed enter on accident, try again!")
                positions = input("What places were the letter added? (Separate by spaces) ").split(" ")

            for pos in positions:
                answer = switch(answer, letter, int(pos))
                print(answer)
        elif confirmation == 'N':
            print("Letter failed.")
            # GUESS AGAIN
        else:
            print("\nWrong input of " + confirmation + " instead of Y/N. Let's try again.")
            continue
        # update the possible letters and words
        possibleLetters = switch(possibleLetters, "", possibleLetters.index(letter))
        possibleWords = updateWords(letter, answer, possibleWords)
        if len(possibleWords) == 1:
            answer = possibleWords[0]

    print("Your word is " + answer +". Hope you come try again sometime! :)")

main()
