# online-shopping-app-Ali-express-
I have developed a project using java implementing object oriented programming.


package onlineshopping;

import java.util.ArrayList;
import java.util.Scanner;
import java.io.*;

public class Onlineshopping {

    private static final String FILE_NAME = "OnlineShoppingApp.txt";
    
    public static void main(String[] args) {
         Scanner scan = new Scanner(System.in);

        int choice;

        do {
            System.out.println("Aliexpress: Shopping Online");
            System.out.println("Press 1 for (ADMIN)");
            System.out.println("Press 2 for (CUSTOMER)");
            System.out.println("Enter Your Choice");
            choice = scan.nextInt();

            switch (choice) {
                case 1 : {
                    Admin admin = new Admin();
                    System.out.println("Enter username:");
                    String username = scan.next();
                    System.out.println("Enter password:");
                    String password = scan.next();
                    if (admin.login(username, password)) {
                        System.out.println("Login successful!");
                        admin.manageProducts();
                        admin.viewOrders();
                    } else {
                        System.out.println("Invalid credentials.");
                    }
                }
                case 2 : {
                    System.out.println("Welcome Customer!");
                    System.out.println("Enter your name:");
                    String name = scan.next();
                    System.out.println("Enter your preferred size:");
                    String size = scan.next();
                    Customer customer = new Customer(name, size);
                    int customerChoice;
                    do {
                        System.out.println("Customer Menu:");
                        System.out.println("1. Add to Cart");
                        System.out.println("2. View Cart");
                        System.out.println("3. Checkout");
                        System.out.println("4. Exit");
                        System.out.println("Enter your choice:");
                        customerChoice = scan.nextInt();
                        
                        switch (customerChoice) {
                            case 1 : {
                                Product sampleProduct = new Product("Sample Product", 19.99, 1234, "Red");
                                customer.addToCart(sampleProduct);
                            }
                            case 2 : customer.viewCart();
                            case 3 : customer.checkout();
                            case 4 : System.out.println("Exiting Customer Menu.");
                            default : System.out.println("Invalid choice. Please try again.");
                        }
                    } while (customerChoice != 4);
                }
                default : System.out.println("Invalid choice. Please try again!");
            }

        } while (true);
    }
     private static ArrayList<OnlineShoppingApp> readOnlineShoppingAppsFromFile(String fileName) {
        ArrayList<OnlineShoppingApp> OnlineShoppingApps = new ArrayList<>();

        try (BufferedReader reader = new BufferedReader(new FileReader(fileName))) {
           String name;
           String price;
           String product_id;
           String color;


            while ((product_id = reader.readLine()) != null) {
                name = reader.readLine();
                price  = reader.readLine();
                color  = reader.readLine();
                OnlineShoppingApps.add(new OnlineShoppingApp(name, price, color,product_id));
            }
        } catch (IOException e) {
            System.err.println("Error reading from file: " + e.getMessage());
        }

        return OnlineShoppingApps;
    }

     private static class OnlineShoppingApp {

        public OnlineShoppingApp() {
        }

