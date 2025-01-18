import java.security.SecureRandom;
import java.util.Scanner;

public class RandomPasswordGenerator {

    // Define the characters allowed in the password
    private static final String UPPERCASE_LETTERS = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    private static final String LOWERCASE_LETTERS = "abcdefghijklmnopqrstuvwxyz";
    private static final String DIGITS = "0123456789";
    private static final String SPECIAL_CHARACTERS = "!@#$%^&*()-_=+<>?/";
    private static final String ALL_CHARACTERS = UPPERCASE_LETTERS + LOWERCASE_LETTERS + DIGITS + SPECIAL_CHARACTERS;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Ask the user for the desired password length
        System.out.print("Enter the desired password length: ");
        int length = scanner.nextInt();
        
        // Generate the password
        String password = generatePassword(length);
        System.out.println("Generated Password: " + password);

        scanner.close();
    }

    private static String generatePassword(int length) {
        // Use SecureRandom for better randomness
        SecureRandom random = new SecureRandom();
        StringBuilder password = new StringBuilder(length);

        // Ensure the password contains at least one character from each category
        password.append(UPPERCASE_LETTERS.charAt(random.nextInt(UPPERCASE_LETTERS.length())));
        password.append(LOWERCASE_LETTERS.charAt(random.nextInt(LOWERCASE_LETTERS.length())));
        password.append(DIGITS.charAt(random.nextInt(DIGITS.length())));
        password.append(SPECIAL_CHARACTERS.charAt(random.nextInt(SPECIAL_CHARACTERS.length())));

        // Fill the remaining length with random characters from all categories
        for (int i = 4; i < length; i++) {
            password.append(ALL_CHARACTERS.charAt(random.nextInt(ALL_CHARACTERS.length())));
        }

        // Shuffle the password to make it more random
        return shuffleString(password.toString());
    }

    private static String shuffleString(String input) {
        SecureRandom random = new SecureRandom();
        char[] characters = input.toCharArray();

        for (int i = characters.length - 1; i > 0; i--) {
            int index = random.nextInt(i + 1);
            // Swap characters
            char temp = characters[i];
            characters[i] = characters[index];
            characters[index] = temp;
        }

        return new String(characters);
    }
}

