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

.. code-block:: dart

     Future<List<dynamic>> fetchRecipes(List<String> ingredients) async {
    const String apiId = '87adcf60';
    const String apiKey = 'APIKEY';

    String ingredientQuery = ingredients.join(',');

    String url = 'https://api.edamam.com/search?app_id=$apiId&app_key=$apiKey&q=$ingredientQuery&to=10';

    try {
      final response = await http.get(Uri.parse(url));
      if (response.statusCode == 200) {
        Map<String, dynamic> data = json.decode(response.body);
        List<dynamic> recipes = data['hits'];
        return recipes;
      } else {
        throw Exception('Failed to load recipes');
      }
    } catch (e) {
      print(e.toString());
      return [];
         }
       }

In this code block, the `fetchRecipes()` method fetches recipes from the Edamam API based on the user's selected ingredients(Saved in from the ingredients manager page). It constructs a URL with the API ID, API key, and user ingredients, sending an HTTP GET request to the API. after this it parses the response data to extract the recipe information.

- **fetchRecipesBasedOnUserIngredients():** Fetches recipes from the Edamam API based on the user's selected ingredients.

- **getRecipeNames():** Retrieves the names of recipes generated based on user ingredients.

.. code-block:: dart

      Future<List<String>> getRecipeNames() async {
    List<dynamic> recipes = await fetchRecipesBasedOnUserIngredients();
    List<String> labels = [];

    for (int i = 0; i < recipes.length && i < 5; i++) {
      Map<String, dynamic> recipe = recipes[i]['recipe'];
      labels.add(recipe['label']);
    }
    return labels;
       } 

- **getRecipeUrls():** Retrieves the URLs of recipes generated based on user ingredients.

.. code-block:: dart

      Future<List<String>> getRecipeUrls() async {
    List<dynamic> recipes = await fetchRecipesBasedOnUserIngredients();
    List<String> urls = [];

    for (int i = 0; i < recipes.length && i < 5; i++) {
      Map<String, dynamic> recipe = recipes[i]['recipe'];
      urls.add(recipe['url']);
    }
    return urls;
       }

The `getRecipeUrls()` method retrieves the URLs of recipes generated based on the user's selected ingredients. It calls the `fetchRecipesBasedOnUserIngredients()` method to fetch recipes, then extracts the URLs from the response data and returns them as a list of strings.

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

- **Factory Design Pattern:** The `fromJson()` constructor uses the factory design pattern to create instances of the `Recipe` and `Ingredient` classes from JSON data. The purpose of the factory design pattern method is a creational design pattern that provides an interface for creating objects in a superclass.

.. code-block:: dart
  factory Recipe.fromJson(String json) {
    final parsed = jsonDecode(json)['recipe'] as Map<String, dynamic>;
    return Recipe(
      label: parsed['label'],
      image: parsed['image'],
      source: parsed['source'],
      url: parsed['url'],
      shareAs: parsed['shareAs'],
      yield: parsed['yield'],
      dietLabels: List<String>.from(parsed['dietLabels']),
      healthLabels: List<String>.from(parsed['healthLabels']),
      cautions: List<String>.from(parsed['cautions']),
      ingredientLines: List<String>.from(parsed['ingredientLines']),
      ingredients: (parsed['ingredients'] as List<dynamic>)
          .map((ingredient) => Ingredient.fromJson(ingredient))
          .toList(),
      cuisineType: parsed['cuisineType'] ?? '',
      mealType: parsed['mealType'] ?? '',
      dishType: List<String>.from(parsed['dishType'] ?? []),
      totalTime: parsed['totalTime'] ?? '',
      recipeYield: parsed['recipeYield'] ?? '',
      calories: List<String>.from(parsed['calories'] ?? []),
      totalWeight: List<String>.from(parsed['totalWeight'] ?? []),
      totalNutrients: List<String>.from(parsed['totalNutrients'] ?? []),
      totalDaily: List<String>.from(parsed['totalDaily'] ?? []),
    );
  }


