Profile Page
=============

The Structure Behind the User Profile Page
------------------------------------------
The user profile page is a page that allows the user to input their personal information. This page is only accessible to the user that is logged in. The user can input their username, name, age, food restriction and a personal bio. The food restriction is very important as it allows the app to put this into account when generating recipies.

Profile Image
-------------

The profile image is a picture of the user that is displayed on the user profile page. 

.. note::

    Not yet implemented: 
    
    The user can upload a picture of themselves to be displayed on the user profile page. The user can also change the picture that is displayed on the user profile page. The user can also delete the picture that is displayed on the user profile page.


Cards
-----

The user profile is made up of cards. Each card is a different section of the user profile. The cards are as follows:

- Username and Food Restriction

- User information (Age, First Name, Last Name, Bio)

Buttons
-------

This page has two buttons that offer some CRUD operations:

- Delete Information (The delete information button allows the user to delete their personal information from the page)

.. code-block:: dart

        Widget _buildActionButtons() {
                return Row(
                    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                    children: [
                        ElevatedButton(
                            onPressed: () {
                                _showDeleteConfirmationDialog();
                            },
                            child: const Text(
                                'Delete Information',
                                style: TextStyle(fontSize: 13),
                            ),
                        ),.. code-block:: dart

    ElevatedButton(
      onPressed: () {
        _showChangeInformationForm();
      },
      child: const Text(
        'Change Information',
        style: TextStyle(fontSize: 13),
      ),
    ),


- Change Information (The change information button allows the user to change/add their personal information on the page)

.. code-block:: dart

        ElevatedButton(
            onPressed: () {
                _showChangeInformationForm();
            },
            child: const Text(
                'Change Information',
                style: TextStyle(fontSize: 13),
            ),
        ),

**Change Information Button Dialogue Box**
----------------

The button dialogue box is a pop-up that appears on the screen when the user clicks on the change information button. The dialogue box has 6 input fields that allow the user to input their personal information. The dialogue has 2 further buttons (Cancel and Save) that allow the user to cancel the operation or save the information that they have inputted.

.. code-block:: dart

    void _showChangeInformationForm() {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: const Text('Change Information'),
          content: SingleChildScrollView(
            child: Form(
              key: _formKey,
              child: Column(
                children: [
                  TextFormField(
                    controller: _usernameController,
                    decoration: const InputDecoration(labelText: 'Username'),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter a username';
                      }
                      if (value.length < 4) {
                        return 'Username must be at least 4 characters';
                      }
                      return null;
                    },
                  ),
                  TextFormField(
                    controller: _ageController,
                    decoration: const InputDecoration(labelText: 'Age'),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter an age';
                      }
                      if (!int.tryParse(value)!.isBetween(18, 99)) {
                        return 'Age must be between 18 and 99';
                      }
                      return null;
                    },
                  ),
                  TextFormField(
                    controller: _firstNameController,
                    decoration: const InputDecoration(labelText: 'First Name'),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter a first name';
                      }
                      if (value.length < 2) {
                        return 'First name must be at least 2 characters';
                      }
                      return null;
                    },
                  ),
                  TextFormField(
                    controller: _lastNameController,
                    decoration: const InputDecoration(labelText: 'Last Name'),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter a last name';
                      }
                      if (value.length < 2 &&
                          profileManager.checkInputLength(value)) {
                        return 'Last name must be at least 2 characters';
                      }
                      return null;
                    },
                  ),
                  TextFormField(
                    controller: _foodRestictionController,
                    decoration:
                        const InputDecoration(labelText: 'Food Restriction'),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter a last name';
                      }
                      if (value.length < 2) {
                        return 'Last name must be at least 2 characters';
                      }
                      return null;
                    },
                  ),
                  TextFormField(
                    controller: _bioController,
                    decoration: const InputDecoration(labelText: 'Bio'),
                    maxLines: 3,

                    // Add a validator for the bio field
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter a bio';
                      }
                      if (value.length < 10) {
                        return 'Bio must be at least 10 characters';
                      }
                      return null;
                    },
                  ),
                ],
              ),
            ),
          ),
          actions: [
            ElevatedButton(
              onPressed: () {
                Navigator.of(context).pop();
              },
              child: const Text('Cancel'),
            ),
            ElevatedButton(
              onPressed: () async {
                try {
                  if (_formKey.currentState?.validate() ?? false) {
                    print("Validation successful");

                    UserModel user = UserModel(
                      age: _ageController.text.trim(),
                      username: _usernameController.text.trim(),
                      firstName: _firstNameController.text.trim(),
                      lastName: _lastNameController.text.trim(),
                      foodRestriction: _foodRestictionController.text.trim(),
                      bio: _bioController.text.trim(),
                    );

                    // Save the user details
                    await profileManager.storeUserDetails(user);

                    // Automatically load updated user details
                    _loadUserDetails();

                    _ageController.clear();
                    _usernameController.clear();
                    _lastNameController.clear();
                    _firstNameController.clear();
                    _foodRestictionController.clear();
                    _bioController.clear();

                    Navigator.of(context).pop();
                  } else {
                    print("Validation failed");
                  }
                } catch (e) {
                  print("Error: $e");
                }
              },
              child: const Text('Save'),
            ),
          ],
        );
      },
    );
  }
  }

