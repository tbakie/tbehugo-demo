+++
title = "Showcase"
date = "2023-10-16T11:02:08-07:00"
author = " Efesoy "
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = false
hideComments = false
color = "red" 
+++
# In this assessment, I have built a TODO list manager. Productivity tools like TODO lists are becoming increasingly popular and with File I/O and ArrayLists you will be able to build one (and implement one or more features of your choosing!). My TODO list manager will allow a user to add items to a TODO list, mark TODOs as completed and save and load TODOs to and from a file.
```java
import java.util.*;
import java.io.*;

public class TodoListManager {
    public static final boolean EXTENSION_FLAG = false;

    public static void main(String[] args) throws FileNotFoundException {
        Scanner console = new Scanner(System.in);
        List<String> todos = new ArrayList<>();
        List<String> todosCompleted = new ArrayList<>();
        System.out.println("Welcome to your TODO List Manager!");
        String input = "";

        // Continue looping until the user inputs 'q' to quit program
        while(!input.equalsIgnoreCase("q")){

            // Present the user different options based on the EXTENSION_FLAG
            if(EXTENSION_FLAG){
                System.out.println("What would you like to do?");
                System.out.print("(A)dd TODO, (M)ark TODO as done, (L)oad TODOs, "
                    + "(S)ave TODOs, (D)isplay completed TODOs, (Q)uit? ");
                
            } else {
                System.out.println("What would you like to do?");
                System.out.print("(A)dd TODO, (M)ark TODO as done, (L)oad TODOs, "
                    + "(S)ave TODOs, (Q)uit? ");
            }
            input = console.nextLine();

            if(input.equalsIgnoreCase("A")){
                addItem(console, todos);

            } else if (input.equalsIgnoreCase("M")){
                markItemAsDone(console, todos, todosCompleted);
            } else if (input.equalsIgnoreCase("L")){
                loadItems(console, todos);

            } else if (input.equalsIgnoreCase("S")){
                saveItems(console, todos);
            
            } else if (input.equalsIgnoreCase("D") && EXTENSION_FLAG){
                displayCompletedTodos(todosCompleted);
            
            } else if (!input.equalsIgnoreCase("Q")){
                System.out.println("Unknown input: " + input);
            } 
            if (!input.equalsIgnoreCase("q")){
                printTodos(todos);
            } 
        }
    }

    /**
     * This method prints current list of TODOs.
     * Uses the List of current TODO items as a parameter.
     */
    public static void printTodos(List<String> todos) {
        System.out.println("Today's TODOs:");
        if (todos.size() == 0){
            System.out.println(" You have nothing to do yet today! Relax!");

        } else {
            for(int i = 0; i < todos.size(); i++){
                System.out.println("  " + (i + 1) + ": " + todos.get(i));
            }
        }
    }

    /**
     * This method adds a new item to the List of TODOs. The user is prompted to
     * enter the new item and its position in the List. If no position is
     * provided, the item is added to the end of the List.
     * This method utilizes 2 parameters:
     * - Console the Scanner object used for user input
     * - todos the List of current TODO items
     */
    public static void addItem(Scanner console, List<String> todos) {
        System.out.print("What would you like to add? ");
        String answerAdd = console.nextLine();
        if (todos.size() == 0){
            todos.add(answerAdd);
        } else {
            System.out.print("Where in the list should it be (1-" 
                    + (todos.size() + 1) + ")? (Enter for end): ");
            String placeAdd = console.nextLine();
            if(placeAdd.isEmpty()){
                todos.add(answerAdd);
            } else {
                int location = Integer.parseInt(placeAdd) - 1;
                todos.add(location, answerAdd);
            }
        }
    }

    /**
     * This method marks an item as done and move it to the list of completed TODOs.
     * The user is prompted to select the item they want to mark as done.
     * This method utulizes 3 parameters:
     * - Console the Scanner object used for user input
     * - todos the List of current TODO items
     * _ todosCompleted the List of completed TODO items
     */
    public static void markItemAsDone(Scanner console, List<String> todos, List<String> todosCompleted) {
        if (todos.size() == 0){
            System.out.println("All done! Nothing left to mark as done!");
            return;
        }
        System.out.print("Which item did you complete (1-" + todos.size() + ")?");
        int index = Integer.parseInt(console.nextLine()) -1;
        String completedItem = todos.remove(index);
        todosCompleted.add(completedItem);
    }

    /**
     * This method loads items from a file into the List of TODOs. The user is prompted
     * to enter the filename. The List is cleared before loading new items.
     * This method utilizes 2 parameters:
     * - Console the Scanner object used for user input
     * - todos the List of current TODO items
     */
    public static void loadItems(Scanner console, List<String> todos)
                                throws FileNotFoundException {
        System.out.print("File name? ");
        String fileName = console.nextLine();
        File myFile = new File(fileName);
        Scanner fileScanner = new Scanner(myFile);
        todos.removeAll(todos);
        while(fileScanner.hasNextLine()){
            String values = fileScanner.nextLine();
            todos.add(values); 
        }
    }

    /**
     * This method saves the List of TODOs to a file. The user is prompted to
     * enter the filename where the items will be saved.
     * This method utilizes 2 parameters:
     * - Console the Scanner object used for user input
     * - todos the List of current TODO items
     */
    public static void saveItems(Scanner console, List<String> todos)
                                throws FileNotFoundException {
        System.out.println("File name? ");
        String fileName = console.nextLine();
        PrintStream output = new PrintStream(new File(fileName));
        for(int i = 0; i < todos.size(); i++){
            output.println(todos.get(i));
        }
    }

    /**
     * This method displays the List of completed TODO items. This method is
     * only called if the EXTENSION_FLAG is set to true.
     * Utilize todosCompleted the List of completed TODO items as a parameter
     */
    public static void displayCompletedTodos(List<String> todosCompleted){
        System.out.println("Completed TODOs: ");
        if(todosCompleted.size() == 0){
            System.out.println("You have not completed any TODOs yet!");
        } else {
            for(int i = 0; i < todosCompleted.size(); i++){
                System.out.println("  " + (i + 1) + ": " + todosCompleted.get(i));
            }
        }
    }
}
  
```