        private OnlineShoppingApp(String name, String price, String color, String product_id) {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private char[] getProduct_id() {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private char[] getName() {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private char[] getPrice() {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private char[] getColor() {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private void setProduct_id(String newproduct_id) {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private void setname(String newname) {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private void setprice(String newprice) {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private void setcolor(String newcolor) {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }

        private void setName(String updatedname) {
            throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
        }
    }
 private static void saveOnlineShoppingAppsToFile(ArrayList<OnlineShoppingApp> OnlineShoppingApps, String fileName) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(fileName))) {
            for (OnlineShoppingApp OnlineShoppingApp : OnlineShoppingApps) {
                writer.write(OnlineShoppingApp.getProduct_id());
                writer.newLine();
                writer.write(OnlineShoppingApp.getName());
                writer.newLine();
                writer.write(OnlineShoppingApp.getPrice());
                writer.newLine();
                writer.write(OnlineShoppingApp.getColor());
                writer.newLine();
            }
        } catch (IOException e) {
            System.err.println("Error writing to file: " + e.getMessage());
        }
    }
 private static void updateOnlineShoppingApp(ArrayList<OnlineShoppingApp> OnlineShoppingApps, Scanner scanner) {
        if (OnlineShoppingApps.isEmpty()) {
            System.out.println("No data available to update.");
            return;
        }
        System.out.print("Enter Product ID of the product to update: ");
        String updateproduct_id = scanner.next();
        OnlineShoppingApp OnlineShoppingAppToUpdate = null;
        for (OnlineShoppingApp OnlineShoppingApp : OnlineShoppingApps) {
            if (OnlineShoppingApp.getProduct_id().equals(updateproduct_id)) {
                OnlineShoppingAppToUpdate = OnlineShoppingApp;
                break;
            }
        }
        if (OnlineShoppingAppToUpdate == null) {
            System.out.println("product not found.");
            return;
        }
        System.out.println("Update Menu:");
        System.out.println("1. Update product ID");
        System.out.println("2. Update  name");
        System.out.println("3. Update price");
        System.out.println("4. Update colour");
        System.out.println("5. Update everything");
        System.out.println("6. Go back");
        System.out.print("Enter your choice: ");
        int updateChoice = scanner.nextInt();
        switch (updateChoice) {
            case 1:
                System.out.print("Enter new product ID: ");
                String newproduct_id = scanner.next();
                boolean isUniqueID = OnlineShoppingApps.stream().noneMatch(OnlineShoppingApp -> OnlineShoppingApp.getProduct_id().equals(newproduct_id));
                if (isUniqueID) {
                    OnlineShoppingAppToUpdate.setProduct_id(newproduct_id);
                    saveOnlineShoppingAppsToFile(OnlineShoppingApps, FILE_NAME);
                    System.out.println("Product ID updated successfully!");
                } else {
                    System.out.println("product ID must be unique. Update failed.");
                }
                break;
            case 2:
                System.out.print("Enter new  name: ");
                String newname = scanner.next();
                OnlineShoppingAppToUpdate.setname(newname);
                saveOnlineShoppingAppsToFile(OnlineShoppingApps, FILE_NAME);
                System.out.println(" name updated successfully!");
                break;
            case 3:
                System.out.print("Enter new price: ");
                String newprice = scanner.next();
                OnlineShoppingAppToUpdate.setprice(newprice);
                saveOnlineShoppingAppsToFile(OnlineShoppingApps, FILE_NAME);
                System.out.println("Last price updated successfully!");
                break;
            case 4:
                System.out.print("Enter new colour: ");
                String newcolor = scanner.next();
                OnlineShoppingAppToUpdate.setcolor(newcolor);
                saveOnlineShoppingAppsToFile(OnlineShoppingApps, FILE_NAME);
                System.out.println("Last colour updated successfully!");
                break;
            case 5:
                System.out.print("Enter new product ID: ");
                String updatedproduct_id = scanner.next();
                boolean isUniqueUpdatedID = OnlineShoppingApps.stream().noneMatch(OnlineShoppingApp -> OnlineShoppingApp.getProduct_id().equals(updatedproduct_id));
                if (isUniqueUpdatedID) {
                    OnlineShoppingAppToUpdate.setProduct_id(updatedproduct_id);
                    System.out.print("Enter new  name: ");
                    String updatedname = scanner.next();
                    OnlineShoppingAppToUpdate.setName(updatedname);
                    System.out.print("Enter new price : ");
                    String updatedprice = scanner.next();
                    OnlineShoppingAppToUpdate.setprice(updatedprice);
                    saveOnlineShoppingAppsToFile(OnlineShoppingApps, FILE_NAME);
                    System.out.println("online shooping app data updated successfully!");
                } else {
                    System.out.println("Product ID must be unique. Update failed.");
                }
                break;
            case 6:
                System.out.println("Going back...");
                break;
            default:
                System.out.println("Invalid choice. Please enter a number from 1 to 6.");
        }
    }
private static void deleteOnlineShoppingApp(ArrayList<OnlineShoppingApp> OnlineShoppingApps, Scanner scanner) {
        if (OnlineShoppingApps.isEmpty()) {
            System.out.println("No online shopping apps data  available to delete.");
            return;
        }
        System.out.print("Enter product ID of the student to delete: ");
        String deleteproduct_id = scanner.next();
        boolean removed = OnlineShoppingApps.removeIf(OnlineShoppingApp -> OnlineShoppingApp.getProduct_id().equals(deleteproduct_id));
        if (removed) {
            saveOnlineShoppingAppsToFile(OnlineShoppingApps, FILE_NAME);
            System.out.println("online shopping app data deleted successfully!");
        } else {
            System.out.println("online shopping app data not found.");
        }
    }


}
class Product {
    private String name;
    private double price;
    private int product_id;
    private String color;

    public Product(String name, double price, int product_id, String color) {
        this.name = name;
        this.price = price;
        this.product_id = product_id;
        this.color = color;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public int getProduct_id() {
        return product_id;
    }

    public String getColor() {
        return color;
    }

    public String printInfo() {
        return "Product: " + name + ", Cost: $" + String.format("%.2f", price) + ", ID: " + product_id + ", Color: " + color;
    }
}

class Customer {
    private String name;
    private String size;
    private ArrayList<Product> cart = new ArrayList<>();

    public Customer(String name, String size) {
        this.name = name;
        this.size = size;
    }

    public String getName() {
        return name;
    }

    public String getSize() {
        return size;
    }

    public void addToCart(Product product) {
        cart.add(product);
        System.out.println(product.getName() + " added to your cart!");
    }

    public void viewCart() {
        if (cart.isEmpty()) {
            System.out.println("Your cart is empty.");
        } else {
            System.out.println("Your Cart:");
            for (Product product : cart) {
                System.out.println(product.printInfo());
            }
        }
    }

    public void checkout() {
        System.out.println("Proceeding to checkout...");
        paymentProcessing();
    }

    public void paymentProcessing() {
        System.out.println("Your payment is under processing...");
       
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Your payment is done!");
        for (Product product : cart) {
            System.out.println(product.printInfo());
        }
    }
}

class Admin {
    private String username = "Arbaz"; 
    private String password = "arbaz123"; 

    public boolean login(String username, String password) {
        return this.username.equals(username) && this.password.equals(password);
    }

    public void manageProducts() {
        Scanner scan = new Scanner(System.in);
        int choice;

        do {
            System.out.println("Product Management");
            System.out.println("1. Add Product");
            System.out.println("2. Edit Product");
            System.out.println("3. Delete Product");
            System.out.println("4. Back");
            System.out.println("Enter your choice:");
            choice = scan.nextInt();

            switch (choice) {
                case 1 : addProduct();
                case 2 : editProduct();
                case 3 : deleteProduct();
                case 4 : System.out.println("Exiting Product Management.");
                default : System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);
    }

    private void addProduct() {
        Scanner scan = new Scanner(System.in);

        System.out.println("Enter product name:");
        String name = scan.nextLine();

        System.out.println("Enter product price (e.g., 19.99):");
        double price = scan.nextDouble();
        scan.nextLine(); 

        System.out.println("Enter product color:");
        String color = scan.nextLine();

        int product_id = (int) (Math.random() * 10000); 

        Product newProduct = new Product(name, price, product_id, color);
       
        System.out.println("Product added: " + newProduct.printInfo());
    }

    private void editProduct() {
          Scanner scan = new Scanner(System.in);
  ArrayList<Product> products = new ArrayList<>(); 

  System.out.println("Enter the ID of the product you want to edit:");
  int productId = scan.nextInt();

  // Find the product to edit
  Product productToEdit = null;
  for (Product product : products) {
    if (product.getProduct_id() == productId) {
      productToEdit = product;
      break;
    }
  }

  // Check if product found
  if (productToEdit == null) {
    System.out.println("Product with ID " + productId + " not found.");
    return;
  }

  // Display current product information
  System.out.println("Current product details:");
  System.out.println(productToEdit.printInfo());
    }

        private void deleteProduct() {
  Scanner scan = new Scanner(System.in);
  ArrayList<Product> products = new ArrayList<>(); 

  System.out.println("Enter the ID of the product you want to delete:");
  int productId = scan.nextInt();

  Product productToDelete = null;
  for (int i = 0; i < products.size(); i++) {
    Product product = products.get(i);
    if (product.getProduct_id() == productId) {
      productToDelete = product;
      products.remove(i); // Remove from product list
      break;
    }
  }

  // Check if product found
  if (productToDelete == null) {
    System.out.println("Product with ID " + productId + " not found.");
    return;
  }

  // Confirmation message
  System.out.println("Product with ID " + productId + " has been deleted.");
}

    public void viewOrders() {
        Scanner scan = new Scanner(System.in);
        int choice;

        do {
            System.out.println("Order Management");
            System.out.println("1. View Order Details (by ID)");
            System.out.println("2. Change Order Status");
            System.out.println("3. Back");
            System.out.println("Enter your choice:");
            choice = scan.nextInt();

            switch (choice) {
                case 1 : viewOrderDetails();
                case 2 : System.out.println("Change order status functionality is not yet available.");
                case 3 : System.out.println("Exiting Order Management.");
                default : System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);
    }

//    private void viewAllOrders() {
//        
//  Scanner scan = new Scanner(System.in);
//  ArrayList<Customer> customers = new ArrayList<>(); 
//
//  boolean hasOrders = false;
//  for (Customer customer : customers) {
//    if (!customer.getCart().isEmpty()) {
//      hasOrders = true;
//      break;
//    }
//  }
//
//  if (!hasOrders) {
//    System.out.println("There are no orders to display.");
//    return;
//  }
//
//  // Display all orders
//  System.out.println("Order History:");
//  for (Customer customer : customers) {
//    if (!customer.getCart().isEmpty()) {
//      System.out.println("Customer: " + customer.getName());
//      for (Product product : customer.getCart()) {
//        System.out.println("\t- " + product.printInfo());
//      }
//      System.out.println(); 
//    }
//  
//}

    

    private void viewOrderDetails() {
        Scanner scan = new Scanner(System.in);

        System.out.println("Enter order ID:");
        int orderId = scan.nextInt();

        
        System.out.println("This feature is not implemented yet.");
    }
}
