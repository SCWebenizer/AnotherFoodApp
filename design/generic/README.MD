PLANNED FEATURES
1.The idea is to have a food application, in which the user can:
- Add, modify, and delete information about foods through an UI
- Store, load, and delete information about foods, from the disk
- Food can range from the simple raw food, to cooked foods or meals
- View filtered foods based on nutrition, categories, brands, preparation duration and other things, without expressions
- Add macronutrients values for simple foods
- See what are the foods with the highest quantities in certain macronutrients, without expressions
- Save and load settings from a configuration file for the application



2.In the next big update, the user can also:
- Add a history system or timestamp value, both for showing when was a food last eaten, and possibly filter by the foods in the last 7 days. Eventually, an easy to access button to mark which was the last eaten food, as going to look and filter for one food may be tedious and slow
- See the nutrition amounts for a certain amont of a food, or of a food combination
- Update foods to include micronutrient information, and have the same functionalities apply for them
- specify brands for foods, acting as separate foods
- Add recipes, with preparation information, duration, quantities, requirements, and the used tools, and with eventual possible alternate recipes or information on what adding more or less of certain ingredients will affect the final recipe
- Calculate estimated nutritional values of cooked foods or meals, based on input and resulting quantities, and cooking methods
- Filter and sort foods in certain orders
- Have ways to interact or automate the application usage with the command line interface (CLI)



3.And finally, in the future, the user can:
- Run the application with a GUI
- Add the foods they have as a form of inventory, and see what can be made with them, while being able to filter them on the same criterias as above
- Add a schedule system with reminders, in order to be able to plan out a week
- Possibly run the application as a server, with a database available and a separate client application is used on a separate computer. This could be done as a CLI argument when starting the application





(Semi-)TECHNICAL DESIGN
The application can be divided into a generic or abstract part, and a food data part. This is more of a observation or logical separation, and the actual component separation should be done in classic software architectural design fashion.

1.The food data part of the application, would represent features such as:
- Having the data represent foods, from the simplest ingredient that may not even be eatable, to complex, cooked foods (implementation)
- Having different categories and nutritional quantities for each food (implementation)
- Having different ways to filter the food types (implementation)
- The CLI arguments (implementation)



2.The generic part of the application, would represent features such as:
- Presenting menus with options to the standard output
- Accepting inputs from standard input
- Writing data values to the standard output
- Storing data values on the disk
- Modify existing data with new values, or deleting it
- The stored data value is in a format that can be updated or changed in future versions, probably JSON (implementation)
- The ability to filter or sort data in a certain order, based on a data field
- Saving and loading application settings in a local file
- Parsing and using CLI arguments
- The ability to filter or sort data in a certain order, based on complex expressions
- Having the ability to switch to the client and server implementation





TECHNICAL DESIGN
Since there is a large list of features of different or even contradictory natures, such as the normal and the client-server implementations, the final software architecture will either be complex, or have two seemingly separate designs, for two different applications, toggled by certain criterias.

Any classes marked with a '(*)' means that it will be implemented in the future.
Any classes marked with a '(?)' means that it might not get implemented. It is a suggestion or idea of how the design can look.



1.There is a class representing the food data, and all of its possible fields.
It contains:
    * name, type, brand, quantity, for identification
    * specification whenever it is a simple kind of food, or is a result of cooking or combining other foods
    * the served amount of this food, on average, by itself or as a result of cooking other foods
    * The foods used in preparing this one, and their quantities
    * calorie amount per 100g, either given or calculated from macronutrient data
    * macronutrient amounts, for carbohydrates, sugars, types of fats, and proteins (and if the proteins cover everything) per 100g
    * micronutrient amounts, per 100g (*)
    * timestamp of when it was last eaten or used in a food that was eaten (*)
    * Setters, getters, initialization and delete methods
    * normal or overriden (language dependent) printing method
Food can range from the simple raw food, to cooked foods or meals
- View filtered foods based on nutrition, categories, brands, preparation duration and other things, without expressions
- Add macronutrients values for simple foods

2.There is an interface for reading and writing data from an abstract source.
Several classes implement this interface:
    * one interacts with the standard interfaces.
    * one interacts with the file system. (*)
    * one interacts with the GUI. (*)
    * one interacts with the CLI. (*) (?)
    * one interacts with the network interface. (*) (?)
//On some of those implementations, a buffered version could be done. Perhaps a future interface just for those?
//At least the standard interfaces class will present a menu to the standard output, and await reading inputs from the standard input.
//The GUI one also presents a menu.
//The CLi one just reads and parses the program arguments, and prints some information to the standard output, eventually offering some feedback about how it is being ran, unless there is a quiet mode. It is kind of a bit combined with the writing part of the standard interface class implementation, minus the menus.
//The network interface implementation will not present any menus, as the actual menu will be present on the client application. Instead, it will send and receive data, prefferably over a stable connection, like TCP. It might still print some information to standard output or standard error however.
//Unsure if the interface and the classes should be split into reader and writer interfaces and classes.


3.There is a class acting both as a wrapper for a food collection, and as the internal state of the application.
It contains methods for:
    * initiating and loading each food object, as a first stage
    * Linking the cooked foods to the existing ones, as a second stage
    * returning the entire food collection.
    * returning a new food collection with filtered objects, or in a sorted matter.
    * adding a food object argument to the collection.
    * adding the contents of a food collection argument to the collection.
    * returning a new food collection with a maximum count of objects. (*)
//This probably can be broken into two parts instead.
//No details on the internal state interactions yet.

4.The class implementing the reading and writing interface for the standard interfaces will have several different menus that can be explored. Inputs are awaited, and prints of the current menu are done.
//One of the menus will actually interact with the food collection wrapper, and display food objects
//Unsure how to design here yet.
