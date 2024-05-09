Testing
========

Functional Requirements
------------------------

Login UI and Register_Login_Manager Tests  (Ref UR 1 and 2)
------------------------------------------------------------
See the :doc:`login_page` for more information.

.. list-table:: Login UI and Register_Login_Manager Tests (Ref UR 1 and 2)
   :widths: 5 25 25 25 25
   :header-rows: 1

   * - ID
     - Procedure
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - LogIn onTap Test {}
     - pumpWidget onTap {}
     - Call is true
     - FR Met: Trigger authentication and function is initiated (UR 1 a).
   * - 2
     - LogIn onTap Existence Test {}
     - pumpWidget onTap {}
     - Widget Exists
     - 
   * - 3
     - showOSError()
     - pumpWidget with OSError function applied
     - Notification is generated when Android user attempts to use Apple Sign In
     - SR Met: Error messages elicited to client interface (UR 1 f)
   * - 4
     - showOSErrors()
     - pumpWidget with OSError function applied
     - Notification is generated to display error messages when creating an account
     - SR Met: Error messages elicited to client interface when invalid information entered (UR 1 f).
   * - 5
     - checkEmailValidity()
     - 'example@example.com'
     - True
     - SR Met: User can input, email, passwords, and required information (UR 1, 2 d, e, f). Improved SR: Validation Rules. Password length above 6 characters and no more than 255. Must include 1 @ character. All proposed functions are shown below:
   * - 6
     - checkEmailValidity()
     - 'a@b.c'
     - False
     - 
   * - 7
     - checkEmailValidity()
     - 'example.com'
     - False
     - 
   * - 8
     - checkEmailValidity()
     - 'ex@mple@example.com'
     - False
     - 
   * - 9
     - checkEmailValidity()
     - Long email of over 255 with @example.com
     - False
     - 
   * - 10
     - confirmPassword()
     - 'jam!es123', 'james!es123'
     - True
     - Contains symbol. Length and Match
   * - 11
     - confirmPassword()
     - 'ja!23', 'ja!23'
     - False
     - Length not retained
   * - 12
     - confirmPassword()
     - 'jam!es123', 'dhsdjshgf'
     - False
     - 
   * - 13
     - confirmPassword()
     - 'jafjhsf', 'jafjhsf'
     - False
     - No Symbol
   * - 14
     - passwordLengthCheck()
     - 'NoSymbolPassword123'
     - False
     - 
   * - 15
     - passwordLengthCheck()
     - ''
     - False
     - 
   * - 16
     - passwordLengthCheck()
     - Password Above 255 characters
     - False
     - 
   * - 17
     - passwordLengthCheck()
     - 'Short'
     - False
     - 
   * - 18
     - passwordLengthCheck()
     - 'jam!es123'
     - True
     - 
   * - 19
     - containsSymbol()
     - '#'
     - True
     - 
   * - 20
     - containsSymbol()
     - 'password'
     - False
     - 
   * - 21
     - isWhiteSpace()
     - ' '
     - True
     - 
   * - 22
     - isWhiteSpace()
     - 'world'
     - False
     - 
   * - 23
     - isWhiteSpace()
     - null
     - False
     - 

Beta-Testing (Ref UR 1 and 2)
------------------------------
See the :doc:`login_page` for more information.

.. list-table:: Login UI and Register_Login_Manager Tests (Ref UR 1 and 2)
   :widths: 5 25 25 25 25
   :header-rows: 1

   * - ID
     - Procedure
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - Trigger Sign Up Process and Complete
     - abigailNorman1@gmail.com, Logintest1
     - Pass
     - FR Met: Ability to initiate account creation, upon receiving valid user details. (UR 2 a)\nSR: System should store username and password into backend database (UR 2 g)
   * - 2
     - Trigger Sign In Process and Complete
     - alex_pearso@the_pearsons.com, Logintest2
     - Pass
     - FR Met: Ability to initiate create account process (UR 1 a)
   * - 3
     - Halt Sign In Process
     - alex_pearso@the_pearsons.com, Activation of signIn rather than signUp completion and then back to signUp screen
     - Fail
     - FR Met: System should terminate an ongoing authentication process, providing an immediate halt to user access validation. (UR 2 b).\nFR Change: Doesn’t return to previous sign In details after halt of sign Up process (UR 2 c).
   * - 4
     - Trigger authentication and Halt authentication
     - abigailNorman1@gmail.com, Activation of signUp rather than signIn
     - Pass
     - FR Met: Should terminate an ongoing authentication process, providing an immediate halt to user access validation (UR 1 b, f).
   * - 5
     - Trigger authentication and Halt authentication, Attempt to continue the sign in process
     - alex_pearso@the_pearsons.com, Activation of signUp rather than signIn and then back to signIn screen
     - Fail
     - FR Change: Doesn’t return to previous log in details (UR 1 c)

 
