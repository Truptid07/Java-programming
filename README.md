# Java-programming task 1

import java.util.Random;
import java.util.Scanner;

public class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        int score = 0;
        int roundsPlayed = 0;
        
        while (true) {
            roundsPlayed++;
            int lowerBound = 1;
            int upperBound = 100;
            int numberToGuess = random.nextInt(upperBound - lowerBound + 1) + lowerBound;
            int maxAttempts = 10;
            int attempts = 0;
            boolean guessedCorrectly = false;
            
            System.out.println("Guess the number between " + lowerBound + " and " + upperBound + ". You have " + maxAttempts + " attempts.");
            
            while (attempts < maxAttempts) {
                System.out.print("Enter your guess: ");
                if (!scanner.hasNextInt()) {
                    System.out.println("Invalid input. Please enter a number.");
                    scanner.next(); // Clear invalid input
                    continue;
                }
                int guess = scanner.nextInt();
                attempts++;
                
                if (guess < numberToGuess) {
                    System.out.println("Too low!");
                } else if (guess > numberToGuess) {
                    System.out.println("Too high!");
                } else {
                    System.out.println("Congratulations! You guessed the number in " + attempts + " attempts.");
                    guessedCorrectly = true;
                    score += maxAttempts - attempts + 1; // Score based on remaining attempts
                    break;
                }
                
                System.out.println("Remaining attempts are: " + (maxAttempts - attempts));
            }
            
            if (!guessedCorrectly) {
                System.out.println("Sorry, you've run out of attempts. The number was " + numberToGuess + ".");
            }
            
            System.out.print("Do you want to play again? (yes/no): ");
            scanner.nextLine(); // Consume newline
            String playAgain = scanner.nextLine().trim().toLowerCase();
            if (!playAgain.equals("yes")) {
                break;
            }
        }
        
        System.out.println("Game over! You played " + roundsPlayed + " rounds and scored " + score + " points.");
        scanner.close();
    }
}
