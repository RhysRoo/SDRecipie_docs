WasteAway: Your Personal Food Waste Management App
==================================================

**Overview**

WasteAway is a mobile application designed to help users manage food waste effectively. After creating an account and connecting to our database, users gain access to a variety of features designed to make food waste management simple and intuitive.

Upon entering the homepage, users are greeted with an introductory video that guides them through the app's navigation. An easy-to-understand app drawer, complete with icons, provides quick access to all pages. A sign-out button is also available for users to log out and return to the login page.

**Technology Stack**

Our app leverages the power of the Flutter framework and Firebase database:

- **Flutter** is a cross-platform mobile development framework that allows for a single codebase written in just one language. This not only reduces development costs but also supports hot reloading for a seamless user experience.

- **Firebase** is our chosen backend database, known for its scalability and real-time data syncing capabilities.


Theming
-------

The app's theme is designed to be user-friendly and intuitive. The color scheme is a combination of green colours to represent the environment and the app's purpose. The app's font is also chosen to be easy to read and understand with black on some instances and white on others to provide a good contrast.


How to Run the Application
==========================

There are two ways to run the application:

1. **Using the Terminal:**

   - Change the directory to match the folder that holds all the app's components. In the terminal, enter the following commands:

     .. code-block:: bash

        cd SDrecipe
        cd recipe_app

   - Then, run the application with the following command:

     .. code-block:: bash

        flutter run

2. **Using the Debugger:**

   - Locate the `main.dart` file from the `lib` folder.
   - Choose the debugger to run the application.

.. note::

   WasteAway is currently under active development. Stay tuned for updates!

Table of Contents
=================

.. toctree::
   :maxdepth: 8

   Profile_Page
   api
   recipe_generator
   Ingredients_Manager
   FAQ_Page
   About_Us_Page
   login_page
   Add_Recipe_Page
