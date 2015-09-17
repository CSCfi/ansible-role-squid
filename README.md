ansible-role-squid
=========

Installs and configures a Squid proxy for RHEL7 based OS.

Requirements
------------

get this error?
<pre>
{"failed": true}
msg: Destination /etc/squid not writable
</pre>

Set "sudo: yes" on the host

Role Variables
--------------

internal_net: "10.0.0.0/8"


Dependencies
------------


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: ansible-role-squid }

License
-------

MIT

Author Information
------------------
