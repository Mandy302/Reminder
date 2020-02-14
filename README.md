/* This program is design for customer that when they enter the date, the program will pop-up which product at home is about to expire.

*/

import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Scanner;
import java.util.Set;
class Reminder {

    private Food food;
    private Date date;
    private List<Reminder> reminderList;

    public Reminder() {
        reminderList = new ArrayList<>();
    }

    public Reminder(Food food, Date date) {
        this.date = date;
        this.food = food;
    }

    private class Date implements Comparable<Date> {
        private final int day;
        private final int month;
        private final int year;

        public Date(int month, int day, int year) {
            this.day = day;
            this.month = month;
            this.year = year;
        }

        public int compareTo(Date antoherDay) {
            if (year < antoherDay.year) return -1;
            else if (month < antoherDay.month) return -1;
            else return Integer.compare(day, antoherDay.day);
        }

        public String toString() {
            StringBuilder sb = new StringBuilder();
            if (month < 10) sb.append('0');
            sb.append(month);
            if (day < 10) sb.append('0');
            sb.append(day);
            sb.append(year);
            return sb.toString();
        }
    }

    private class Food implements Comparable<Food> {
        private String name;

        public Food(String name) {
            this.name = name;
        }

        public int compareTo(Food anohterFood) {
            return CharSequence.compare(name, anohterFood.name);
        }

        public String getName() {
            return name;
        }
    }

    private void add(String name, int month, int day, int year) {
        reminderList.add(new Reminder(new Food(name), new Date(day, month, year)));
    }

    private void print() {
        for (Reminder query : reminderList) {
            System.out.println(query.toString());
        }
        System.out.println();
    }

    public String toString() {
        return food.getName() + "  Expire by " + date.toString();
    }

    public void start() {
        while (true) {
            Scanner sca = new Scanner(System.in);
            String str = "";
            Set<Character> validOper = new HashSet<>();
            validOper.add('S');
            validOper.add('A');
            validOper.add('C');
            validOper.add('E');

            do {
                System.out.println("Welcome to Reminder.\n"
                                           + "To show the current Reminder<S>,  "
                                           + "To add items<A>,  "
                                           + "To clean the Reminder<C>,  "
                                           + "Exit<E>.");
                str = sca.next();
            } while (str.length() != 1 || !validOper.contains(str.charAt(0)));
            char oper = str.charAt(0);
            if (oper == 'E') break;

            switch (oper) {
                case 'S':
                    print();
                    break;
                case 'A':
                    System.out.println("Enter an item name, expired day, month, and year.");
                    str = sca.next();
                    int day = sca.nextInt();
                    int month = sca.nextInt();
                    int year = sca.nextInt();
                    add(str, day, month, year);
                    break;
                case 'C':
                    reminderList = new ArrayList<>();
                    break;
            }
        }
    }

    public static void main(String[] args) {
        Reminder r = new Reminder();
        r.start();
    }
}
