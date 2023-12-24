# -assignment
QNO1
#include <iostream>
using namespace std;
class Shape {
public:
    virtual void draw() const = 0;
    virtual void displayArea() const {
        cout << "Area: Not applicable for an undefined shape." << endl;
    }
};

class Circle : public Shape {
private:
    double radius;
public:
    Circle(double r) : radius(r) {}
    void draw() const override {
        cout << "Drawing a circle." << endl;
    }
    void displayArea() const override {
        double area = 3.14159 * radius * radius;
        cout << "Area of the circle: " << area << endl;
    }
};
class Rectangle : public Shape {
private:
    double length;
    double width;
public:
    Rectangle(double l, double w) : length(l), width(w) {}
    void draw() const override {
        cout << "Drawing a rectangle." << endl;
    }
    void displayArea() const override {
        double area = length * width;
        cout << "Area of the rectangle: " << area << endl;
    }
};
int main() {
    Circle circle(5.0);
    Rectangle rectangle(4.0, 6.0);
    Shape* shapePtr = &circle;
    shapePtr->draw();
    shapePtr->displayArea();
    shapePtr = &rectangle;
    shapePtr->draw();
    shapePtr->displayArea();
    return 0;
}


QNO2

#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Product {
private:
    int productId;
    string productName;
    double price;

public:
    Product(int id, const string& name, double p) : productId(id), productName(name), price(p) {}

    void displayDetails() const {
        cout << "Product ID: " << productId << ", Name: " << productName << ", Price: $" << price << endl;
    }

    double getPrice() const {
        return price;
    }
};

class ShoppingCart {
private:
    vector<Product*> products;

public:
    void addProduct(Product* product) {
        products.push_back(product);
    }

    void displayAllProducts() const {
        cout << "Products in the Shopping Cart:" << endl;
        for (const auto& product : products) {
            product->displayDetails();
        }
    }

    double calculateTotalCost() const {
        double total = 0.0;
        for (const auto& product : products) {
            total += product->getPrice();
        }
        return total;
    }
};

class User {
private:
    int userId;
    ShoppingCart* cart;

public:
    User(int id) : userId(id), cart(nullptr) {}

    void displayDetails() const {
        cout << "User ID: " << userId << endl;
        if (cart) {
            cout << "User has a shopping cart." << endl;
        }
        else {
            cout << "User does not have a shopping cart." << endl;
        }
    }

    void associateShoppingCart(ShoppingCart* shoppingCart) {
        cart = shoppingCart;
    }
};

int main() {
    Product* laptop = new Product(101, "Laptop", 1200.0);
    Product* phone = new Product(102, "Smartphone", 800.0);
    Product* headphones = new Product(103, "Headphones", 100.0);
    ShoppingCart* cart = new ShoppingCart();
    cart->addProduct(laptop);
    cart->addProduct(phone);
    cart->addProduct(headphones);
    User* user1 = new User(1);
    User* user2 = new User(2);
    user1->associateShoppingCart(cart);
    user1->displayDetails();
    user2->displayDetails();
    cart->displayAllProducts();
    double totalCost = cart->calculateTotalCost();
    cout << "Total Cost in ShoppingCart: $" << totalCost << endl;
    delete laptop;
    delete phone;
    delete headphones;
    delete cart;
    delete user1;
    delete user2;
    return 0;
}
