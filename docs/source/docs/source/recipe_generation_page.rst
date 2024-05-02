.. _recipe_generation_page:

Recipe Generation Page
======================

Usage
-----
The recipe_generation_page folder allows users to generate recipes based on their selected ingredients. It comprises three main components:

- **API Search:** The 'api_search.dart' file contains the 'RecipeService' class, which communicates with the Edamam API to retrieve recipes based on user ingredients.

- **Recipe Generation:** The 'generation_page.dart' file implements the 'GenerationPage' widget, which shows created recipes and allows you to refresh the information.

- **Recipe Model:** The `recipe.dart` file defines the `Recipe` and `Ingredient` classes, which represent recipe data fetched from the API.

Each file contributes to the overall functionality of the recipe generation page as follows:

API Search (api_search.dart)
-----------------------------
The `RecipeService` class interacts with the Edamam API to fetch recipes based on user ingredients. It provides the following functionalities:

- **fetchRecipes():** Fetches recipes from the Edamam API using HTTP GET requests and returns a list of dynamic objects representing recipe data.

- **fetchRecipesBasedOnUserIngredients():** Fetches recipes from the Edamam API based on the user's selected ingredients.

- **getRecipeNames():** Retrieves the names of recipes generated based on user ingredients.

- **getRecipeUrls():** Retrieves the URLs of recipes generated based on user ingredients.

Generation Page (generation_page.dart)
--------------------------------------
The 'GenerationPage' widget shows the created recipes and allows users to update them. It has the following components:

- **State Management:** Uses stateful widgets to dynamically manage page content.

- **Refresh Button:** Allows users to refresh the content to generate new recipes based on updated ingredients.

- **Content Display:** Displays the generated recipe titles and their corresponding URLs.

Recipe Model (recipe.dart)
---------------------------
The `Recipe` and `Ingredient` classes represent recipe data fetched from the Edamam API. They provide the following attributes and functionalities:

- **Recipe Class:** Represents a recipe item with various properties such as label, image, source, URL, etc.

- **Ingredient Class:** Represents an ingredient item within a recipe with attributes like text, quantity, unit, and food.

- **fromJson() Constructor:** Parses JSON data into instances of the `Recipe` and `Ingredient` classes.

