import java.util.HashSet;
import java.util.Random;
import java.util.Scanner;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Input the length of the secret code:");
        int codeLength;
        try {
            codeLength = Integer.parseInt(scanner.nextLine());
        } catch (NumberFormatException e) {
            System.out.println("Error: Invalid input. Please enter a valid number.");
            return;
        }

        System.out.println("Input the number of possible symbols in the code:");
        int numPossibleSymbols;
        try {
            numPossibleSymbols = Integer.parseInt(scanner.nextLine());
        } catch (NumberFormatException e) {
            System.out.println("Error: Invalid input. Please enter a valid number.");
            return;
        }

        if (codeLength <= 0 || codeLength > 36 || numPossibleSymbols <= 0 || numPossibleSymbols > 36) {
            System.out.println("Error: Invalid input. Code length and number of possible symbols should be between 1 and 36.");
            return;
        }

        if (codeLength > numPossibleSymbols) {
            System.out.printf("Error: It's not possible to generate a code with a length of %d with %d unique symbols.%n", codeLength, numPossibleSymbols);
            return;
        }

        String secretCode = generateSecretCode(codeLength, numPossibleSymbols);
        System.out.printf("The secret is prepared: %s (%s).%n", "*".repeat(codeLength), getSymbolRange(numPossibleSymbols));
        System.out.println("Okay, let's start a game!");

        int numOfGuesses = 0;
        while (true) {
            numOfGuesses++;
            System.out.printf("Turn %d:%n", numOfGuesses);
            String guess = scanner.nextLine();
            int[] result = gradeGuess(guess, secretCode);
            System.out.printf("Grade: %d bull(s) and %d cow(s)%n", result[0], result[1]);
            if (result[0] == codeLength) {
                System.out.println("Congratulations! You guessed the secret code.");
                break;
            }
        }
        System.out.printf("You made %d guesses.%n", numOfGuesses);
    }

    public static String generateSecretCode(int length, int numPossibleSymbols) {
        Random random = new Random();
        Set<Character> uniqueSymbols = new HashSet<>();
        StringBuilder codeBuilder = new StringBuilder();

        while (uniqueSymbols.size() < length) {
            char symbol = getRandomSymbol(random, numPossibleSymbols);
            if (uniqueSymbols.add(symbol)) {
                codeBuilder.append(symbol);
            }
        }
        return codeBuilder.toString();
    }

    private static char getRandomSymbol(Random random, int numPossibleSymbols) {
        int randomNumber = random.nextInt(numPossibleSymbols);
        if (randomNumber < 10) {
            return (char) ('0' + randomNumber);
        } else {
            return (char) ('a' + (randomNumber - 10));
        }
    }

    private static String getSymbolRange(int numPossibleSymbols) {
        StringBuilder range = new StringBuilder("0-9");
        for (char ch = 'a'; ch < 'a' + numPossibleSymbols - 10; ch++) {
            range.append(", ").append(ch);
        }
        return range.toString();
    }

    public static int[] gradeGuess(String guess, String secretCode) {
        int bulls = 0;
        int cows = 0;
        for (int i = 0; i < secretCode.length(); i++) {
            char ch = secretCode.charAt(i);
            if (guess.charAt(i) == ch) {
                bulls++;
            } else if (secretCode.indexOf(guess.charAt(i)) != -1) {
                cows++;
            }
        }
        return new int[]{bulls, cows};
    }
}
