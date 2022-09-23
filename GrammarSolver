// Jasarjan Singh
// CSE 143
// TA: Himani Nijhawan
// Assesment #4 GrammarSolver
// This program generates random sentences (or other output) 
// from a set of specially-formatted rules (grammar)
import java.util.*;

public class GrammarSolver {

    private SortedMap<String, String[]> grammarRules;

    // pre: the List parameter, rules, needs to be in BNF format 
    //      throws an IllegalArgumentException if the list 
    //      is empty or if there are two or more entries 
    //      in the grammar for the same non-terminal.
    // post: initialize a new grammar over the given BNF grammar 
    //       rules where each rule corresponds to one line of text.
    public GrammarSolver(List<String> rules) {
        if (rules.isEmpty()) {
            throw new IllegalArgumentException();
        }
        grammarRules = new TreeMap<>();
        for (String word: rules) { 
            String[] seperate = word.split("::=");
            String nonTerminal = seperate[0];
            seperate = seperate[1].split("\\|");
            if (grammarRules.containsKey(nonTerminal)) {
                throw new IllegalArgumentException();
            }
            grammarRules.put(nonTerminal, seperate);
        }
    }

    // post: returns true if the given symbol is a 
    //       non-terminal in the grammar and false otherwise
    public boolean grammarContains(String symbol) {
        return grammarRules.containsKey(symbol);
    }

    // post: returns a string representation of the various 
    //       non-terminal symbols from the grammar as a sorted, 
    //       comma-separated list enclosed in square brackets
    public String getSymbols() {
        return grammarRules.keySet().toString();
    }

    // pre: throws an IllegalArgumentException if times is 
    //      negative or if the symbol is not a non-terminal
    // post: generate times random occurrences of the 
    //       given symbol and return them in a String[]
    public String[] generate(String symbol, int times) {
        if (!grammarContains(symbol) || times < 0) {
            throw new IllegalArgumentException();
        }
        String[] s = new String[times];
        for (int i = 0; i < times; i++) {
            s[i] = generateString(symbol);
        }
        return s;
    }

    // pre: throws an IllegalArgumentException if the given  
    //      String symbol is not a non-terminal
    // post: generates random occurrences of the given String symbol
    //       and returns random strings of non-terminal symbols 
    private String generateString(String symbol) {
        if(!grammarContains(symbol)) {
            return symbol;
        }
        Random r = new Random();
        String result = "";
        String[] rules = grammarRules.get(symbol);
        int n = r.nextInt(rules.length);
        String[] rule = rules[n].trim().split("\\s+");
        for(int i = 0; i < rule.length; i++) {
            result += generateString(rule[i]) + " ";
        }
        return result.trim();
    }
}
