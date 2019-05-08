# JavaCode

import java.util.stream.IntStream;

public class Main {

    static int max = 0;
    static int min = 100;
    static int entet = 7;

    public static void main(String[] args) {
        int[] randomArr = new int[101];
        int[] arr = new int[80];
        int random = 0;

        for (int ii = 0; ii < arr.length; ii++) {
            for (int i = 0; i < randomArr.length; i++) {
                randomArr[i] = Main.rand();

            }
            random = IntStream.of(randomArr).sum();
            arr[ii] = random;
        }

        for (int i = 0; i < arr.length; i++) {
            if(max < arr[i]) {
                max = arr[i];
            }
            if(min > arr[i]) {
                min = arr[i];
            }
        }

        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
            if(i == entet) {
                System.out.println();
                entet += 8;
            }

        }
        System.out.println('\n');
        System.out.println("Минимальное число: " + min);
        System.out.println("Максимальное число: " + max + '\n');

        Main.arraySort(arr);
        System.out.println("Сортированиный массив: " + '\n');
        entet = 7;
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
            if (i == entet) {
                System.out.println();
                entet += 8;
            }
        }
    }

    public static int rand() {
        int ran = 0;
        double r = Math.random();
        if(r <= 0.5) {
            ran = 0;
        }
        if(r >= 0.51) {
            ran = 1;
        }
        return ran;

    }
    public static void arraySort(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            int min = arr[i];
            int min_i = i;

            for (int j = i+1; j < arr.length; j++) {
                if (arr[j] < min) {
                    min = arr[j];
                    min_i = j;
                }
            }

            if (i != min_i) {
                int tmp = arr[i];
                arr[i] = arr[min_i];
                arr[min_i] = tmp;
            }
        }
    }
}
