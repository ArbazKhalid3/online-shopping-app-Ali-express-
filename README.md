# online-shopping-app-Ali-express-
I have developed a project using java implementing object oriented programming.
 import java.util.ArrayList;
import java.util.Scanner;

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
            System.out.println("4. View All Products");
            System.out.println("5. Back");
            System.out.println("Enter your choice:");
            choice = scan.nextInt();

            switch (choice) {
                case 1:
                    addProduct();
                    break;
                case 2:
                    editProduct();
                    break;
                case 3:
                    deleteProduct();
                    break;
                case 4:
                    viewProducts();
                    break;
                case 5:
                    System.out.println("Exiting Product Management.");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 5);
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
        
    }

    private void deleteProduct() {
        
    }

    private void viewProducts() {
        
    }

    public void viewOrders() {
        Scanner scan = new Scanner(System.in);
        int choice;

        do {
            System.out.println("Order Management");
            System.out.println("1. View All Orders");
            System.out.println("2. View Order Details (by ID)");
            System.out.println("3. Change Order Status");
            System.out.println("4. Back");
            System.out.println("Enter your choice:");
            choice = scan.nextInt();

            switch (choice) {
                case 1:
                    viewAllOrders();
                    break;
                case 2:
                    viewOrderDetails();
                    break;
                case 3:
                    System.out.println("Change order status functionality is not yet available.");
                    break;
                case 4:
                    System.out.println("Exiting Order Management.");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);
    }

    private void viewAllOrders() {
        
    }

    private void viewOrderDetails() {
        Scanner scan = new Scanner(System.in);

        System.out.println("Enter order ID:");
        int orderId = scan.nextInt();

        
        System.out.println("This feature is not implemented yet.");
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);

        int choice;

        do {
            System.out.println("Aliexpress: Shopping Online");
            System.out.println("Press 1 for (ADMIN)");
            System.out.println("Press 2 for (CUSTOMER)");
            System.out.println("Enter Your Choice");
            choice = scan.nextInt();

            if (choice == 1) {
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

            } else if (choice == 2) {
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
                        case 1:
                            
                            Product sampleProduct = new Product("Sample Product", 19.99, 1234, "Red");
                            customer.addToCart(sampleProduct);
                            break;
                        case 2:
                            customer.viewCart();
                            break;
                        case 3:
                            customer.checkout();
                            break;
                        case 4:
                            System.out.println("Exiting Customer Menu.");
                            break;
                        default:
                            System.out.println("Invalid choice. Please try again.");
                    }
                } while (customerChoice != 4);

            } else {
                System.out.println("Invalid choice. Please try again!");
            }

        } while (true);
    }
}
