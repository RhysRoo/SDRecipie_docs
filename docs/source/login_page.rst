Login Page
==========

What to see
----------

On the login page, you are displayed with 2 input text boxes. These text fields allow the user to input an email address and password. If the login details don't match the backend (Firebase Auth), then the authentication will fail and the user will be prompted to try again.

Authentication page class
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


