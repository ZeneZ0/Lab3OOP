# Lab3OOP
#Файл Main:
public class Main {
    public static void main(String[] args) {
        Menu.start();
    }
}
#Файл Menu:
import java.util.Scanner;
public class Menu {
    private static TextUtils textUtils = new TextUtils();
    private static final ArrayUtils arrayUtils = new ArrayUtils();
    private static final FileHandler fileHandler = new FileHandler();
    private static final Scanner scanner = new Scanner(System.in);

    public static void start() {
        while (true) {
            try {
                showMainMenu();
                int choice = getChoice();

                switch (choice) {
                    case 1:
                        handleTextMenu();
                        break;
                    case 2:
                        handleArrayMenu();
                        break;
                    case 3:
                        System.out.println("Программа завершена.");
                        return;
                    default:
                        System.out.println("Неверный выбор. Попробуйте снова.");
                }
            } catch (TextOnlyDigitsException e) {
                System.out.println("Ошибка: Текст должен содержать буквы, а не только цифры.");
            } catch (NumberFormatException e) {
                System.out.println("Ошибка: Введите число!");
            } catch (Exception e) {
                System.out.println("Произошла ошибка: " + e.getMessage());
            }
        }
    }

    private static void showMainMenu() {
        System.out.println("\nГлавное меню:");
        System.out.println("1. Работа с текстом");
        System.out.println("2. Работа с массивом");
        System.out.println("3. Выход");
        System.out.print("Выберите пункт меню: ");
    }

    private static void handleTextMenu() {
        while (true) {
            try {
                showTextMenu();
                int choice = getChoice();

                switch (choice) {
                    case 1:
                        inputTextFromConsole();
                        break;
                    case 2:
                        loadTextFromFile();
                        break;
                    case 3:
                        saveTextToFile();
                        break;
                    case 4:
                        showText();
                        break;
                    case 5:
                        showSentenceCount();
                        break;
                    case 6:
                        showMostFrequentWord();
                        break;
                    case 7:
                        showLetterStatistics();
                        break;
                    case 8:
                        return;
                    default:
                        System.out.println("Неверный выбор. Попробуйте снова.");
                }
            } catch (Exception e) {
                System.out.println("Произошла ошибка: " + e.getMessage());
            }
        }
    }

    private static void handleArrayMenu() {
        while (true) {
            try {
                showArrayMenu();
                int choice = getChoice();

                switch (choice) {
                    case 1:
                        inputArrayFromConsole();
                        break;
                    case 2:
                        loadArrayFromFile();
                        break;
                    case 3:
                        saveArrayToFile();
                        break;
                    case 4:
                        showArray();
                        break;
                    case 5:
                        showArrayWithoutDuplicates();
                        break;
                    case 6:
                        return;
                    default:
                        System.out.println("Неверный выбор. Попробуйте снова.");
                }
            } catch (Exception e) {
                System.out.println("Произошла ошибка: " + e.getMessage());
            }
        }
    }

    private static void showTextMenu() {
        System.out.println("\nМеню работы с текстом:");
        System.out.println("1. Ввести текст с консоли");
        System.out.println("2. Загрузить текст из файла");
        System.out.println("3. Сохранить текст в файл");
        System.out.println("4. Показать текст");
        System.out.println("5. Показать количество предложений");
        System.out.println("6. Показать самое частое слово");
        System.out.println("7. Показать статистику по первым буквам");
        System.out.println("8. Вернуться в главное меню");
        System.out.print("Выберите пункт меню: ");
    }

    private static void showArrayMenu() {
        System.out.println("\nМеню работы с массивом:");
        System.out.println("1. Ввести массив с консоли");
        System.out.println("2. Загрузить массив из файла");
        System.out.println("3. Сохранить массив в файл");
        System.out.println("4. Показать массив");
        System.out.println("5. Удалить дубликаты");
        System.out.println("6. Вернуться в главное меню");
        System.out.print("Выберите пункт меню: ");
    }

    private static int getChoice() {
        return Integer.parseInt(scanner.nextLine());
    }

    private static void showText() {
        if (textUtils.getText().isEmpty()) {
            System.out.println("Текст пуст. Сначала введите или загрузите текст.");
        } else {
            System.out.println("\nТекущий текст:");
            System.out.println(textUtils.getText());
        }
    }

    private static void showArray() {
        int[] currentArray = arrayUtils.getNumbers();
        if (currentArray == null || currentArray.length == 0) {
            System.out.println("Массив пуст. Сначала введите или загрузите массив.");
        } else {
            System.out.println("\nТекущий массив:");
            for (int number : currentArray) {
                System.out.print(number + " ");
            }
            System.out.println();
        }
    }

