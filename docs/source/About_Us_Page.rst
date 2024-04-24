About_Us_Page
=============

Page Overview
-------------

The about us page is a page that tells the user about the scope of our mission with the app and the team behind it. It is a scrollable page with a header, a paragraph of text, and a team section with a picture of each team member and a short bio and a way to communicate with any member of the team through email.

Launch Email Functionality
---------------------

To launch the email function, the user must click on the contact by email link on the team member's card. This will launch the email app on the user's device with the email address of the team member already filled in. The user can then write an email to the team member and send it.

.. code-block:: dart

    // Method to launch email app
  void _launchEmail() async {
    final Uri emailLaunchUri = Uri(
      scheme: 'mailto',
      path: 'up2120303@myport.ac.uk',
    );
    if (await canLaunch(emailLaunchUri.toString())) {
      await launch(emailLaunchUri.toString());
    } else {
      print('Could not launch email');
    }
  }
    
Scroll Functionality
--------------------

.. code-block:: dart

    body: SingleChildScrollView()

Any content that is placed inside the SingleChildScrollView widget will be scrollable. This is because the SingleChildScrollView widget allows the user to scroll through the content that is placed inside it. This is useful for the about us page as it allows the user to scroll through the team section to see all the team members.