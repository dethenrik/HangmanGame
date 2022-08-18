# HangmanGame
this is a program i made for school called hangmanGame, its a game where you can guess wrong 6 times and the limps of the hangman gets added everytime you guess wrong. it is possible to make your own words and sent to a friend, as of now the word are (cake, tommygun, monitor, sunrise and sundown). have a great day :)
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
using System;
using System.Collections.Generic;
using static System.Random;
using System.Text;

namespace HangmanGame
{
    internal class program
    {
        public static void PrintHangman(int wrong)
        {
            if (wrong == 0)
            {
                Console.WriteLine("\n+---+");
                Console.WriteLine("    |");
                Console.WriteLine("    |");
                Console.WriteLine("    |");
                Console.WriteLine("   ===");
            }
            else if (wrong == 1)
            {
                Console.WriteLine("\n+---+");
                Console.WriteLine(" o  |");
                Console.WriteLine("    |");
                Console.WriteLine("    |");
                Console.WriteLine("   ===");
            }
            else if (wrong == 2)
            {
                Console.WriteLine("\n+---+");
                Console.WriteLine(" o   |");
                Console.WriteLine(" |   |");
                Console.WriteLine("     |");
                Console.WriteLine("    ===");
            }
            else if (wrong == 3)
            {
                Console.WriteLine("\n+---+");
                Console.WriteLine(" o   |");
                Console.WriteLine("/|   |");
                Console.WriteLine("     |");
                Console.WriteLine("    ===");
            }
            else if (wrong == 4)
            {
                Console.WriteLine("\n+---+");
                Console.WriteLine(" o   |");
                Console.WriteLine("/|\\ |");
                Console.WriteLine("     |");
                Console.WriteLine("    ===");
            }
            else if (wrong == 5)
            {
                Console.WriteLine("\n+---+");
                Console.WriteLine(" o   |");
                Console.WriteLine("/|\\ |");
                Console.WriteLine("/    |");
                Console.WriteLine("    ===");
            }
            else if (wrong == 6)
            {
                Console.WriteLine("\n+---+");
                Console.WriteLine(" o   |");
                Console.WriteLine("/|\\ |");
                Console.WriteLine("/ \\ |");
                Console.WriteLine("    ===");
            }
        }

        public static int printWord(List<Char> guessedLetters, string randomWord)//creating a list that has <>=Letters thats been guessed called guessedLetters
        {
            int counter = 0;// counting wrong guessses
            int rightLetter = 0;// counting right guesses
            Console.Write("\r\n");// makes sure there is enough spacing between lines
            foreach (Char c in randomWord)// allow us to repeat the letter in the string given to us in the beginning of the game
            {
                if (guessedLetters.Contains(c))// if character we are on is inside of the random name we generated, it will print it out
                {
                    Console.Write(c + " "); // character guessed plus a space.
                    rightLetter++;// counts the amount of letters if correct
                }
                else
                {
                    Console.Write(" ");
                }
                counter++;// counts towards wrong guesses
            }
            return rightLetter;
        }
        public static void printLines(string randomWord) // method for printing out the lines under the letters.
        {
            Console.Write("\r");// makes a new line
            foreach (char c in randomWord)// allow us to repeat the letter in the string given to us in the beginning of the game
            {
                Console.OutputEncoding = System.Text.Encoding.Unicode;
                Console.Write("\u0305 ");
            }
        }

        public static void Main(string[] args)
        {
            Console.WriteLine("Welcome to Hangman :)");//welcome statement
            Console.WriteLine("---------------------");// splitter

            Random random = new Random(); // creates a random object
            List<string> wordDictionary = new List<string> { "cake", "tommygun", "monitor", "sunrise", "sundown" };// this is a list containing word i need for Hangman, called wordDictionary and the type is string
            int index = random.Next(wordDictionary.Count); // creates an int called index and takes random in its hands a walk through the dictionary and generate a random number between 0 and the amount of words in wordDictionary
            string randomWord = wordDictionary[index]; // generates a word from the number given by index inside of wordDictionary (does not print the name onmly saves it in randomWord)


            foreach (char x in randomWord)// creates the lines needed for the user to guess the word
            {
                Console.Write("_ ");
            }

            int lengthOfWordToGuess = randomWord.Length;// creates a variable on length of the word to guess
            int amountOfTimesWrong = 0; // keeps track on times wrong
            List<char> currentLettersGuessed = new List<char> ();// list of letters guessed
            int currentLettersRight = 0;// keeps track on amount of letters guessed correctly


            while (amountOfTimesWrong != 6 && currentLettersRight != lengthOfWordToGuess)// makes so that we can keep playing unless we havent guessed the entire word or amount of times wrong is not 6
            {
                Console.Write("\nLetters guessed so far: ");
                foreach (char letter in currentLettersGuessed)// created as we need to go through the list currentLettersGuessed to find out which letters have been guessed and print it out
                {
                    Console.Write(letter + " ");
                }

                // user input
                Console.Write("\nGuess a letter: ");
                char letterGuessed = Console.ReadLine()[0];// puts letter guessed inside of letterGuessed and it only takes the first letter[0] so user can type in a whole word but only first letter will be taken out of the word and saved.
                if (currentLettersGuessed.Contains(letterGuessed))//checks through if letter have been used already - if "currentLettersGuessed" contains "letterGuessed" do something
                {
                    Console.Write("\r\nYou have already guessed this letter");
                    PrintHangman(amountOfTimesWrong);// prints the Hangman and the amount of letters guessed wrong
                    currentLettersRight = printWord(currentLettersGuessed, randomWord);
                    printLines(randomWord);
                }
                else
                {
                    //check if letter is in the word or not 
                    bool right = false;
                    for (int i = 0; i < randomWord.Length; i++) if (letterGuessed == randomWord[i]) { right = true; }// if the guessed letters is anywhere here is will change from right to true in case the word do contain the letter
                    {
                        if (right)
                        {
                            PrintHangman(amountOfTimesWrong);// prints hangman 
                            currentLettersGuessed.Add(letterGuessed);// adds letter guessed to array
                            currentLettersRight = printWord(currentLettersGuessed, randomWord);// sets amount of right letters
                            Console.Write("\r\n");
                            printLines(randomWord);// prints lines underneath the word
                        }
                        else// incase user is wrong
                        {
                            amountOfTimesWrong++; //plusses amount of times wrong by 1
                            currentLettersGuessed.Add(letterGuessed);// adds letter guessed to array
                            PrintHangman(amountOfTimesWrong);// have to be after the counter to make sure it adds the limps to the stickman
                            currentLettersRight = printWord(currentLettersGuessed, randomWord);
                            Console.Write("\r\n");
                            printLines(randomWord);// prints lines underneath the word
                        }
                    }
                }
            }
                Console.WriteLine("\r\nGame is over have a nice day :) ");
        }
    }
}


![image](https://user-images.githubusercontent.com/98741878/185410143-40a225af-e848-4a90-a831-dd0b0316bd18.png)



![image](https://user-images.githubusercontent.com/98741878/185410437-416d1995-f7b6-424a-a352-9a55fb5bfa83.png)


![image](https://user-images.githubusercontent.com/98741878/185410506-89bd7b04-dc75-47d6-9fcb-0ddd802270e6.png)



