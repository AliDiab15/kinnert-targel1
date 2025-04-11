/*
* ali diab || עלי דיאב
* 326149762
* HW01
* */
import java.util.*;

public class WordCalculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter the expression:");
        String input = scanner.nextLine().trim().toLowerCase();
        scanner.close();

        Map<String, Integer> numbers = new HashMap<>();
        numbers.put("zero", 0);   numbers.put("one", 1);
        numbers.put("two", 2);    numbers.put("three", 3);
        numbers.put("four", 4);   numbers.put("five", 5);
        numbers.put("six", 6);    numbers.put("seven", 7);
        numbers.put("eight", 8);  numbers.put("nine", 9);
        numbers.put("ten", 10);

        Map<String, String> ops = new HashMap<>();
        ops.put("plus", "+");
        ops.put("minus", "-");
        ops.put("times", "*");
        ops.put("divided", "/");

        String[] words = input.split(" ");
        int[] values = new int[100];
        String[] operations = new String[99];
        int valueIndex = 0, opIndex = 0;

        for (int i = 0; i < words.length;) {
            if (numbers.containsKey(words[i])) {
                values[valueIndex++] = numbers.get(words[i]);
                i++;
            } else if (i + 1 < words.length && words[i].equals("divided") && words[i + 1].equals("by")) {
                operations[opIndex++] = "/";
                i += 2;
            } else if (ops.containsKey(words[i])) {
                operations[opIndex++] = ops.get(words[i]);
                i++;
            } else {
                System.out.println("Invalid input!");
                return;
            }
        }
        for (int i = 0; i < opIndex; i++) {
            if (operations[i].equals("*") || operations[i].equals("/")) {
                int a = values[i];
                int b = values[i + 1];
                int result = operations[i].equals("*") ? a * b : a / b;
                values[i] = result;
                for (int j = i + 1; j < valueIndex - 1; j++) {
                    values[j] = values[j + 1];
                }
                valueIndex--;

                // نزيح العمليات
                for (int j = i; j < opIndex - 1; j++) {
                    operations[j] = operations[j + 1];
                }
                opIndex--;
                i--;
            }
        }
        int result = values[0];
        for (int i = 0; i < opIndex; i++) {
            if (operations[i].equals("+")) {
                result += values[i + 1];
            } else if (operations[i].equals("-")) {
                result -= values[i + 1];
            }
        }

        System.out.println("The result of '" + input + "' is: " + result);
    }
}
/*C:\Users\Admin\.jdks\openjdk-23.0.2\bin\java.exe "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2024.3.5\lib\idea_rt.jar=57026" -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath "C:\Users\Admin\Desktop\HW of Java Langu\Main.java\out\production\Main.java" Main
Enter the expression:
eight divided by two plus seven plus two times three minus one
The result of 'eight divided by two plus seven plus two times three minus one' is: 16

Process finished with exit code 0
*/