Profile Manager Test (Ref UR 3)
-------------------------------
See the :doc:`Profile_Page` for more information.

.. list-table:: Profile Manager Test (Ref UR 3)
   :widths: 5 25 25 25 25
   :header-rows: 1

   * - ID
     - Function
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - deleteUserDetails()
     - ‘dummyUID’
     - Returns Null
     - 
   * - 2
     - deleteUserDetails()
     - ‘nullUID’ : Unauthorised 
     - Returns Null
     - 
   * - 3
     - storeUserDetails()
     - UserModel = {age:‘30’, firstName:‘John’, foodRestriction:‘None’, lastName:‘Doe’, userName:‘johndoes123’, bio:‘Hello I am John Doe’} on “dummyUID”
     - Returns Snapshot Exists and firstName:’John’
     - FR Met: Create and Manage a profile with personal information and preferences (UR 3 a)
   * - 4
     - storeUserDetails()
     - UserModel = {age:‘30’, firstName:‘John’, foodRestriction:‘None’, lastName:‘Doe’, userName:‘johndoes123’, bio:‘Hello I am John Doe’} on “dummyUID”
     - Returns Snapshot is greaterThan 0
     - SR Patially Met: Create their profiles, allowing input of information (UR 3 c).
   * - 5
     - storeUserDetails()
     - No Stored Data
     - Returns Null
     - FR Met: Secure authenticate and authorise mechanisms to safeguard user profile (UR 3 b).
   * - 6
     - getUserDetails()
     - UserModel = {age:‘30’, firstName:‘John’, foodRestriction:‘None’, lastName:‘Doe’, userName:‘johndoes123’, bio:‘Hello I am John Doe’} on “dummyUID”
     - Returns entire snapshot of information for usage
     - SR Met: System consists of a module for users to create and manage their profiles allowing them to input and update personal information (UR 3 c). SR Met: System should store user inputs into the backend (UR 3 e)
   * - 7
     - getUserDetails()
     - Null UID
     - Returns Null
     - 
   * - 8
     - checkInputLength()
     - ‘This is an example bio’
     - Returns True
     - 
   * - 9
     - checkInputLength()
     - Bio that exceeds 255
     - Returns False
     - SR Partially Met: User bio should be less than 200 characters (UR 3 d)
   * - 10
     - checkInputLength()
     - ‘’
     - Returns False
     - 

User Manager Test (Rf UR 3)
---------------------------
See the :doc:`Profile_Page` for more information.

.. list-table:: User Manager Test (Rf UR 3)
   :widths: 5 25 25 25 25
   :header-rows: 1

   * - ID
     - Function
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - getUserUID()
     - ‘dummyUID’
     - Returns dummyUID
     - 
   * - 2
     - getUserUID()
     - null
     - Returns null
     - 
   * - 3
     - getFoodRestriction()
     - foodRestriction: ‘Vegetarian’ on ‘dummyUID’
     - Returns Vegetarian
     - 
   * - 4
     - getFoodRestriction()
     - foodRestriction: ‘N/A’ on ‘dummyUID’
     - Returns N/A
     - 
   * - 5
     - getFoodRestriction()
     - Null
     - Returns Null
     - 
   * - 6
     - toJson()
     - UserModel Instance
     - Returns {‘firstName’: ‘john’, ‘lastName’: ‘doe’, ‘username’: ‘johndoe’, ‘age’: ‘30’, ‘foodRestiction’: ‘vegetarian’}
     - 

Ingredient Manager Tests (Ref UR 4)
-----------------------------------

