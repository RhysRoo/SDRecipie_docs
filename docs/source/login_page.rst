Login Page
==========

**What to see**
On the login page, you are displayed with 2 input text boxes. These text fields allow the user to input an email address and password. If the login details don't match the backend (Firebase Auth), then the authentication will fail and the user will be prompted to try again.

*Authentication page class*

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

