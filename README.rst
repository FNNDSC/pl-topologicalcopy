pl-topologicalcopy
================================

.. image:: https://img.shields.io/docker/v/fnndsc/pl-topologicalcopy
    :target: https://hub.docker.com/r/fnndsc/pl-topologicalcopy

.. image:: https://img.shields.io/github/license/fnndsc/pl-topologicalcopy
    :target: https://github.com/FNNDSC/pl-topologicalcopy/blob/master/LICENSE

.. image:: https://github.com/FNNDSC/pl-topologicalcopy/workflows/ci/badge.svg
    :target: https://github.com/FNNDSC/pl-topologicalcopy/actions


.. contents:: Table of Contents


Abstract
--------

A plugin ts app to copy filtered output directories from many input plugin instances.


Description
-----------

``topologicalcopy`` is a ChRIS-based application to copy filtered output directories from a
list of input plugin instances.


Usage
-----

.. code::

    python topologicalcopy.py
            [-h] [--help]
            [--json]
            [--man]
            [--meta]
            [--savejson <DIR>]
            [-v <level>] [--verbosity <level>]
            [--version]
            <outputDir>
            [--plugininstances <instances>]
            [-f <filter>] [--filter <filter>]
            [-g] [--groupByInstance]


Arguments
~~~~~~~~~

.. code::

        [-h] [--help]
        If specified, show help message and exit.

        [--json]
        If specified, show json representation of app and exit.

        [--man]
        If specified, print (this) man page and exit.

        [--meta]
        If specified, print plugin meta data and exit.

        [--savejson <DIR>]
        If specified, save json representation file to DIR and exit.

        [-v <level>] [--verbosity <level>]
        Verbosity level for app. Not used currently.

        [--version]
        If specified, print version number and exit.

        [--plugininstances <instances>]
        If specified, it's a string representing a comma-separated list of plugin
        instance ids.

        [-f <filter>] [--filter <filter>]
        If specified, it's a string representing a comma-separated list of regular
        expressions.

        [-g] [--groupByInstance]
        If specified then an output directory is created for each input plugin instance
        within this plugin app's output path


Getting inline help is:

.. code:: bash

    docker run --rm fnndsc/pl-topologicalcopy topologicalcopy --man

Run
~~~

You need you need to specify the output directory using the `-v` flag to `docker run`.


.. code:: bash

    docker run --rm -u $(id -u) -v $(pwd)/out:/outgoing      \
        fnndsc/pl-topologicalcopy topologicalcopy /outgoing


Development
-----------

Build the Docker container:

.. code:: bash

    docker build -t local/pl-topologicalcopy .

Run unit tests:

.. code:: bash

    docker run --rm local/pl-topologicalcopy nosetests

Examples
--------

This example will copy all files in the output directories of plugin instances with id 1,3
and 7 that have `.dcm` extension. Note: This is a utility 'ts' plugin that only works in
the context of the ChRIS platform.

.. code:: bash

    docker run --rm -v $(pwd)/out:/outgoing fnndsc/pl-topologicalcopy    \
    topologicalcopy /outgoing --plugininstances "1,3,7" --filter "\.dcm$,\.dcm$,\.dcm$"


.. image:: https://raw.githubusercontent.com/FNNDSC/cookiecutter-chrisapp/master/doc/assets/badge/light.png
    :target: https://chrisstore.co