.. list-table:: Ingredient Manager Tests (Ref UR 4)
   :widths: 5 25 25 25 25
   :header-rows: 1
   See the :doc:`Ingredients_Manager` for more information.

   * - ID
     - Function Name
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - storeUserIngredients()
     - {{‘Lemon’, ‘30’, ‘2024-07-03’}} on ‘dummyUID’
     - Returns {{‘Lemon’, ‘30’, ‘2024-07-03’}} and Snapshot Stored
     - 
   * - 2
     - storeUserIngredients()
     - {{‘Lemon’, ‘30’, ‘2024-07-03’}} on nullID
     - Returns {}
     - 
   * - 3
     - getIngredients()
     - {{‘Lemon’, ‘30’, ‘2024-07-03’}} on ‘dummyUID’
     - Returns {{‘Lemon’, ‘30’, ‘2024-07-03’}} on ‘dummyUID’
     - 
   * - 4
     - getIngredients()
     - {{‘Lemon’, ‘30’, ‘2024-07-03’}, {‘Melon’, ‘30’, ‘2024-07-01’}}
     - Returns {{‘Lemon’, ‘30’, ‘2024-07-03’}, {‘Melon’, ‘30’, ‘2024-07-01’}}
     - 
   * - 5
     - getIngredients()
     - {}
     - {}
     - 
   * - 6
     - validateQuantity()
     - ‘15’
     - True
     - 
   * - 7
     - validateQuantity()
     - ‘5’
     - False
     - 
   * - 8
     - convertStringtoDatetime()
     - ‘2024-03-31’
     - True
     - 
   * - 9
     - convertStringtoDatetime()
     - ‘Invalid Date’
     - False
     - 
   * - 10
     - checkDateAgainstTodaysDate()
     - ‘2024-03-31’
     - False
     - 
   * - 11
     - checkDateAgainstTodaysDate()
     - ‘2024-08-02’
     - True
     - 
   * - 12
     - checkDateAgainstTodaysDate()
     - ‘’
     - False
     - 
   * - 13
     - checkUserDatetime()
     - ‘Invalid Datetime’
     - False
     - 
   * - 14
     - checkUserDatetime()
     - ‘’
     - False
     - 
   * - 15
     - checkUserDatetime()
     - ‘2024-02-02’
     - True
     - 

Open Food Api Tests (Ref UR 4, 8)
--------------------------------
See the :doc:`Ingredients_Manager` for more information.

.. list-table:: Open Food Api Tests
   :widths: 5 20 20 10 35
   :header-rows: 1

   * - ID
     - Function
     - Test Inputs
     - Result
     - Description to meet specification
   * - 1
     - ingredientAPICheck()
     - ‘eggs’
     - True
     - SR Met: Validates ingredient names (UR 4 g).
   * - 2
     - ingredientAPICheck()
     - ‘msg’
     - True
     - SR Met (UR 8 c): Validates recipe’s ingredient names.
   * - 3
     - ingredientAPICheck()
     - ‘banana’
     - True
     - 
   * - 4
     - ingredientAPICheck()
     - ‘nullwhjq’
     - False
     - 
   * - 5
     - ingredientAPICheck()
     - ‘’
     - False
     - 
   * - 6
     - ingredientAPICheck()
     - ‘dwjfedfeqgwegewg’
     - False
     - 

API Search Test (Ref UR 4)
----------------------------

.. list-table:: Api Search Test (Ref UR 4)
   :widths: 5 25 25 25 25
   :header-rows: 1
   See the :doc:`recipe_generation_page` for more information.

   * - ID
     - Function
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - fetchRecipesBasedOnUserIngredients()
     - getUserIngredients() = {}
     - Returns isEmpty() == True
     - Changed SR: Validation Rules (UR 4 d)
   * - 2
     - fetchRecipeBasedOnUserIngredients()
     - [[‘Tomato’], [‘Onion’]]
     - Returns results.length > 1 and first recommendationLabel is ‘Tomato Soup’
     - FR Changed: Dynamic generation of top 5 recipes (UR 4 a, g). FR Met: User input, ingredient name and ingredient expiry date to generate recipes (UR 4 b) SR Change: Personalised Engine tailored met (UR 4 f).
   * - 3
     - testPerformance()
     - 
     - True
     - NF SR: Recipes should be generated in less than a few seconds.

