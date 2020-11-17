postgresql_tuning
=========

Role will tune postgresql server according to information about hardware.\
Followin OS parameters will be updated:
* vm.swappiness
* vm.overcommit_memory

Followin postgresql parameters will be updated:
* postgresql_work_mem
* max_connections
* maintenance_work_mem
* shared_buffers
* effective_cache_size
* random_page_cost


Requirements
------------

Postgresql server must be installed and running.

Role Variables
--------------

For ssd drives 1 should be replaced with higher number (e.g. 2,3 or even 10 depending on disk speed)\
Default value is:\
`postgresql_drive_effective_spindle_count: 1`

On small instances with 4 CPU or less it is recommended to have at least 10 connections\
default is:\
`postgresql_min_connections: 10`

should be 1.1 for ssd, 4 for hdd and 5 for very slow virtual or network drives\
default is:\
`postgresql_random_page_cost: 4`

Name of the postgresql service (on RHEL familiy is is postgresql but if you install from postgresql repo it is postgesql-number)\
default is:\
`postgresql_service_name: postgresql`

Setting overcommit to 2 prevents postgresql crashing from out of memory error\
Allowed values are:\
0 - heuristic overcommit\
1 - always overcommit, never check\
2 -  always check, never overcommit\
default value is:\
`vm_overcommit_memory: 2` 

Sets swappiness to minimal level but does not disable it (to disable set to 0)\
default value is:\
`vm_swappiness: 1`

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: yilativs.postgresql_tune, postgresql_random_page_cost: 1 }

License
-------

GPLv2

Author Information
------------------

Vitaliy Semochking yilativs@gmail.com
