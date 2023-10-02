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
Since there is a large list of features of different or even contradictory natures, such as the normal and the client-server implementations, the design will either be complex, or have two seemingly separate designs, for two different applications, toggled by certain criterias.