Food Notification Manager Tests (Ref UR 4,5)
--------------------------------------------

.. list-table:: Food Notification Manager Tests (Ref UR 4,5)
   :widths: 5 25 25 25 25
   :header-rows: 1
   See the :doc:`home_page` for more information.

   * - ID
     - Function Name
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - removeExpiredIngredientAndNotify()
     - {‘ingredients’: {‘name’: ‘Lemon’, ‘weight’: ‘30’, ‘expiryDate: ‘2021-07-03’}} on ‘dummyUID’
     - removedIngredients return of length 1 item. With name ‘Lemon’ and ‘2021-07-03’ expiryDate
     - FR: Notification can be displayed to the UI interface (UR 5 a).
   * - 2
     - removeExpiredIngredientAndNotify()
     - {‘ingredients’: {‘name’: ‘Lemon’, ‘weight’: ‘30’, ‘expiryDate: ‘2021-07-03’}, {name: ‘Melon’, ‘weight’: ‘30’, ‘expiryData’: ‘2025-07-03’}} on ‘dummyUID’
     - Returns : {‘name’: ‘Lemon’, ‘weight’: ‘30’, ‘expiryDate: ‘2021-07-03’} being the expired ingredients to Notify
     - SR Met: Identifies which expired ingredients there are and removes them from the system. For both (UR 4 b, e, g) and (UR 5 c)
   * - 3
     - removedExpiredIngredientAndNotify()
     - {‘ingredients’: {‘name’: ‘Lemon’, ‘weight’: ‘30’, ‘expiryDate: ‘2021-07-03’}, {name: ‘Melon’, ‘weight’: ‘30’, ‘expiryData’: ‘2025-07-03’}, {‘name’: ‘Carrot’, ‘weight’: ‘30’, ‘expiryDate: ‘2022-07-03’}, {‘name’: ‘Lemon’, ‘weight’: ‘30’, ‘expiryDate: ‘2023-01-03’}} on ‘dummyUID’
     - Returns {‘name’: ‘Lemon’, ‘expiryDate: ‘2021-07-03’,name:‘Carrot’,‘expiryDate: ‘2022-07-03’, ‘name’: ‘Lemon’, ‘expiryDate: ‘2023-01-03’}
     - 
   * - 4
     - removedExpiredIngredientAndNotify()
     - {‘ingredients’: {‘name’: ‘Lemon’, ‘weight’: ‘30’, ‘expiryDate: ‘2021-07-03’}, {name: ‘Melon’, ‘weight’: ‘30’, ‘expiryData’: ‘2025-07-03’}, {‘name’: ‘Carrot’, ‘weight’: ‘30’, ‘expiryDate: ‘2022-07-03’}, {‘name’: ‘Lemon’, ‘weight’: ‘30’, ‘expiryDate: ‘2023-01-03’}} on null UID
     - Return {}
     - 
   * - 5
     - warnEfficiency()
     - 95% efficiency 
     - Returns True 
     - SR Met Partially: Notification generated for efficiency warning. Efficiency system not implemented (UR 5 b).

Add Recipe Manager Tests (Ref UR 8)
-----------------------------------

