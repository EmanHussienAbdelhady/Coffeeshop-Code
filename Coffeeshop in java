import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class CoffeeShop {
    /**
     *
     */
    private String name;
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    private MenuItem[] menu;
    private String[] orders;

    // Constructor
    public CoffeeShop(String name, MenuItem[] menu) {
        this.name = name;
        this.menu = menu;
        this.orders = new String[0];
    }

    // Method to add an order
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

    // Method to fulfill an order
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

    // Method to list orders
    public String[] listOrders() {
        return orders;
    }

    // Method to calculate due amount
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

    // Method to find cheapest item
    public String cheapestItem() {
        MenuItem cheapest = menu[0];
        for (MenuItem item : menu) {
            if (item.getPrice() < cheapest.getPrice()) {
                cheapest = item;
            }
        }
        return cheapest.getName();
    }

    // Method to get drinks only
    public String[] drinksOnly() {
        List<String> drinkList = new ArrayList<>();
        for (MenuItem item : menu) {
            if (item.getType().equalsIgnoreCase("drink")) {
                drinkList.add(item.getName());
            }
        }
        return drinkList.toArray(new String[0]);
    }

    // Method to get food only
    public String[] foodOnly() {
        List<String> foodList = new ArrayList<>();
        for (MenuItem item : menu) {
            if (item.getType().equalsIgnoreCase("food")) {
                foodList.add(item.getName());
            }
        }
        return foodList.toArray(new String[0]);
    }

    public static void main(String[] args) {
        // Define menu items
        MenuItem[] menuItems = {
            new MenuItem("Latte", "drink", 3.99),
            new MenuItem("Iced coffee", "drink",0.18),
            new MenuItem("Cinnamon roll", "food", 1.99),
            new MenuItem("Ham and cheese sandwich", "food", 4.99),
            new MenuItem("Tuna sandwich", "food", 5.49),
            new MenuItem("Lemonade", "drink", 0.16),
            new MenuItem("Orange juice", "drink", 2.49),
            new MenuItem("Cranberry juice", "drink", 2.99),
            new MenuItem("Pineapple juice", "drink", 2.99),
            new MenuItem("bacon", "food", 2.99)
        };

        // Create coffee shop
        CoffeeShop tcs = new CoffeeShop("Tesha's Coffee Shop", menuItems);

        // Test adding orders
        try {
            System.out.println(tcs.addOrder("hot cocoa")); // "This item is currently unavailable!"
        } catch (ItemUnavailableException e) {
            System.out.println("This item is currently unavailable");
        }

        try {
            System.out.println(tcs.addOrder("iced tea")); // "This item is currently unavailable!"
        } catch (ItemUnavailableException e) {
            System.out.println("This item is currently unavailable");
        }

        try {
            System.out.println(tcs.addOrder("cinnamon roll")); // "Order added!"
        } catch (ItemUnavailableException e) {
            System.out.println("This item is currently unavailable");
        }

        try {
            System.out.println(tcs.addOrder("iced coffee")); // "Order added!"
        } catch (ItemUnavailableException e) {
            System.out.println("This item is currently unavailable");
        }

        // Test listing orders and calculating due amount
        System.out.println(Arrays.toString(tcs.listOrders())); // ["cinnamon roll", "iced coffee"]
        System.out.println(String.format("%.2f", tcs.dueAmount())); // 2.17

        // Test fulfilling orders
        System.out.println(tcs.fulfillOrder()); // "The cinnamon roll is ready!"
        System.out.println(tcs.fulfillOrder()); // "The iced coffee is ready!"
        System.out.println(tcs.fulfillOrder()); // "All orders have been fulfilled!"

        // Test listing orders and calculating due amount after fulfilling all orders
        System.out.println(Arrays.toString(tcs.listOrders())); // []
        System.out.println(String.format("%.2f", tcs.dueAmount())); // 0.00

        // Test finding cheapest item
        System.out.println(tcs.cheapestItem()); // "Lemonade"

        // Test getting drinks only
        System.out.println(Arrays.toString(tcs.drinksOnly())); // ["Lemonade", "Orange juice", "Cranberry juice", "Pineapple juice"]

        // Test getting food only
        System.out.println(Arrays.toString(tcs.foodOnly())); // ["Cinnamon roll", "Ham and cheese sandwich", "Tuna sandwich"]
    }
}

class MenuItem {
    private String name;
    private String type;
    private double price;

    // Constructor
    public MenuItem(String name, String type, double price) {
        this.name = name;
        this.type = type;
        this.price = price;
    }

    // Getter methods
    public String getName() {
        return name;
    }

    public String getType() {
        return type;
    }

    public double getPrice() {
        return price;
    }
}

class ItemUnavailableException extends Exception {
    public ItemUnavailableException() {
        super("This item is currently unavailable!");
    }
}