## The program begins by printing a short introduction. Then, the program prompts for a patient's name, followed by the patient information that will be used to compute the priority score (see below). The program uses this information to compute a score and determine the patient's priority. This information is printed out, along with a brief recommendation based on the priority. The program then prints a thank you message and prompts for another patient name. This process continues until the word quit is typed as the name, at which point summary statistics for the day are printed

```java
import java.util.*;
public class PatientPrioritizer {
    public static final int HOSPITAL_ZIP = 12345;

    public static void main (String[] args){
        Scanner console = new Scanner(System.in);
        int numPatients = 0;
        int highestPriorityScore = 0;
        
        introduction();
        String name = getName(console);
        while (!name.equals("quit")) {
            numPatients++;
            int score = getPatientScore(console);
            System.out.println();   
            printPatientPriority(name, score);   
            closing();
            if (score > highestPriorityScore) {
                highestPriorityScore = score;
            }
            name = getName(console);
        }    
        printOverallStatistics(numPatients, highestPriorityScore);   
        
    }
    
    // this method just prints out introduction statements
    public static void introduction() {
        System.out.println("Hello! We value you and your time, so we will help");
        System.out.println("you prioritize which patients to see next!");
        System.out.println("Please answer the following questions about the next patient so");
        System.out.println("we can help you do your best work :)");
        System.out.println();  
    }
    
    // this method gets patient' name
    // parameters:
    // - Scanner console: it's input that we can write somethings
    // returns:
    // - String: patient's name
    public static String getName(Scanner console){
        System.out.println("Please enter the next patient's name or \"quit\" to end the program.");
        System.out.print("Patient's name: ");
        return console.next();
    }

    // this methods get patient's all other informartion
    // also this methods has five other methods
    // parameters:
    // - Scanner console: it's input that we can write somethings
    // returns: 
    //- int: calculated priority score 
    public static int getPatientScore(Scanner console) {
        int age = getPatientAge(console);
        int zipCode = getPatientZipCode(console);
        boolean inNetwork = isHospitalInNetwork(console);
        int painLevel = getPatientPainLevel(console);
        double temperature = getPatientTemperature(console);

        return calculatePriorityScore(age, zipCode, inNetwork, painLevel, temperature);
    }

    // this method calculates patient priority score
    // age (int), zipCode (int), inNetwork (boolean), painLevel (int) and temperature (double).
    // then it returns score (int)
    public static int calculatePriorityScore(int age, int zipCode, boolean inNetwork,
            int painLevel, double temperature){        
        int score = 100;
        if (age < 12 || age >= 75) {
            score += 50;
        }
        
        int firstDigit = zipCode / 10000;
        int secondDigit = (zipCode / 1000) % 10;

        if (firstDigit == HOSPITAL_ZIP / 10000) {
            score += 25;
            if (secondDigit == (HOSPITAL_ZIP / 1000) % 10) {
                score += 15;
            }
        }

        if (inNetwork) {
            score += 50;
        }

        score += painLevel * 10;

        if (temperature > 99.5) {
            score += 8;
        }

        return score;
    }

    //  this method gets patient' age
    // parameters:
    // - Scanner console: it's input that we can write somethings
    // returns:
    // - int: patient's age
    public static int getPatientAge(Scanner console) {
        System.out.print("Patient age: ");
        return console.nextInt();
    }

    // this method gets patient' zipCode
    // parameters:
    // - Scanner console: it's input that we can write somethings
    // returns:
    // - int: patient's zipCode
    public static int getPatientZipCode(Scanner console) {
        System.out.print("Patient zip code: ");
        int zipCode = console.nextInt();
        while (!fiveDigits(zipCode)) {
            System.out.print("Invalid zip code, enter valid zip code: ");
            zipCode = console.nextInt();  
        }
        return zipCode;  
    }

    // this method gets patient' inNetwork
    // parameters:
    // - Scanner console: it's input that we can write somethings
    // returns:
    // - boolean: patient's inNetwork
    public static boolean isHospitalInNetwork(Scanner console) {
        System.out.print("Is our hospital \"in network\" for the patient's insurance? ");
        String response = console.next();
        return response.equals("y") || response.equals("yes");
    }

    // this method gets patient' painLevel
    // parameters:
    // - Scanner console: it's input that we can write somethings
    // returns:
    // - int: patient's painLevel
    public static int getPatientPainLevel(Scanner input) {
        System.out.print("Patient pain level (1-10): ");
        int painLevel = input.nextInt();
        while (painLevel < 1 || painLevel > 10) {
            System.out.print("Invalid pain level, enter valid pain level (1-10): ");
            painLevel = input.nextInt();
        }
        return painLevel;
    }

    // this method gets patient' temperature
    // parameters:
    // - Scanner console: it's input that we can write somethings
    // returns:
    // - double: patient's temperature
    public static double getPatientTemperature(Scanner console) {
        System.out.print("Patient temperature (in degrees Fahrenheit): ");
        return console.nextDouble();
    }

    // this method gets patient' priority
    // parameters:
    // - String name: name of the patient
    // - int score: calculated score of patient
    public static void printPatientPriority(String name, int score) {
        System.out.println("We have found patient "+ name +" to have a priority score of: "+score);
        System.out.print("We have determined this patient is ");
        if (score >= 333) {
            System.out.println("high priority,");
            System.out.println("and it is advised to call an appropriate medical provider ASAP.");
            System.out.println();
        } else if (score >= 168) {
            System.out.println("medium priority.");
            System.out.println("Please assign an appropriate medical provider to their case");
            System.out.println("and check back in with the patient's "
                    + "condition in a little while.");
            System.out.println();
        } else {
            System.out.println("low priority.");
            System.out.println("Please put them on the waitlist for when a "
                    + "medical provider becomes available.");
            System.out.println();
        }
    }

    // this method just print out closing statements
    public static void closing(){
        System.out.println("Thank you for using our system!");
        System.out.println("We hope we have helped you do your best!");
        System.out.println();
    }

    // this method implements at the end overall Statistics of patients 
    // parameters:
    // - numPatients: how many people use this system
    // - highestPriorityScore: the highest score people got
    public static void printOverallStatistics(int numPatients, int highestPriorityScore) {
        System.out.println("Statistics for the day:");
        System.out.println("..." + numPatients + " patients were helped");
        System.out.print("...the highest priority patient we saw had a score of " );
        System.out.println(highestPriorityScore);
        System.out.println("Good job today!");       
    }

    // Takes in an integer input.
    // Returns true if the integer has 5 digits, and false otherwise.
    public static boolean fiveDigits(int val) {
        val = val / 10000; // get first digit
        if (val == 0) { // has less than 5 digits
            return false;
        } else if (val / 10 == 0) { // has 5 digits
            return true;
        } else { // has more than 5 digits
            return false; 
        }
        // NOTE: the above can be written with improved "boolean zen" as follows: 
        // return val != 0 && val / 10 == 0;
    }
}
```