import java.util.HashMap;
import java.util.Map;
import java.util.Set;
import java.util.HashSet;
import java.util.Vector;
import java.util.Arrays;

public class Main {

    public static void taskTotalCombination(Vector<Integer> Die1, Vector<Integer> Die2) {
        int totalCombination = Die1.size() * Die2.size();
        System.out.println("Total Combination : Size of Die1 X Size of Die2: " + totalCombination);
        System.out.println();
    }

    public static void taskCombinationsPossible(Vector<Integer> Die1, Vector<Integer> Die2) {
        System.out.println("All Possible Combinations:");
        System.out.println();

        for (int i = 1; i <= Die1.size(); i++) {
            for (int j = 1; j <= Die2.size(); j++) {
                System.out.print("(" + i + "," + j + ") ");
            }
            System.out.println();
        }

        System.out.println();
    }

    public static void taskProbability(Vector<Integer> Die1, Vector<Integer> Die2) {
        System.out.println("All Possible Sums:");
        System.out.println();

        Map<Integer, Float> combination = new HashMap<>();
        Set<Integer> unique = new HashSet<>();
        Map<Integer, Vector<Vector<Integer>>> values = new HashMap<>();

        for (int i = 0; i < Die1.size(); i++) {
            for (int j = 0; j < Die2.size(); j++) {
                Vector<Integer> val = new Vector<>();
                val.add(i + 1);
                val.add(j + 1);

                int sum = Die1.get(i) + Die2.get(j);

                values.computeIfAbsent(sum, k -> new Vector<>()).add(val);

                if (!unique.contains(sum)) {
                    System.out.print(sum + " ");
                }
                unique.add(sum);
                combination.put(sum, combination.getOrDefault(sum, 0f) + 1);
            }
        }
        System.out.println();
        System.out.println();

        System.out.println("Combinations for Each Sum:");
        System.out.println();

        for (Map.Entry<Integer, Vector<Vector<Integer>>> entry : values.entrySet()) {
            System.out.print("Sum " + entry.getKey() + ": ");
            for (Vector<Integer> v : entry.getValue()) {
                System.out.print("(" + v.get(0) + ", " + v.get(1) + ") ");
            }
            System.out.println();
        }
        System.out.println();

        int totalCombination = Die1.size() * Die2.size();

        System.out.println("Probability of All Possible Sums:");
        System.out.println();

        for (Map.Entry<Integer, Float> entry : combination.entrySet()) {
            System.out.print("probability(sum=" + entry.getKey() + ")= ");
            System.out.print(entry.getValue() + "(occurrence)/" + totalCombination + "(total combination)= ");
            float probability = entry.getValue() / totalCombination;
            System.out.println(probability);
        }
    }

    public static void main(String[] args) {
        Vector<Integer> Die1 = new Vector<>(Arrays.asList(1, 2, 3, 4, 5, 6));
        Vector<Integer> Die2 = new Vector<>(Arrays.asList(1, 2, 3, 4, 5, 6));

        taskTotalCombination(Die1, Die2);
        taskCombinationsPossible(Die1, Die2);
        taskProbability(Die1, Die2);
    }
}
