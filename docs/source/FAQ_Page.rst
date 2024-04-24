FAQ Page
=========

Introduction
------------

This is a FAQ page that allows users to ask questions and get answers. The questions and answers are stored locally in application. The user can add a question and answer, edit a question and answer. The user can also search for a question by typing in the search bar above all preset questions and answers. And press the seach button to send the query. 

QAItem
------

The QAItem class is a model class that represents a question and answer. It has two properties: question and answer. The QAItem class also has a convenience initializer that takes in a question and answer and sets the properties.

.. code-block:: dart

    class QAItem extends StatelessWidget {
  final String title;
  final List<Widget> children;
  final Color backgroundColor;
  final Color titleColor;
  final Color childrenColor;

  const QAItem({
    super.key,
    required this.title,
    required this.children,
    this.backgroundColor = Colors.green,
    this.titleColor = Colors.black,
    this.childrenColor = Colors.white,
  });


searchBar
---------

.. note::

    The search functionality is implemented, but the functionally to search is not implemented. The search bar is a text field that allows the user to type in a question and press the search button to search for the question. The search bar is a stateful widget that has a text controller that allows the user to type in a question. The search bar also has a search button that allows the user to press the search button to search for the question.


Buttons
-------

- Each of the preset questions and answer blocks has a gesture detector that reveals the answer when the user taps on the question.