    private static void inputTextFromConsole() {
        System.out.print("Введите текст: ");
        String inputText = scanner.nextLine();
        textUtils = new TextUtils(inputText);
        System.out.println("Текст успешно введен");
    }

    private static void loadTextFromFile() {
        try {
            System.out.print("Введите имя файла: ");
            String fileName = scanner.nextLine();
            String text = fileHandler.readFromFile(fileName);
            textUtils.setText(text);
            System.out.println("Текст успешно загружен");
        } catch (Exception e) {
            System.out.println("Ошибка при чтении файла: " + e.getMessage());
        }
    }

    private static void saveTextToFile() {
        try {
            System.out.print("Введите имя файла: ");
            String fileName = scanner.nextLine();
            fileHandler.writeToFile(fileName, textUtils.getText());
            System.out.println("Текст успешно сохранен");
        } catch (Exception e) {
            System.out.println("Ошибка при сохранении файла: " + e.getMessage());
        }
    }

    private static void showSentenceCount() {
        System.out.println("Количество предложений: " + textUtils.countSentence());
    }

    private static void showMostFrequentWord() {
        System.out.println("Самое частое слово: " + textUtils.mostFreqntWord());
    }

    private static void showLetterStatistics() {
        System.out.println("Слов на гласную: " + textUtils.firstLetrVowel());
        System.out.println("Слов на согласную: " + textUtils.firstLetrConsonant());
    }

    private static void inputArrayFromConsole() {
        try {
            System.out.print("Введите числа через пробел: ");
            String input = scanner.nextLine();
            int[] numbers = parseArray(input);
            arrayUtils.setNumbers(numbers);
            System.out.println("Массив успешно введен");
        } catch (NumberFormatException e) {
            System.out.println("Ошибка: Введите корректные числа!");
        }
    }

    private static void loadArrayFromFile() {
        try {
            System.out.print("Введите имя файла: ");
            String fileName = scanner.nextLine();
            int[] numbers = fileHandler.readArrayFromFile(fileName);
            arrayUtils.setNumbers(numbers);
            System.out.println("Массив успешно загружен");
        } catch (Exception e) {
            System.out.println("Ошибка при чтении файла: " + e.getMessage());
        }
    }

    private static void saveArrayToFile() {
        try {
            System.out.print("Введите имя файла: ");
            String fileName = scanner.nextLine();
            fileHandler.writeArrayToFile(fileName, arrayUtils.removeDuplicates());
            System.out.println("Массив успешно сохранен");
        } catch (Exception e) {
            System.out.println("Ошибка при сохранении файла: " + e.getMessage());
        }
    }

    private static void showArrayWithoutDuplicates() {
        System.out.println("Массив без дубликатов:");
        for (int number : arrayUtils.removeDuplicates()) {
            System.out.print(number + " ");
        }
        System.out.println();
    }

    private static int[] parseArray(String input) {
        String[] parts = input.trim().split("\\s+");
        int[] numbers = new int[parts.length];
        for (int i = 0; i < parts.length; i++) {
            numbers[i] = Integer.parseInt(parts[i]);
        }
        return numbers;
    }
}
#Файл FileHandler:
import java.io.*;
import java.nio.charset.StandardCharsets;

public class FileHandler {
    public String readFromFile(String fileName) throws IOException {
        StringBuilder content = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(
                new InputStreamReader(new FileInputStream(fileName), StandardCharsets.UTF_8))) {
            String line;
            while ((line = reader.readLine()) != null) {
                content.append(line).append("\n");
            }
        }
        return content.toString();
    }

    public void writeToFile(String fileName, String content) throws IOException {
        try (BufferedWriter writer = new BufferedWriter(
                new OutputStreamWriter(new FileOutputStream(fileName), StandardCharsets.UTF_8))) {
            writer.write(content);
        }
    }

    public int[] readArrayFromFile(String fileName) throws IOException {
        try (BufferedReader reader = new BufferedReader(
                new InputStreamReader(new FileInputStream(fileName), StandardCharsets.UTF_8))) {
            String[] numbers = reader.readLine().split("\\s+");
            int[] array = new int[numbers.length];
            for (int i = 0; i < numbers.length; i++) {
                array[i] = Integer.parseInt(numbers[i]);
            }
            return array;
        }
    }

    public void writeArrayToFile(String fileName, int[] array) throws IOException {
        try (BufferedWriter writer = new BufferedWriter(
                new OutputStreamWriter(new FileOutputStream(fileName), StandardCharsets.UTF_8))) {
            StringBuilder content = new StringBuilder();
            for (int number : array) {
                content.append(number).append(" ");
            }
            writer.write(content.toString().trim());
        }
    }
}

