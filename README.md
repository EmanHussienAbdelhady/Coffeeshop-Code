# Coffeeshop-Code
explanation and also note that there's a comment on each line to clarify

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;


This line imports the necessary classes from the Java standard library for working with arrays and lists.


public class CoffeeShop {
    private String name;
    private MenuItem[] menu;
    private String[] orders;


This line defines a class called `CoffeeShop` with three private instance variables: `name`, which is a `String` representing the name of the coffee shop; `menu`, which is an array of `MenuItem` objects representing the menu items available at the coffee shop; and `orders`, which is an array of `String` objects representing the current orders placed at the coffee shop.


public CoffeeShop(String name, MenuItem[] menu) {
    this.name = name;
    this.menu = menu;
    this.orders = new String[0];
}


This is a constructor method for the `CoffeeShop` class. It takes two arguments: the name of the coffee shop and an array of `MenuItem` objects representing the menu items available at the coffee shop. It initializes the instance variables `name` and `menu` with the provided arguments and initializes the `orders` array as an empty array with a length of 0.

public String addOrder(String itemName) throws ItemUnavailableException {
    boolean found = false;
    for (MenuItem item : menu) {
        if (item.getName().equalsIgnoreCase(itemName)) {
            found = true;
            String[] newOrders = new String[orders.length + 1];
            System.arraycopy(orders, 0, newOrders, 0, orders.length);
            newOrders[orders.length] = itemName;
            orders = newOrders;
            return "Order added!";
        }
    }
    if (!found) {
        throw new ItemUnavailableException();
    }
    return "";
}


This is a method for the `CoffeeShop` class that adds an order to the `orders` array. It takes an argument `itemName`, which is a `String` representing the name of the item being ordered. It loops through the `menu` array to see if the item is available. If the item is available, it adds the item name to the `orders` array and returns the string `"Order added!"`. If the item is not available, it throws an `ItemUnavailableException`. If the loop completes without finding the item, it returns an empty string.


public String fulfillOrder() {
    if (orders.length == 0) {
        return "All orders have been fulfilled!";
    }
    String itemName = orders[0];
    String[] newOrders = new String[orders.length - 1];
    System.arraycopy(orders, 1, newOrders, 0, orders.length - 1);
    orders = newOrders;
    return "The " + itemName + " is ready!";
}


This is a method for the `CoffeeShop` class that fulfills the next order in the `orders` array. It checks if the `orders` array is empty. If it is, it returns the string `"All orders have been fulfilled!"`. If it is not empty, it removes the first item from the `orders` array, updates the `orders` array to exclude the removed item, and returns a string indicating that the item is ready.


public String[] listOrders() {
    return orders;
}


This is a method for the `CoffeeShop` class that returns the `orders` array.


public double dueAmount() {
    double total = 0;
    for (String itemName : orders) {
        for (MenuItem item : menu) {
            if (item.getName().equalsIgnoreCase(itemName)) {
                total += item.getPrice();
                break;
            }
        }
    }
    return total;
}


This is a method for the `CoffeeShop` class that calculates the total due amount for all orders in the `orders` array. It loops through the `orders` array and for each order, loops through the `menu` array to find the corresponding `MenuItem` object and add its price to the `total` variable. It then returns the `total` variable.


public String cheapestItem() {
    MenuItem cheapest = menu[0];
    for (MenuItem item : menu) {
        if (item.getPrice() < cheapest.getPrice()) {
            cheapest = item;
        }
    }
    return cheapest.getName();
}


This is a method for the `CoffeeShop` class that finds the cheapest item on the menu. It initializes a `MenuItem` object called `cheapest` with the first item in the `menu` array, and loops through the `menu` array to compare the prices of all menu items with the current cheapest item. If a cheaper item is found, it updates the `cheapest` variable to that item. It then returns the name of the cheapest item.


public String[] drinksOnly() {
    List<String> drinkList = new ArrayList<>();
    for (MenuItem item : menu) {
        if (item.getType().equalsIgnoreCase("drink")) {
            drinkList.add(item.getName());
        }
    }
    return drinkList.toArray(new String[0]);
}


This is a method for the `CoffeeShop` class that returns an array of all drink items on the menu. It initializes an empty `ArrayList` called `drinkList`, loops through the `menu` array to find all items with the type `"drink"`, and adds the names of those items to the `drinkList` array. It then converts the `drinkList` array to a regular array and returns it.


public String[] foodOnly() {
    List<String> foodList = new ArrayList<>();
    for (MenuItem item : menu) {
        if (item.getType().equalsIgnoreCase("food")) {
            foodList.add(item.getName());
        }
    }
    return foodList.toArray(new String[0]);
}


This is a method for the `CoffeeShop` class that returns an array of all food items on the menu. It works in a similar way to the `drinksOnly` method, but finds items with the type `"food"` instead.

