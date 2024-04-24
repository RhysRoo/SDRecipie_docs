Login Page
==========

What to see
----------

On the login page, you are displayed with 2 input text boxes. These text fields allow the user to input an email address and password. If the login details don't match the backend (Firebase Auth), then the authentication will fail and the user will be prompted to try again.

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
