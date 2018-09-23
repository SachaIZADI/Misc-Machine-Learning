How to deploy a scikit-learn model in a django app
====================================

© (Michel Sassano)[https://github.com/SassanoM]


#1 Coding guidelines
--------------------

If you have to create custom classes or functions for your machine learning model/tasks.

**Don't declare your class or functions in the same file as your notebook.**

If you declare class or function in the notebook where you serialise your model you will have the following error:

.. code:: bash

    AttributeError: module '__main__' has no attribute 'ItemSelector'

For example, if you want to declare a class named "ItemSelector".

Create a file **transformation.py** and declare your class in this file. Then in your notebook **from transformation import ItemSelector**

You have to do this because otherwise when you'll pickle/unpickle your ML model you'll have an error.

If you declare your class / functions inside the notebook file the serializer will search for them inside the __main__ context and won't be
able to find them.

By importing them from another module you'll be able to port your model to another platform/context.

* Every custom/homemade function or class has to be declared in a separate module or package


How to import your ML model to the django app
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To import your ML model to the platform:

- create a folder "yourfolder" under the machine_learning folder (my_project/my_app/machine_learning/)
- copy the model "yourmodel.pk" file
- copy the "yourcustomthings.py" file where you have your custom class function
- add your package to the python/django PATH by adding the following lines to the my_project/my_app/apps.py file

.. code:: bash

    # Adding "yourfolder" to the path so joblib can unpickle the ML model correctly (dependency to yourcustomthings.py)
    sys.path.insert(0, "my_project/my_app/myfolder")
