login Page
==========


Introduction
------------

The log in page allows users to authenticate themselves in order to access the application's features and personalized content. 

To use the login page:

1. The user should enter their username or email address in the corresponding input field.
2. Enter their password in the password input field.
3. Click the "Log In" button to authenticate.

Usage
-----

This section describes what the log in folder does:
 
- **Authentication:** Users can create accounts log in using their email address along with their password. The RegisterLoginManager page contains methods for signing in and registering users with Firebase Authentication. 
- **Error Handling:** The login page handles various authentication such as incorrect username/password or network errors.
- **Navigation:** After successful authentication, users are typically redirected to the application's main dashboard or home screen.


Maintenance
===========

The Maintenance section describes how the software achieves its functionality and how developers can maintain and extend it. 

The login folder has more than three files in it. Here are the uses of the most important files:
- `Login_page.dart`: This file represents the UI of the login page. It includes text fields for users to input their email and password, as well as buttons for signing in with email/password, Google, and Apple.
  - `Register_page.dart`: Similar to the `Login_page.dart`, this file represents the UI of the registration page. It allows users to create a new account by providing their email and password.
  - `register_login_manager.dart`: This file contains methods for signing in and registering users. It handles Firebase authentication and error handling.

**The classes and functions that are relevant are summarised as follows:**

Authentication Page Class
------------------------

.. code-block:: dart

   class AuthPage extends StatelessWidget {
       const AuthPage({super.key});

       @override
       Widget build(BuildContext context) {
           return Scaffold(
               body: StreamBuilder<User?>(
                       stream: FirebaseAuth.instance.authStateChanges(),
                       builder: (context, snapshot) {
                           // User is logged in
                           if (snapshot.hasData) {
                               return const HomePage();
                           }

                           // User is not logged in
                           else {
                               return const LoginOrRegisterPage();
                           }
                       }),
           );
       }
   }

Logo Image
-----------

There is a logo image on the login page that is directly above the user input fields. This code is a seperate class with all the attributes of the tiled image.

.. code-block:: dart

     // A Tile for the logo
     class LogoTiling extends StatelessWidget {
         final String imagePath;
         const LogoTiling({super.key, required this.imagePath});

         @override
         Widget build(BuildContext context) {
             return Container(
                 padding: const EdgeInsets.all(10),
                 decoration: BoxDecoration(
                     border: Border.all(color: Colors.white),
                     borderRadius: BorderRadius.circular(16),
                     color: Colors.grey[200],
                 ),
                 child: Image.asset(
                     imagePath,
                     height: 250,
                 ),
             );
         }
     }

.. code-block:: dart

    const LogoTiling(imagePath: 'assets/images/logo/logo.png')

Signin With Apple and Google
--------------------------

On the app it allows the user to log straight into the application with Apple and Google. This is a convenient way for the user to gain access in a fast and easy way and makes it easy as no additional passwords are required to gain access.

.. code-block:: dart

    // Apple and Google Sign In
    final GoogleSignInHandler _googleSignInHandler = GoogleSignInHandler();
    final AppleSignInHandler _appleSignInHandler = AppleSignInHandler();

Register Button
---------------

The register button allows the user to create a account if there not registered - prompting the user to enter a email address and password that will communicate with the database to see if the username and password are both unique, before allowing the account to be created. The register_login_manager.dart handles all the operations.

.. code-block:: dart

    Future<String> signUserUp(
      BuildContext context,
      TextEditingController emailController,
      TextEditingController passwordController,
      TextEditingController confirmPasswordController) async {
    final String email = emailController.text.trim();
    final String trimmedPassword = passwordController.text.trim();
    final String trimmedConfirmPassword = confirmPasswordController.text.trim();

    showDialog(
      context: context,
      builder: (context) {
        return const Center(
          child: CircularProgressIndicator(),
        );
      },
    );

**Check Email Validity**

.. code-block:: dart

   bool checkEmailValidity(final String email) {
       if (email.length >= 3 && email.length < 254 && email.contains('@')) {
           var atIndex = email.indexOf('@');
           // Split the email string by "@" and check if there are exactly two parts
           return atIndex >= 3 && email.split('@').length == 2;
       }
       return false;
   }

**Password Confirmation**

This function is a validation rule that checks that the password is the same as the confirmation password.

.. code-block:: dart

    bool confirmPassword(final String passwordOne, final String passwordTwo) {
    if (samePassword(passwordOne, passwordTwo) &&
        passwordLengthCheck(passwordOne)) {
      return true;
    }
    return false;
  }

**Password Length Checker**

Upon creating a password the user has a given validation rule, that checks the given length of the password. if the password doesnt match the given rule. The user will be assigned to try again until the rule has beem met.

.. code-block:: dart

  bool passwordLengthCheck(final String passwordOne) {
  if ((passwordOne.length >= 6 && passwordOne.length <= 200) &&
      containsSymbol(passwordOne)) {
    return true;
  }
  return false;
  }

**Password Length Checker**

Upon creating a password the user has a given validation rule, that checks the given length of the password. if the password doesnt match the given rule. The user will be assigned to try again until the rule has beem met.

.. code-block:: dart

  bool passwordLengthCheck(final String passwordOne) {
  if ((passwordOne.length >= 6 && passwordOne.length <= 200) &&
      containsSymbol(passwordOne)) {
    return true;
  }
  return false;
  }

**Other Validation Checkers**

This validation rule checks user inputs

.. code-block:: dart

  bool containsSymbol(String input) {
  // Converts input to unicode
  for (var char in input.runes) {
    if (!isAlphaNumeric(char) && !isWhitespace(char)) {
      return true;
    }
  }
  return false;
  }

*This function takes an integer argument charCode, which represents a Unicode character code. The function checks if the provided character code falls within the ranges of alphanumeric characters in the ASCII table*

- Ranges 48 - 57 corresponds to digits 0 - 9
- Ranges 65 - 90 corresponds to uppercase letters A - Z
- Ranges 97 - 122 corresponds to lowercase letters a - z

.. code-block:: dart

  bool isAlphaNumeric(int charCode) {
  return (charCode >= 48 && charCode <= 57) || // 0-9
      (charCode >= 65 && charCode <= 90) || // A-Z
      (charCode >= 97 && charCode <= 122); // a-z
  }

This function checks if the provided character code is equal to 32

.. code-block:: dart

  bool isWhitespace(int charCode) {
  return charCode == 32; // space
  }

