import java.util.stream.IntStream;

public class Main {
    static int max = 0;
    static int min = 100;
    static int entet = 7;
    static int average;
    static float averageFloat;
    static float sigma = 0;

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
            if (max < arr[i]) {
                max = arr[i];
            }
            if (min > arr[i]) {
                min = arr[i];
            }
        }

        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
            if (i == entet) {
                System.out.println();
                entet += 8;
            }

        }
        System.out.println('\n');

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

        average = IntStream.of(arr).sum();
        averageFloat = (float) average;
        averageFloat = averageFloat / 80;
        System.out.println('\n');
        System.out.println("Среднее арифметическое: " + averageFloat);
        System.out.println("Минимальное число: " + min);
        System.out.print("Максимальное число: " + max + '\n');
        System.out.println("Размах ряда: " + (max - min));
        System.out.println("Мода: " + mostPopular(arr));
        for (int i = 0; i < arr.length; i++) {
            float temp;
            temp = 50 - arr[i];
            temp = temp * temp;
            sigma += temp;
        }
        
        sigma = sigma / 50;
        float radicalOfSigma = sigma;

        System.out.println("Дисперсия по выборке: " + (sigma));
        System.out.println("Среднеквадратичное отклонение: " + radical(radicalOfSigma));

    }


    public static double radical(float number) {
        double t;
        double squareRoot = number / 2;
        do {
            t = squareRoot;
            squareRoot = (t + (number / t)) / 2;
        } while ((t - squareRoot) != 0);
        return squareRoot;
    }

    public static int rand() {
        int ran = 0;
        double r = Math.random();
        if(r < 0.5) {
            ran = 0;
        }
        if(r > 0.5) {
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

    public static int mostPopular(int[] array) {
        if (array == null || array.length == 0) {
            return 0;
        }
        arraySort(array);

        int prev = array[0];
        int popular = array[0];
        int count = 1;
        int maxCount = 1;

        for (int i = 1; i < array.length; i++) {
            if (array[i] == prev) {
                count++;
            } else {
                if (count > maxCount) {
                    popular = array[i - 1];
                    maxCount = count;
                }
                prev = array[i];
                count = 1;
            }
        }
        return count > maxCount ? array[array.length - 1] : popular;
    }
}