- Controllers (The controllers are used to store the information that the user inputs into the input fields)

- Validators (The validators are used to validate the information that the user inputs into the input fields)

- Actions (The actions are the buttons that allow the user to cancel the operation or save the information that they have inputted)

Profile Manager
---------------

The profile manager is a class that is used to manage the user profile page. The profile manager is responsible for storing the user's personal information and loading the user's personal information. The profile manager is also responsible for deleting the user's personal information.

.. code-block:: dart

    class ProfileManager {
    late UserManager userManager;
    late FirebaseAuth? auth = FirebaseAuth.instance;
    late FirebaseFirestore firestore = FirebaseFirestore.instance;

    ProfileManager({FirebaseAuth? auth, FirebaseFirestore? firestore}) {
        this.auth = auth ?? FirebaseAuth.instance;
        this.firestore = firestore ?? FirebaseFirestore.instance;
        userManager = UserManager(auth: this.auth!, firestore: this.firestore);
    }    

**Initial Values**

When first entering the user profile page, by default it will dispalay N/A for all the fields. This is because the user has not inputted any information yet.

.. code-block:: dart

    // Set all fields to "N/A"
      Map<String, dynamic> newData = {
        'age': 'N/A',
        'username': 'N/A',
        'firstName': 'N/A',
        'lastName': 'N/A',
        'foodRestriction': 'N/A',
        'bio': 'N/A'
      };


**getUserDeatails Function**

This function is used to retrieve the user's personal information from the database. The function first gets the user's UID and then retrieves the user's personal information from the database using the UID.

.. code-block:: dart

    Future<Map<String, dynamic>?> getUserDetails() async {
    try {
      String? uid = await userManager.getCurrentUserUID();
      DocumentSnapshot<Map<String, dynamic>> documentSnapshot =
          await firestore.collection("UserDetails").doc(uid).get();

      if (documentSnapshot.exists) {
        return documentSnapshot.data();
      } else {
        print('Document does not exist');
      }
    } catch (e) {
      print("Error retrieving user details: $e");
    }
    return null;
  }

**storeUserDetails Function**

This function is used to store the user's personal information in the database. The function first gets the user's UID and then stores the user's personal information in the database using the UID.

.. code-block:: dart

    Future<void> storeUserDetails(UserModel user) async {
    try {
      String? uid = await userManager.getCurrentUserUID();
      await firestore.collection("UserDetails").doc(uid).set(user.toJson());
      print('User details stored successfully');
    } catch (e) {
      print("Error storing user details: $e");
    }
  }

**deleteUserDetails Function**

This function is used to delete the user's personal information from the database. The function first gets the user's UID and then deletes the user's personal information from the database using the UID. The function also updates the local user information (e.g., clear currentUser). 

.. code-block:: dart

    Future<void> deleteUserDetails() async {
    try {
      String? uid = await userManager.getCurrentUserUID();

      // Reference to the user document in the "UserDetails" collection
      DocumentReference userRef =
          FirebaseFirestore.instance.collection('UserDetails').doc(uid);

      // Set all fields to "N/A"
      Map<String, dynamic> newData = {
        'age': 'N/A',
        'username': 'N/A',
        'firstName': 'N/A',
        'lastName': 'N/A',
        'foodRestriction': 'N/A',
        'bio': 'N/A'
      };

      // Update the user document with the new values
      await userRef.set(newData);

      // Optionally, you might want to update the local user information (e.g., clear currentUser)
      // currentUser = null;
      print('Deleted info');
    } catch (e) {
      print("Error deleting user details: $e");
    }
  }
 }


