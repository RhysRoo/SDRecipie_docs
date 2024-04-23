=================
Ingredients_Manager
=================

**Purpose of this Page**
The ingredients manager is a page allowing the user to input ingredients they have lying around in the house, the quantity, as well as the expiry date of the select item.

**Input Fields**
This page has 3 input fields for the user to enter before the select ingredient can be added to the list of ingredients as the validation rule permits it.

- Enter ingredient: this is the name of the select ingredient e.g. Rice and must be String values.
- Enter grams: This is the quantity of the selected ingredient and must be Integer values.
- This is the expiry date of the select ingredient. for example must follow yyyy-mm-dd format and Integer values.

**Buttons** 
There is 3 buttons on this page:
* Add button: The add button is used to add all the entered ingredients to the database
* Save button: The save button is used to save all changes to the page.
* Individual delete button: The individual delete button is used to remove the select ingredients from the list of ingredients.

**indivdual Ingredient**
Each individual ingredient is separated by a card, which allows clean and simplistic spacing between all ingredient elements.

**Open_food_Api**
* The open food API calls and recieves from https://world.openfoodfacts.org/cgi/search.pl?search_terms=$ingredientName&search_simple=1&action=process&json=1