#Файл TextUtils:
public class TextUtils implements Cloneable {
    private String text;

    public TextUtils() {
        this.text = "";
    }

    public TextUtils(String text) {
        validateText(text);
        this.text = text;
    }

    private static void validateText(String text) {
        if (text == null || text.trim().isEmpty()) {
            throw new TextOnlyDigitsException();
        }

        boolean hasLetters = false;
        boolean hasOnlyDigitsAndPunctuation = true;

        for (int i = 0; i < text.length(); i++) {
            char c = text.charAt(i);

            // Проверка на буквы (русские и английские)
            if ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z') ||
                    (c >= 'а' && c <= 'я') || (c >= 'А' && c <= 'Я') || c == 'ё' || c == 'Ё') {
                hasLetters = true;
                hasOnlyDigitsAndPunctuation = false;
                break;
            }
        }

        if (!hasLetters || hasOnlyDigitsAndPunctuation) {
            throw new TextOnlyDigitsException();
        }
    }

    public int countSentence() {
        int count = 0;
        for (int i = 0; i < text.length(); i++) {
            if (text.charAt(i) == '.' || text.charAt(i) == '!' || text.charAt(i) == '?') {
                count++;
            }
        }
        return count;
    }

    public String mostFreqntWord() {
        String[] words = text.toLowerCase().split("[\\s.,!?;:]+");
        int[] wordCounts = new int[words.length];
        int maxCount = 0;
        int maxIndex = 0;

        for (int i = 0; i < words.length; i++) {
            if (!words[i].isEmpty()) {
                for (int j = 0; j < words.length; j++) {
                    if (words[i].equals(words[j])) {
                        wordCounts[i]++;
                    }
                }
                if (wordCounts[i] > maxCount) {
                    maxCount = wordCounts[i];
                    maxIndex = i;
                }
            }
        }
        return words[maxIndex];
    }

    public int firstLetrVowel() {
        String[] words = text.toLowerCase().split("[\\s.,!?;:]+");
        int vowelCount = 0;

        for (String word : words) {
            if (!word.isEmpty() && isVowel(word.charAt(0))) {
                vowelCount++;
            }
        }
        return vowelCount;
    }

    public int firstLetrConsonant() {
        String[] words = text.toLowerCase().split("[\\s.,!?;:]+");
        int consonantCount = 0;

        for (String word : words) {
            if (!word.isEmpty() && !isVowel(word.charAt(0))) {
                consonantCount++;
            }
        }
        return consonantCount;
    }

    private boolean isVowel(char ch) {
        return "аеёиоуыэюя".indexOf(ch) != -1;
    }

    public String getText() {
        return text;
    }

    public void setText(String text) {
        validateText(text);
        this.text = text;
    }

    public TextUtils clone() {
        try {
            return (TextUtils) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}
#Файл ArrayUtils:
import java.util.Arrays;

public class ArrayUtils implements Cloneable {
    private int[] numbers;

    public ArrayUtils() {
        this.numbers = new int[0];
    }

    public ArrayUtils(int[] numbers) {
        this.numbers = numbers;
    }

    public int[] removeDuplicates() {
        int[] uniqueNumbers = new int[numbers.length];
        int count = 0;

        for (int i = 0; i < numbers.length; i++) {
            boolean isDuplicate = false;

            for (int j = 0; j < i; j++) {
                if (numbers[i] == numbers[j]) {
                    isDuplicate = true;
                    break;
                }
            }

            if (!isDuplicate) {
                uniqueNumbers[count++] = numbers[i];
            }
        }

        return Arrays.copyOf(uniqueNumbers, count);
    }

    public void setNumbers(int[] numbers) {
        this.numbers = numbers;
    }

    @Override
    public ArrayUtils clone() {
        try {
            ArrayUtils cloned = (ArrayUtils) super.clone();
            cloned.numbers = numbers.clone();
            return cloned;
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
    public int[] getNumbers() {
        return numbers;
    }
}
#Exception TextOnlyDigitsException:
class TextOnlyDigitsException extends RuntimeException {
  public TextOnlyDigitsException() {
    super("Tекст должен содержать не только цифры, но и буквы.");
  }
}
