VROOM VROOM is a sophisticated command-line application that faithfully emulates the experience of renting a vehicle. This user-friendly software allows customers to effortlessly browse a wide selection of available cars, handpick their preferred vehicle, and instantly determine the total cost of their rental. Developed using C++, this project leverages the principles of object-oriented programming, including advanced techniques such as polymorphism, inheritance, and operator overloading, to deliver a seamless and intuitive user experience.


Key Features

The Rental Car System offers the following key features:

1. Diverse Car Selection: Users can choose from different car types, including Economy, Luxury, SUVs, and Six Seaters, catering to various needs.

2. Effective Resource Management: The system maintains a list of available cars and their details, ensuring efficient resource usage.

3. Accurate Monetary Handling: The system calculates the total cost of the rental, taking into account the selected car type and the duration of the rental. It also displays the total cost to the user.

Key Object-Oriented Concepts Demonstrated

The project effectively demonstrates several important object-oriented concepts:

1.Abstraction: The project demonstrates abstraction by defining the base class Car as an abstract class, making it impossible to create instances of this class. This enforces a clear separation between the common characteristics of cars and the specific details of individual car types.

2. Polymorphism: The base class `Car` serves as an abstract base class, and its derived classes override the `getType` function to provide specific details for each car type. This allows different car types to be treated uniformly.

3. Friend Function: Two friend functions, `operator<<` and `rentCar`, are defined. These functions are not members of the `Car` class but have access to its private members. The `operator<<` function is used to display car details, while the `rentCar` function is responsible for renting a car.

4. Operator Overloading: The `operator<<` function overloads the `<<` operator for displaying car details. This demonstrates the use of operator overloading in the project.

5. Inheritance: The derived classes, such as `EconomyCar`, `LuxuryCar`, `SUV`, and `SixSeater`, inherit from the base class `Car`. They inherit data members and overridden functions, promoting code reusability.

6.. Encapsulation: Data members in the `Car` class, such as `make`, `model`, `year`, `seats`, and `dailyRate`, are encapsulated as private. Access is provided through getter functions, ensuring data 
security.
7.Method Overriding: Derived car type classes override methods from the base class to supply specific details tailored to each car type.




In conclusion, Vroom Vroom is more than just a software project; it's a revolution in car rental services. By leveraging C++ and advanced OOP techniques, it has created a bridge between the digital world and the realm of vehicle rentals, delivering a sophisticated, user-centric, and transparent experience that aligns seamlessly with the needs and expectations of modern customers.
