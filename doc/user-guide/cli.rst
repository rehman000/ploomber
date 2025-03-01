Command line interface
======================

.. note::  This is an introductory tutorial to the command line interface, for a full API description, see: :doc:`../api/cli`.

Entry points
------------

By default, the CLi looks for an ``pipeline.yaml`` file in certain standard
locations (:ref:`api-cli-default-locations`). If your pipeline exists in a
non-standard location, pass the ``--entry-point`` argument.

The ``pipeline.yaml`` file is known as "entry point". However, this is
not the only type of entry point (See this guide to learn
more: :doc:`../user-guide/spec-vs-python`).

Basic commands
--------------

Build pipeline (skips up-to-date tasks):

.. code-block:: console

    ploomber build


Forced build (runs all tasks, regardless of status):

.. code-block:: console

    ploomber build --force


Generate pipeline plot:

.. code-block:: console

    ploomber plot


.. _user-guide-cli-interactive-sessions:

Interactive sessions
--------------------

Interactive sessions are a great way to develop your pipeline. Everything you
can do with the commands above (and more), you can do it with an interactive
session.

To start an interactive session:

.. code-block:: console

    ploomber interact

The command above starts a Python session, parses your pipeline, and exposes
a ``dag`` variable (an instance of the :py:mod:`ploomber.DAG` class).

For example, to generate the plot:

.. code-block:: python
    :class: ipython

    dag.plot()

Get task names:

.. code-block:: python
    :class: ipython

    list(dag)

You can also interact with specific tasks:

.. code-block:: python
    :class: ipython

    task = dag['task_name']

**Tip:** If using IPython or Jupyter, press ``Tab`` to get autocompletion when
typing the task name: ``dag['some_task']``

Get task's product:

.. code-block:: python
    :class: ipython

    dag['some_task'].product

If the product is a dictionary:

.. code-block:: python
    :class: ipython

    dag['some_task'].product['product_name']

You can use this to avoid hardcoding paths to load products:


.. code-block:: python
    :class: text-editor

    import pandas as pd

    df = pd.read_csv(dag['some_task'].product)


If you are working with Python tasks (functions, scripts, or notebooks), you can
start a line by line debugging session:

.. code-block:: python
    :class: ipython

    dag['some_task'].debug()

Enter ``quit`` to exit the debugging session. Refer to
`The Python Debugger <https://docs.python.org/3/library/pdb.html>`_
documentation for details.

To print the source code of a given task:

.. code-block:: python
    :class: ipython

    dag['some_task'].source

To find the source code location of a given task:

.. code-block:: python
    :class: ipython

    dag['some_task'].source.loc


Get upstream dependencies:

.. code-block:: python
    :class: ipython

    dag['some_task'].upstream

Get downstream tasks:

.. code-block:: python
    :class: ipython

    dag.get_downstream('some_task')

Other commands
--------------

Here's a list of commands that this introductory guide didn't cover:

* ``examples``: Locally copy Ploomber examples from (link to repo)
* ``report``: Generate a pipeline report
* ``scaffold``: Create base project layout
* ``status``: Pipeline status summary
* ``task``: Execute a single task

To learn more, see the CLI API documentation: :doc:`../api/cli`.