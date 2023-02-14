:author: rules_proto_grpc
:description: rules_proto_grpc Bazel rules for grpc-gateway
:keywords: Bazel, Protobuf, gRPC, Protocol Buffers, Rules, Build, Starlark, grpc-gateway


grpc-gateway
============

.. list-table:: Rules
   :widths: 1 2
   :header-rows: 1

   * - Rule
     - Description
   * - `gateway_grpc_compile`_
     - Generates grpc-gateway ``.go`` files
   * - `gateway_openapiv2_compile`_
     - Generates grpc-gateway OpenAPI v2 ``.json`` files
   * - `gateway_grpc_library`_
     - Generates grpc-gateway library files

.. _gateway_grpc_compile:

gateway_grpc_compile
--------------------

Generates grpc-gateway ``.go`` files

Example
*******

Full example project can be found `here <https://github.com/rules-proto-grpc/rules_proto_grpc/tree/master/example/grpc-gateway/gateway_grpc_compile>`__

``WORKSPACE``
^^^^^^^^^^^^^

.. code-block:: python

   load("@rules_proto_grpc//:repositories.bzl", "bazel_gazelle", "io_bazel_rules_go")  # buildifier: disable=same-origin-load
   
   io_bazel_rules_go()
   
   load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
   
   go_rules_dependencies()
   
   go_register_toolchains(
       version = "1.15.8",
   )
   
   bazel_gazelle()
   
   load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
   
   gazelle_dependencies()
   
   load("@rules_proto_grpc//grpc-gateway:repositories.bzl", rules_proto_grpc_gateway_repos = "gateway_repos")
   
   rules_proto_grpc_gateway_repos()
   
   load("@com_github_grpc_ecosystem_grpc_gateway_v2//:repositories.bzl", "go_repositories")
   
   go_repositories()

``BUILD.bazel``
^^^^^^^^^^^^^^^

.. code-block:: python

   load("@rules_proto_grpc//grpc-gateway:defs.bzl", "gateway_grpc_compile")
   
   gateway_grpc_compile(
       name = "api_gateway_grpc",
       protos = ["@rules_proto_grpc//grpc-gateway/example/api:api_proto"],
   )

Attributes
**********

.. list-table:: Attributes for gateway_grpc_compile
   :widths: 1 1 1 1 4
   :header-rows: 1

   * - Name
     - Type
     - Mandatory
     - Default
     - Description
   * - ``protos``
     - ``label_list``
     - true
     - 
     - List of labels that provide the ``ProtoInfo`` provider (such as ``proto_library`` from ``rules_proto``)
   * - ``options``
     - ``string_list_dict``
     - false
     - ``[]``
     - Extra options to pass to plugins, as a dict of plugin label -> list of strings. The key * can be used exclusively to apply to all plugins
   * - ``verbose``
     - ``int``
     - false
     - ``0``
     - The verbosity level. Supported values and results are 1: *show command*, 2: *show command and sandbox after running protoc*, 3: *show command and sandbox before and after running protoc*, 4. *show env, command, expected outputs and sandbox before and after running protoc*
   * - ``prefix_path``
     - ``string``
     - false
     - ``""``
     - Path to prefix to the generated files in the output directory
   * - ``extra_protoc_args``
     - ``string_list``
     - false
     - ``[]``
     - A list of extra args to pass directly to protoc, not as plugin options

Plugins
*******

- ``@rules_proto_grpc//grpc-gateway:grpc_gateway_plugin``
- ``@rules_proto_grpc//go:grpc_go_plugin``
- ``@rules_proto_grpc//go:go_plugin``

.. _gateway_openapiv2_compile:

gateway_openapiv2_compile
-------------------------

Generates grpc-gateway OpenAPI v2 ``.json`` files

Example
*******

Full example project can be found `here <https://github.com/rules-proto-grpc/rules_proto_grpc/tree/master/example/grpc-gateway/gateway_openapiv2_compile>`__

``WORKSPACE``
^^^^^^^^^^^^^

.. code-block:: python

   load("@rules_proto_grpc//:repositories.bzl", "bazel_gazelle", "io_bazel_rules_go")  # buildifier: disable=same-origin-load
   
   io_bazel_rules_go()
   
   load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
   
   go_rules_dependencies()
   
   go_register_toolchains(
       version = "1.15.8",
   )
   
   bazel_gazelle()
   
   load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
   
   gazelle_dependencies()
   
   load("@rules_proto_grpc//grpc-gateway:repositories.bzl", rules_proto_grpc_gateway_repos = "gateway_repos")
   
   rules_proto_grpc_gateway_repos()
   
   load("@com_github_grpc_ecosystem_grpc_gateway_v2//:repositories.bzl", "go_repositories")
   
   go_repositories()