.. list-table:: Add Recipe Manager Tests (Ref UR 8)
   :widths: 5 20 20 10 25
   :header-rows: 1
   See the :doc:`Add_Recipe_Page` for more information.

   * - ID
     - Function Name
     - Test Inputs
     - Result
     - Description to Meet Specification (Ref SR and FR)
   * - 1
     - deleteRecipe()
     - {‘ingredient1’, ‘ingredient2’, ‘ingredient3’} associated with ‘dummyUID’
     - Document doesn’t exist
     - New FR: Users should be able to remove recipes that have been created by them.
   * - 2
     - deleteRecipe()
     - {‘ingredient1’, ‘ingredient2’, ‘ingredient3’} associated with null UID
     - Document doesn’t exist due to Error
     - Partially Met (UR 8 d): Additional validation rules
   * - 3
     - deleteRecipe()
     - {‘ingredient1’, ‘ingredient2’, ‘ingredient3’, ‘ingredient4’} with ‘dummyUID’
     - Document doesn’t exist
     - FR Met: Ensures that users can only delete recipes associated with their UID.
   * - 4
     - saveRecipe()
     - {{‘ingredient1’, ‘quantity1’},{ ‘ingredient2’, ‘quantity2’}} with ‘dummyUID’ and ‘None’ food restriction
     - Recipe Stored, shown through retrieval
     - FR succeeded: Users can submit their recipes in terms of a form. (UR 8 a, c)
   * - 5
     - saveRecipe()
     - {{‘ingredient1’, ‘quantity1’},{ ‘ingredient2’, ‘quantity2’}} with ‘null’ UID and ‘None’ food restriction
     - {} Unauthorised
     - Partially Met (UR 8 d): Additional validation rules
   * - 6
     - getAllRecipes()
     - Unauthorised access
     - {} Unauthorised
     - NF SR: System must prevent unauthorized access to recipe data.
   * - 7
     - getAllRecipes()
     - {‘ingredients’: {‘ingredient1’, ‘ingredient2’, ‘ingredient3’}}
     - {‘ingredients’: {‘ingredient1’, ‘ingredient2’, ‘ingredient3’}}
     - FR Met: System should correctly retrieve all recipes containing specified ingredients.


FAQ Page Test (Ref UR 9)
-------------------------

.. list-table:: FAQ Page Test (Ref UR 9)tle
   :widths: 5 25 25 25 25
   :header-rows: 1
   See the :doc:`FAQ_Page` for more information.

   * - ID
     - Function
     - Test Inputs
     - Result
     - Description to Meet Specification
   * - 1
     - FAQ_Page()
     - pumpWidget() : Structural Expectation
     - True
     - SR: Must develop a module that organises common user queries in a structured format (UR 9 a)
   * - 2
     - FAQ_Page()
     - pumpWidget() : Structural Expectation
     - True
     - Changed SR: FAQ Questions and Query Content are less than 200 characters (UR 9 f)

Non-Functional Test:
--------------------

.. list-table:: Non-Functional Test
   :widths: 5 20 15 15 10 20
   :header-rows: 1

   * - ID
     - Procedure
     - Inputs
     - Description
     - Result
     - Description to Meet Specification
   * - 1
     - Integration of Third Party Services can be identified through ‘open_food_facts’ and ‘Adaman API’
     - See tests
     - Compatibility
     - True
     - NF SR: The system must be able to integrate third party services.
   * - 2
     - Tested through development of the project as Flutter Environments can load the project onto both services.
     - Run application
     - Compatibility
     - True
     - NF Change: The system must be compatible with IOS devices and Chrome Services.
   * - 3
     - Determined at a development time of 20.2s for application build.
     - Run application
     - Performance
     - 
     - NF SR: System must respond within a maximum response time of 30 seconds.
   * - 4
     - Determined at a 2s response time seen through function testPerformance() for Adaman API.
     - Run application
     - Performance and Reliability
     - 
     - NF SR: Recipe generation is efficient and recipes load in less than a few seconds
   * - 5
     - Use of Google Cloud sign in processes.
     - Beta-Testing for (UR 1 and 2)
     - Security and Reliability
     - True 
     - NF SR: Authentication and authorisation mechanisms must adhere to industrial-standard protocols to safeguard user authentication and profile information.
   * - 6
     - Encryption of information was not used before filtering to Google Services.
     - Beta-Testing for (UR 1 and 2)
     - Security
     - Failed for Encryption, Passed for Unauthorised access.
     - NF SR Partially Met: User data, profiles, submitted recipes, and ratings, must be stored and transmitted securely using encryption methods to protect against unauthorised access.
   * - 7
     - Widget test to show presence of widget menu and layouts with associated functionality.
     - ‘home_page_tests’
     - Usability
     - True
     - NF SR: Navigation menu is intuitive with a user-friendly layout and useful tooltips.
   * - 8
     - All previous tests. An extensive amount of validation rules for our system have been developed.
     - ‘ingredient_manager_tests’
     - Quality Assurance
     - True
     - NF SR: Rigorous testing procedures, e.g., security testing, must be conducted to ensure the overall reliability and integrity of the system.
