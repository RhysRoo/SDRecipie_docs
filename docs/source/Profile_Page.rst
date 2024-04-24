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
                        ),

- Change Information (The change information button allows the user to change/add their personal information on the page)