``BUILD.bazel``
^^^^^^^^^^^^^^^

.. code-block:: python

   load("@rules_proto_grpc//grpc-gateway:defs.bzl", "gateway_openapiv2_compile")
   
   gateway_openapiv2_compile(
       name = "api_gateway_grpc",
       protos = ["@rules_proto_grpc//grpc-gateway/example/api:api_proto"],
   )

Attributes
**********

.. list-table:: Attributes for gateway_openapiv2_compile
   :widths: 1 1 1 1 4
   :header-rows: 1

   * - Name
     - Type
     - Mandatory
     - Default
     - Description
   * - ``protos``
     - ``label_list``
     - true
     - 
     - List of labels that provide the ``ProtoInfo`` provider (such as ``proto_library`` from ``rules_proto``)
   * - ``options``
     - ``string_list_dict``
     - false
     - ``[]``
     - Extra options to pass to plugins, as a dict of plugin label -> list of strings. The key * can be used exclusively to apply to all plugins
   * - ``verbose``
     - ``int``
     - false
     - ``0``
     - The verbosity level. Supported values and results are 1: *show command*, 2: *show command and sandbox after running protoc*, 3: *show command and sandbox before and after running protoc*, 4. *show env, command, expected outputs and sandbox before and after running protoc*
   * - ``prefix_path``
     - ``string``
     - false
     - ``""``
     - Path to prefix to the generated files in the output directory
   * - ``extra_protoc_args``
     - ``string_list``
     - false
     - ``[]``
     - A list of extra args to pass directly to protoc, not as plugin options

Plugins
*******

- ``@rules_proto_grpc//grpc-gateway:openapiv2_plugin``

.. _gateway_grpc_library:

gateway_grpc_library
--------------------

Generates grpc-gateway library files

Example
*******

Full example project can be found `here <https://github.com/rules-proto-grpc/rules_proto_grpc/tree/master/example/grpc-gateway/gateway_grpc_library>`__

``WORKSPACE``
^^^^^^^^^^^^^

.. code-block:: python

   load("@rules_proto_grpc//:repositories.bzl", "bazel_gazelle", "io_bazel_rules_go")  # buildifier: disable=same-origin-load
   
   io_bazel_rules_go()
   
   load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
   
   go_rules_dependencies()
   
   go_register_toolchains(
       version = "1.15.8",
   )
   
   bazel_gazelle()
   
   load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
   
   gazelle_dependencies()
   
   load("@rules_proto_grpc//grpc-gateway:repositories.bzl", rules_proto_grpc_gateway_repos = "gateway_repos")
   
   rules_proto_grpc_gateway_repos()
   
   load("@com_github_grpc_ecosystem_grpc_gateway_v2//:repositories.bzl", "go_repositories")
   
   go_repositories()

``BUILD.bazel``
^^^^^^^^^^^^^^^

.. code-block:: python

   load("@rules_proto_grpc//grpc-gateway:defs.bzl", "gateway_grpc_library")
   
   gateway_grpc_library(
       name = "api_gateway_library",
       importpath = "github.com/rules-proto-grpc/rules_proto_grpc/grpc-gateway/examples/api",
       protos = ["@rules_proto_grpc//grpc-gateway/example/api:api_proto"],
   )

Attributes
**********

.. list-table:: Attributes for gateway_grpc_library
   :widths: 1 1 1 1 4
   :header-rows: 1

   * - Name
     - Type
     - Mandatory
     - Default
     - Description
   * - ``protos``
     - ``label_list``
     - true
     - 
     - List of labels that provide the ``ProtoInfo`` provider (such as ``proto_library`` from ``rules_proto``)
   * - ``options``
     - ``string_list_dict``
     - false
     - ``[]``
     - Extra options to pass to plugins, as a dict of plugin label -> list of strings. The key * can be used exclusively to apply to all plugins
   * - ``verbose``
     - ``int``
     - false
     - ``0``
     - The verbosity level. Supported values and results are 1: *show command*, 2: *show command and sandbox after running protoc*, 3: *show command and sandbox before and after running protoc*, 4. *show env, command, expected outputs and sandbox before and after running protoc*
   * - ``prefix_path``
     - ``string``
     - false
     - ``""``
     - Path to prefix to the generated files in the output directory
   * - ``extra_protoc_args``
     - ``string_list``
     - false
     - ``[]``
     - A list of extra args to pass directly to protoc, not as plugin options
   * - ``deps``
     - ``label_list``
     - false
     - ``[]``
     - List of labels to pass as deps attr to underlying lang_library rule
   * - ``importpath``
     - ``string``
     - false
     - ``None``
     - Importpath for the generated files
