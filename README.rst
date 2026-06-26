Ansible Role: AzerothCore Docker
================================

Deploys an `AzerothCore <https://www.azerothcore.org/>`_ Docker environment
using the official ``acore-docker`` project. The role automates cloning the
required repositories, building custom server images, deploying the Docker
Compose stack, and optionally integrating the Individual Progression module.

Features
--------

* Clone the official ``acore-docker`` repository.
* Build a custom AzerothCore server from source.
* Build and optionally push images to a local Docker registry.
* Deploy the complete Docker Compose project.
* Mount custom modules and configuration.
* Support the Individual Progression module.
* Override both the builder and Docker Compose configuration without modifying
  upstream repositories.

Requirements
------------

The target host should have:

* Docker
* Docker Compose
* Git
* Sufficient disk space for building AzerothCore images

Role Variables
--------------

General
^^^^^^^

=============================== ================================================
Variable                        Description
=============================== ================================================
``azerothcore_docker_project_path``  Docker Compose project directory.
``azerothcore_docker_modules_path``  Directory containing AzerothCore modules.
``azerothcore_docker_config_path``   Server configuration directory.
``azerothcore_docker_assets_path``   Client data directory.
=============================== ================================================

Repositories
^^^^^^^^^^^^

================================================= ===================================
Variable                                          Description
================================================= ===================================
``azerothcore_docker_repository``                 acore-docker repository.
``azerothcore_docker_repository_version``         Version of acore-docker reposiotry.
``azerothcore_docker_builder_repository``         AzerothCore source repository.
``azerothcore_docker_builder_version``            Version of builder reposiotry.
================================================= ===================================

Individual Progression
^^^^^^^^^^^^^^^^^^^^^^

================================================== ==============================
Variable                                           Description
================================================== ==============================
``azerothcore_docker_progression_enabled``         Enable progression support.
``azerothcore_docker_progression_repository``      Progression module repository.
``azerothcore_docker_progression_version``         Module revision.
``azerothcore_docker_progression_phase``           Progression phase to configure.
================================================== ==============================

Docker Registry
^^^^^^^^^^^^^^^

================================================== ============================
Variable                                           Description
================================================== ============================
``azerothcore_docker_registry_enabled``            Enable the local registry.
``azerothcore_docker_registry_port``               Registry port.
``azerothcore_docker_registry_address``            Registry address.
``azerothcore_docker_push_images``                 Push images after building.
``azerothcore_docker_image_tag``                   Image tag applied to builds.
================================================== ============================

Database
^^^^^^^^

=============================== ===========================================
Variable                        Description
=============================== ===========================================
``azerothcore_docker_db_pwd``   MariaDB root password (**required**).
=============================== ===========================================

Compose Overrides
^^^^^^^^^^^^^^^^^

``azerothcore_docker_compose_overrides`` allows callers to customise the
generated Docker Compose configuration. This can be used to:

* Mount additional modules.
* Replace Docker images.
* Override health checks.
* Expose additional ports.
* Add custom volumes.

``azerothcore_docker_builder_overrides`` similarly allows customisation of the
generated builder configuration before images are built.

Dependencies
------------

This role has no required Ansible Galaxy dependencies.

Example Playbook
----------------

.. code-block:: yaml

   - hosts: game_servers
     become: true

     vars:
       azerothcore_docker_db_pwd: "{{ vault_azerothcore_db_password }}"

     roles:
       - role: azerothcore_docker

Example Configuration
---------------------

.. code-block:: yaml

   azerothcore_docker_progression_enabled: true
   azerothcore_docker_progression_phase: 7

   azerothcore_docker_registry_enabled: true

   azerothcore_docker_db_pwd: <password>

License
-------

GPL v3.0

Notes
-----

AI (specifically ChatGPT) was used to generate this README as I struggle with
writing documentation.