API Reference
=============
This document is the API reference of Remofile. All classes, functions
and exceptions are accessible from a single import of the **remofile**
package.

.. code-block:: python

    from remofile import *

The programming interface is essentially made of two classes which are
:ref:`Client<client-class-ref>` and :ref:`Server<server-class-ref>`.
They implement both side of the :doc:`Remofile protocol </protocol-specifications>`.

Interface overview
------------------
The client class implements all primitive file operations and therefore
any more complex file operations can, in theory, be implemented on top
of it.

List of primitive file operations.

* List files
* Create a file
* Create a directory
* Upload a file
* Upload a directory
* Download a file
* Download a directory
* Delete a file (or directory)

However, the algorithm module already implements a couple of
useful more :ref:`advanced file operations <advanced-algorithms-ref>`
for you. For instance, it can upload and download trees of files,
understand glob patterns and handle conflicts. It also has functions to
synchronize directories from client to server and server to client.

Dealing with errors is an important aspect in a code that involves file
operations. A :ref:`set of exceptions<handling-exceptions-ref>` are
defined and they all have the :py:exc:`RemofileException` exception as
base class. Therefore, you can catch most of Remofile-related exceptions in
one statement.

.. code-block:: python

    try:
        do_file_operation()
    except RemofileException:
        deal_with_exception()

Additionally, some :ref:`helper functions<helper-functions-ref>` like
:py:func:`generate_token`, :py:func:`generate_keys` and
:py:func:`is_file_name_valid` are also exposed.

Two main classes
----------------

.. py:currentmodule:: remofile

.. _client-class-ref:

.. autoclass:: Client

    .. automethod:: __init__

    .. automethod:: list_files
    .. automethod:: create_file
    .. automethod:: make_directory
    .. automethod:: upload_file
    .. automethod:: upload_directory
    .. automethod:: download_file
    .. automethod:: download_directory
    .. automethod:: delete_file

.. _server-class-ref:

.. autoclass:: Server

    .. automethod:: __init__

    .. autoattribute:: root_directory
    .. autoattribute:: file_size_limit
    .. autoattribute:: chunk_size_range

    .. automethod:: run
    .. automethod:: terminate

.. _advanced-algorithms-ref:

Advanced algorithms
-------------------
A bunch of advanced algorithms are implemented on top of the primitive file
operations because in practice, we need more than that.

You will particularly want to have a look at :py:func:`upload_files` and
:py:func:`download_files` as they provide a more sophisticated interface to
fine-grain control what is to be uploaded or downloaded. And you may also need
synchronization features in both directions which is done with
:py:func:`synchronize_upload` and :py:func:`synchronize_download`.

.. autofunction:: upload_files
.. autofunction:: download_files
.. autofunction:: synchronize_upload
.. autofunction:: synchronize_download

.. _handling-exceptions-ref:

Handling exceptions
-------------------
This section isn't written yet.

.. autoexception:: RemofileException

.. autoexception:: SourceNotFound
.. autoexception:: DestinationNotFound

.. autoexception:: UnexpectedError
.. autoexception:: BadRequestError
.. autoexception:: UnknownError
.. autoexception:: CorruptedResponse

.. autoexception:: FileNameError

.. _helper-functions-ref:

Helper functions
----------------
These helper functions will come in handy to generate a random valid token and
generate a pair of private and public key to configure the server with. There
is also a function to check validity of a filename as defined by the Remofile
protocol.

.. autofunction:: generate_token
.. autofunction:: generate_keys
.. autofunction:: is_file_name_valid
