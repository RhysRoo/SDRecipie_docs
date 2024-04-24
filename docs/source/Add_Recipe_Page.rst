Add Recipe Page
================

Creating Recipes
----------------

On this page, you can create recipes by following these steps:

1. **Naming the Recipe**: You can name your recipe anything you want.

2. **Entering Food Restrictions**: You will be required to enter any food restrictions you may have, such as vegan, vegetarian, gluten-free, etc.

3. **Entering Ingredients**: You will need to enter the ingredients you want to use in your recipe.

4. **Entering Units**: After entering the ingredients, you will need to specify the units for each ingredient, such as weight (cups, grams, etc.).

Checking Ingredients
--------------------

Once you're finished, click the plus button to send the query. The ingredients will be checked with an API to verify their validity. This ensures that the ingredients are valid and can be matched with active ingredients to be made into recipes.

Pending Recipe Ingredients
--------------------------

Everytime you add an ingredient to the recipe, it will be added to the "Pending Recipe Ingredients" section. You can see the ingredients you have added and the units you have added them in. You can also delete the ingredients from this section if you have made a mistake.

View Recipes
------------

After creating a recipe, you can view it on the "View Recipes" page. You can also edit or delete the recipe from this page. When the window of the created recipes is clicked you will be able to rate the recipe from 0 - 5 stars, see the date it was created in yyyy-mm-dd format. If you click on the created recipe ypu will be able to see the ingredients and the units of the ingredients. 

Text Fields
-------

You can enter the name of the recipe, the food restrictions, the ingredients, and the units in the text fields provided.

*Ingredient input field*

.. code-block:: dart

        child: TextField(
                controller: _ingredientController,
                decoration: const InputDecoration(
                    hintText: 'Enter ingredient',
                ),
        ),

*Quantity input field*

.. code-block:: dart

    child: TextField(
            controller: _quantityController,
            keyboardType: TextInputType.number,
            decoration: const InputDecoration(
              hintText: 'Quantity',
            ),
          ),

Adding Ingredients
------------------

The following code block represents a function in Dart named `_addIngredient`. This function is asynchronous, meaning it can perform operations that might take some time to complete, such as fetching data from an API or validating input.

.. code-block:: dart

        Future<void> _addIngredient() async {
                String ingredient = _ingredientController.text;
                String quantity = _quantityController.text;

                // Validation: Check if ingredient and quantity are not empty
                if (await _validateIngredient(ingredient, quantity)) {
                    setState(() {
                        _ingredients.add({
                            'ingredient': ingredient,
                            'quantity': quantity.isNotEmpty ? '$quantity $_selectedUnit' : null,
                        });
                        _ingredientController.clear();
                        _quantityController.clear();
                        _selectedUnit = 'Select Unit';
                    });
                    print(_ingredients);
                }
        }

The function `_addIngredient` retrieves the text from two text fields: one for the ingredient name and one for the quantity. It then validates these inputs using the `_validateIngredient` function. If the inputs are valid, the function updates the state of the application.

In the updated state, a new ingredient is added to the `_ingredients` list. Each ingredient is a map with two keys: 'ingredient' and 'quantity'. The 'ingredient' key maps to the name of the ingredient, and the 'quantity' key maps to the quantity of the ingredient, combined with the selected unit. If no quantity is provided, the 'quantity' key maps to `null`.

After adding the new ingredient, the function clears the text fields and resets the selected unit to 'Select Unit'. Finally, it prints the updated list of ingredients to the console.

Buttons
-------

On the main add recipe page there 4 buttons on display but more under view recipes.

**Add Ingredient Button**

- Add ingredient button: is displayed as a plus symbol that allows the user experience to be seamless

- Save Recipe Button: is a button that allows the user to save the recipe they have created with all the ingredients and units

- View Recipes Button: is a button that allows the user to view all the recipes they have created in a isloated environment

- Clear Ingredients Button: is a button that allows the user to clear all the ingredients they have in the queue to be added to recipe.

**View Recipes Buttons**

- Delete Recipe Button: is a button that allows the user to delete the recipe they have created
- View more information Button: is a button that allows the user to view more information about the recipe they have created

.. code-block:: dart

    ElevatedButton(
            onPressed: () {
              Navigator.push(
                context,
                MaterialPageRoute(builder: (context) => const ShowRecipePage()),
              );
            },
            style: ElevatedButton.styleFrom(
              backgroundColor: const Color.fromARGB(255, 75, 175, 80),
            ),
            child: const Row(
              children: [
                Icon(Icons.cookie_outlined),
                SizedBox(width: 8.0),
                Text('View Recipes'),
              ],
            ),
          ),

ShowIngredients function

    This function is used to display the ingredients in a popup dialog box.

.. code-block:: dart

    void _showIngredientsPopup(BuildContext context, String recipeName,
      List<Map<String, dynamic>> ingredients) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Ingredients for $recipeName'),
          content: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            mainAxisSize: MainAxisSize.min,
            children: [
              for (final ingredient in ingredients)
                Text(
                  '${ingredient['quantity'] ?? 'Quantity not specified'} of ${ingredient['ingredient']}',
                  style: const TextStyle(fontSize: 14),
                ),
            ],
          ),
          actions: [
            const SizedBox(
              height: 15,
            ),
            TextButton(
              onPressed: () {
                Navigator.of(context).pop(); // Close the dialog
              },
              child: const Text('Close'),
            ),
          ],
        );
      },
    );
  }
    

**Delete Recipes**

.. code-block:: dart

    // Function to delete a recipe
    Future<void> _deleteRecipe(
        String recipeName, List<Map<String, dynamic>> ingredients) async {
    try {
        await addRemoveRecipeManager.deleteRecipe(recipeName, ingredients);
        // Update the state to reflect the changes
        await _fetchRecipes();
    } catch (e) {
        print("Error deleting recipe: $e");
    }
    }


**Rating Recipe Button**

