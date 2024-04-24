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

Ingredient input field

.. code-block:: dart
    child: TextField(
            controller: _ingredientController,
            decoration: const InputDecoration(
              hintText: 'Enter ingredient',
            ),
          ),
        ),

Quantity input field

.. code-block:: dart
    child: TextField(
            controller: _quantityController,
            keyboardType: TextInputType.number,
            decoration: const InputDecoration(
              hintText: 'Quantity',
            ),
          ),

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

