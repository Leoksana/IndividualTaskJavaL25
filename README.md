# IndividualTaskJavaL25
Main.java
```java
import java.util.Scanner;

public class Main {
    private static Scanner scanner = new Scanner(System.in);
    private static CheeseService itemService = new CheeseService();

    public static void main(String[] args) {
        while (true) {
            System.out.println("Press 1 to add an item");
            System.out.println("Press 2 to print all items");
            System.out.println("Press 3 to remove an item");
            System.out.println("Press 4 to update an item");
            System.out.println("Press 5 to exit");
            int action = scanner.nextInt();
            // If the user chooses 1, then we call addItem();
            if (action == 1) {
                addItem();
            } else if (action == 2) {
                printItems();
            } else if (action == 3) {
                removeItem();
            } else if (action == 4) {
                updateItem();
            } else {
                break;
            }
        }
    }

    public static void addItem() {
        System.out.println("Provide an item name");
        String name = scanner.next();
        System.out.println("Provide an item cost");
        int cost = scanner.nextInt();
        Cheese item = new Cheese(name, cost);
        itemService.addItem(item);
    }

    public static void printItems() {
        System.out.println("These are the items in the storage:");
        var items = itemService.getItems();
        for (var item : items) {
            System.out.println(item.getName() + ": €" + item.getCost());
        }
    }

    public static void removeItem() {
        System.out.println("Provide the name of the item to remove");
        String name = scanner.next();
        itemService.removeItem(name);
    }

    public static void updateItem() {
        System.out.println("Provide the name of the item to update");
        String name = scanner.next();
        System.out.println("Provide the new cost of the item");
        int newCost = scanner.nextInt();
        itemService.updateItem(name, newCost);
    }
}
```
Cheese.java
```java
public class Cheese {
    private String name;
    private int cost;

    public Cheese(String name, int cost) {
        this.name = name;
        this.cost = cost;
    }

    public String getName() {
        return name;
    }

    public int getCost() {
        return cost;
    }

    public void setCost(int cost) {
        this.cost = cost;
    }
}
```

CheeseShop.java
```java
import java.util.ArrayList;

public class CheeseShop {
    // List to hold items in the cart
    private ArrayList<Cheese> cart = new ArrayList<>();

    // Method to add a cheese item to the cart
    public void addCheeseToCart(Cheese item) {
        cart.add(item);
    }

    // Method to remove a cheese item from the cart
    public void removeItemFromCart(Cheese item) {
        cart.remove(item);
    }

    // Method to get the total cost of items in the cart
    public int checkout() {
        int sum = 0;
        for (var item : cart) {
            sum += item.getCost();
        }
        return sum;
    }
}
```

CheeseService.java
```java
import java.util.ArrayList;
public class CheeseService{
    private ArrayList<Cheese> items = new ArrayList<Cheese>();

    public ArrayList<Cheese> getItems() {
        return items;
    }

    public void addItem(Cheese item) {
        items.add(item);
    }

    public void removeItem(String name) {
        for (var item : items) {
            if (item.getName() == name) {
                items.remove(item);
                return;
            }
        }
    }

    public void updateItem(String name, int cost) {
        for (var item : items) {
            if (item.getName() == name) {
                item.setCost(cost);
                return;
            }
        }
    }
}
```
