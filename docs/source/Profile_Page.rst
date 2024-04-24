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



