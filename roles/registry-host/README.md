Registry
=========
This role install and configure the docker-distribution. docker-distribution is only availinle on centos 7. So before trying to install the packages we first check if the versions of the os is a centos 7.  We then install the required packages. You're not forced to create a self signed certificate to have access to your registry. Adding this to the docker daemon { "insecure-registries" : ["myregistrydomain.com:5000"]} let . here we'll create the self-signed certificate be carreful that the common name match exactly the name of the hosts machines.


Requirements
------------
py-brcipt is the only supported encription for http auth. py-bcrypt is an password hashing algorithm.


Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

source
------------------

https://www.centlinux.com/2019/04/configure-secure-registry-docker-distribution-centos-7.html

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
