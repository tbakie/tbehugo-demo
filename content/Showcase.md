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