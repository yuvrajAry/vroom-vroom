
#include <iostream>
#include <string>
#include <vector>

using namespace std;

class Car {
public:
    Car(string make, string model, int year, int seats, double dailyRate)
        : make(make), model(model), year(year), seats(seats), dailyRate(dailyRate) {}

    virtual string getType() const = 0;

    string getMake() const { return make; }
    string getModel() const { return model; }
    int getYear() const { return year; }
    int getSeats() const { return seats; }
    double getDailyRate() const { return dailyRate; }

    virtual void display() const {
        cout << "Make: " << make <<endl;
        cout << "Model: " << model <<endl;
        cout << "Year: " << year <<endl;
        cout << "Seats: " << seats <<endl;
        cout << "Daily Rate: $" << dailyRate <<endl;
    }

    friend ostream& operator<<(ostream& out, const Car& car) {
        out << "Make: " << car.make <<endl;
        out << "Model: " << car.model <<endl;
        out << "Year: " << car.year <<endl;
        out << "Seats: " << car.seats <<endl;
        out << "Daily Rate: $" << car.dailyRate <<endl;
        return out;
    }

private:
    string make;
    string model;
    int year;
    int seats;
    double dailyRate;
};

class EconomyCar : public Car {
public:
    EconomyCar(string make, string model, int year)
        : Car(make, model, year, 5, 40.0) {}

    string getType() const override { return "Economy"; }
};

class LuxuryCar : public Car {
public:
    LuxuryCar(string make, string model, int year)
        : Car(make, model, year, 6, 100.0) {}

    string getType() const override { return "Luxury"; }
};

class SUV : public Car {
public:
    SUV(string make, string model, int year)
        : Car(make, model, year, 7, 80.0) {}

    string getType() const override { return "SUV"; }
};

class SixSeater : public Car {
public:
    SixSeater(string make, string model, int year)
        : Car(make, model, year, 6, 70.0) {}

    string getType() const override { return "Six Seater"; }
};

class RentalSystem {
public:
    void addCar(Car* car) {
        if (carCount < MaxCars) {
            cars[carCount++] = car;
        }
        else {
            cout << "Cannot add more cars. The system is full." << endl;
        }
    }

    void displayCars() {
        for (int i = 0; i < carCount; i++) {
            cout << *cars[i];
            cout << "Type: " << cars[i]->getType() << "\n\n";
        }
    }

Car* rentCar(int seats, int days) {
    if (seats < 5) {
        cout << "No cars available with fewer than 5 seats." << endl;
        return nullptr;
    }
    vector<Car*> matchingCars;

    for (int i = 0; i < carCount; i++) {
        if (cars[i]->getSeats() >= seats) {
            matchingCars.push_back(cars[i]);
        }
    }

    if (matchingCars.empty()) {
        cout << "No cars available with the requested number of seats." << endl;
        return nullptr;
    } else {
        cout << "Available " << seats << " seater cars:\n";
        for (int i = 0; i < matchingCars.size(); i++) {
            cout << i + 1 << ". " << matchingCars[i]->getType() << " " << matchingCars[i]->getMake() << " " << matchingCars[i]->getModel() << endl;
        }

        int choice;
        cout << "Enter the number of the car you want to rent: ";
        cin >> choice;

        if (choice >= 1 && choice <= matchingCars.size()) {
            Car* chosenCar = matchingCars[choice - 1];
            cout << "You have rented a " << chosenCar->getType() << " car for " << days << " days." << endl;
            cout << "Details of the rented car:\n";
            cout << *chosenCar;
            return chosenCar;
        } else {
            cout << "Invalid choice. Rental canceled." << endl;
            return nullptr;
        }
    }
}



private:
    static const int MaxCars = 20;
    Car* cars[MaxCars] = {nullptr};
    int carCount = 0;
};

int main() {
    RentalSystem rentalSystem;

    rentalSystem.addCar(new EconomyCar("Toyota", "Corolla", 2022));
    rentalSystem.addCar(new LuxuryCar("Mercedes", "E-Class", 2022));
    rentalSystem.addCar(new SUV("Ford", "Explorer", 2022));
    rentalSystem.addCar(new SixSeater("Honda", "Odyssey", 2022));
    rentalSystem.addCar(new SixSeater("Honda", "BR-V", 2022));
    rentalSystem.addCar(new SixSeater("SKODA", "SLAVIA", 2022));
    rentalSystem.addCar(new SixSeater("FORD", "GT", 2022));
    rentalSystem.addCar(new SUV("Ford", "Endeavour", 2022)); 
    rentalSystem.addCar(new SUV("Toyota ", "Fortuner", 2022)); 
    rentalSystem.addCar(new SUV("Hyundai", "Creta", 2022)); 
    rentalSystem.addCar(new SUV("KIA", "SELTOS", 2022)); 
    rentalSystem.addCar(new LuxuryCar("Mercedes", "S-Class", 2022));
    rentalSystem.addCar(new LuxuryCar("BMW", "7-Series", 2022));
    rentalSystem.addCar(new LuxuryCar("Audi", "A-8", 2022));
    
    rentalSystem.addCar(new EconomyCar("SUZUKI", "SWIFT", 2022));
    rentalSystem.addCar(new EconomyCar("SUZUKI", "WAGONR", 2022));
    rentalSystem.addCar(new EconomyCar("HYUNDAI", "SANTRO", 2022));

    cout << "Available Cars:\n";
    rentalSystem.displayCars();

    int seats, days;
    cout << "Enter the number of seats you need: ";
    cin >> seats;
    cout << "Enter the number of days you want to rent: ";
    cin >> days;

    Car* rentedCar = rentalSystem.rentCar(seats, days);

    if (rentedCar != nullptr) {
        double totalCost = rentedCar->getDailyRate() * days;
        cout << "Total Cost: $" << totalCost << "\n";
    }

    return 0;
}
