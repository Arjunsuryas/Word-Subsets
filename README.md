# Word-Subsets
In_java
import java.util.*;
public class Solution {
    public List<String> wordSubsets(String[] words1, String[] words2) {
        int[] required = new int[26]; 
        for (String word : words2) {
            int[] wordCount = new int[26]; 
            for (char c : word.toCharArray()) {
                wordCount[c - 'a']++; 
            }
            for (int i = 0; i < 26; i++) {
                required[i] = Math.max(required[i], wordCount[i]);
            }
        }

        List<String> result = new ArrayList<>();
        for (String word : words1) {
            int[] wordCount = new int[26]; 
            for (char c : word.toCharArray()) {
                wordCount[c - 'a']++; 
            }
            boolean isUniversal = true;
            for (int i = 0; i < 26; i++) {
                if (required[i] > 0 && wordCount[i] < required[i]) {
                    isUniversal = false;
                    break;
                }
            }
            if (isUniversal) {
                result.add(word);
            }
        }

        return result;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        String[] words1 = {"amazon", "apple", "facebook", "google", "leetcode"};
        String[] words2 = {"e", "o"};
        System.out.println(solution.wordSubsets(words1, words2)); 
        String[] words1_2 = {"amazon", "apple", "facebook", "google", "leetcode"};
        String[] words2_2 = {"l", "e"};
        System.out.println(solution.wordSubsets(words1_2, words2_2));
    }
}
