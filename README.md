import java.math.BigDecimal;
import java.util.Scanner;

public class FinancialTracker {
    static BigDecimal[] expenses = new BigDecimal[30]; 

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int choice;
        do {
            System.out.println("\n1. Ввести расходы за день");
            System.out.println("2. Показать все расходы за месяц");
            System.out.println("3. Показать самую большую сумму расхода за месяц");
            System.out.println("4. Выйти");
            System.out.print("Выберите действие: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    enterExpenses(scanner);
                    break;
                case 2:
                    displayExpenses();
                    break;
                case 3:
                    displayMaxExpense();
                    break;
                case 4:
                    System.out.println("Программа завершена.");
                    break;
                default:
                    System.out.println("Неверный выбор. Попробуйте еще раз.");
            }
        } while (choice != 4);
        
        scanner.close();
    }

    public static void enterExpenses(Scanner scanner) {
        System.out.print("Введите день (1-30): ");
        int day = scanner.nextInt();
        if (day < 1 || day > 30) {
            System.out.println("Неверный день. Введите число от 1 до 30.");
            return;
        }
        
        System.out.print("Введите сумму трат: ");
        BigDecimal amount = scanner.nextBigDecimal();

        if (expenses[day - 1] != null) {
            System.out.print("Траты для этого дня уже введены. Хотите перезаписать сумму? (1 - да/2 - нет): ");
            String answer = scanner.next();
            if (!answer.equalsIgnoreCase("да")) {
                return;
            }
        }

        expenses[day - 1] = amount;
        System.out.println("Траты успешно сохранены для дня " + day);
    }

    public static void displayExpenses() {
        System.out.println("\nРасходы за месяц:");
        for (int i = 0; i < expenses.length; i++) {
            if (expenses[i] != null) {
                System.out.println("День " + (i + 1) + ": " + expenses[i]);
            }
        }
    }

    public static void displayMaxExpense() {
        BigDecimal maxExpense = BigDecimal.ZERO;
        int maxDay = -1;

        for (int i = 0; i < expenses.length; i++) {
            if (expenses[i] != null && expenses[i].compareTo(maxExpense) > 0) {
                maxExpense = expenses[i];
                maxDay = i + 1;
            }
        }

        if (maxDay != -1) {
            System.out.println("\nСамая большая сумма расхода за месяц: " + maxExpense + " в день " + maxDay);
        } else {
            System.out.println("Расходы за месяц еще не найдены.");
        }
    }
}
