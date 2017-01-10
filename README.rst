===================
elastic-doc-manager
===================

.. image:: https://travis-ci.org/mongodb-labs/elastic-doc-manager.svg?branch=master
   :alt: View build status
   :target: https://travis-ci.org/mongodb-labs/elastic-doc-manager

**Note: This is the document manager for Elasticsearch 1.x. If you want to use
Elasticsearch >= 2.0, please install elastic2-doc-manager.**

Getting Started
===============

This package is a document manager for
`mongo-connector <https://github.com/mongodb-labs/mongo-connector>`_. that
targets Elasticsearch version 1.x.
For information on running mongo-connector with Elasticsearch, please see the
`MongoConnector Usage with Elasticsearch
<https://github.com/mongodb-labs/mongo-connector/wiki/Usage%20with%20ElasticSearch>`_
wiki page.

Installation
============

The installation of the elastic-doc-manager depends on which version of
Elasticsearch you are targeting.

Elasticsearch 1.x
-----------------

For use with an Elasticsearch 1.x server, install with
`pip <https://pypi.python.org/pypi/pip>`__::

  pip install 'elastic-doc-manager'

Amazon Elasticsearch 1.x Service
--------------------------------

To use with Amazon Elasticsearch Service, you must install the required AWS
dependencies along with the version of Elasticsearch::

  pip install 'elastic-doc-manager[aws]'

Elasticsearch >= 2.0
--------------------

This is the document manager for Elasticsearch 1.x only. If you
want to target 2.0 or greater, please install the
`elastic2-doc-manager <https://github.com/mongodb-labs/elastic2-doc-manager>`_.

Development
-----------

You can also install the development version of elastic-doc-manager
manually::

  git clone https://github.com/mongodb-labs/elastic-doc-manager.git
  pip install -e './elastic-doc-manager'

You may have to run ``pip`` with ``sudo``, depending on where you're
installing and what privileges you have.

**Note: Before mongo-connector version 2.2.2, the elastic doc manager was packaged with mongo-connector
and only supported Elasticsearch 1.x.**

Running the tests
-----------------
Requirements
~~~~~~~~~~~~

1. Copy of the Elastic 1.x Document Manager Github repository

  The tests are not included in the package from PyPI and can only be acquired by cloning this repository on Github::

      git clone https://github.com/mongodb-labs/elastic-doc-manager

2. Mongo Orchestration

  Mongo Connector runs MongoDB on its own using another tool called `Mongo Orchestration <https://github.com/mongodb/mongo-orchestration>`__. This package should install automatically if you run ``python setup.py test``, but the Mongo Orchestration server still needs to be started manually before running the tests::

      mongo-orchestration --bind 127.0.0.1 --config orchestration.config start

  will start the server. To stop it::

      mongo-orchestration --bind 127.0.0.1 --config orchestration.config stop

  The location of the MongoDB server should be set in orchestration.config. For more information on how to use Mongo Orchestration, or how to use it with different arguments, please look at the Mongo-Orchestration README.

3. Environment variables

  There are a few influential environment variables that affect the tests. These are:

    - ``DB_USER`` is the username to use if running the tests with authentication enabled.
    - ``DB_PASSWORD`` is the password for the above.
    - ``MONGO_PORT`` is the starting port for running MongoDB. Future nodes will be started on sequentially increasing ports.
    - ``ES_HOST`` is the hostname on which Elasticsearch is running.
    - ``ES_PORT`` is the port on which Elasticsearch is running.
    - ``MO_ADDRESS`` is the address to use for Mongo Orchestration (i.e. hostname:port)

All the tests live in the `tests` directory.

Running tests on the command-line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

While the tests take care of setting up and tearing down MongoDB clusters on their own, make sure to start Elastic before doing a full test run!

You can run all the tests with one command (this works in all supported Python versions)::

  python setup.py test

In addition, you can be more selective with which tests you run (in Python > 2.6 only)! For example, if you only wanted to run the elastic doc manager tests::

  python -m unittest tests.test_elastic_doc_manager

Error messages
~~~~~~~~~~~~~~

Some of the tests are meant to generate lots of ``ERROR``-level log messages, especially the rollback tests. mongo-connector logs exceptions it encounters while iterating the cursor in the oplog, so we see these in the console output while MongoDB clusters are being torn apart in the tests. As long as all the tests pass with an `OK` message, all is well.
