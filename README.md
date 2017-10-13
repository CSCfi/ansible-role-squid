[![Build Status](https://travis-ci.org/CSCfi/ansible-role-squid.svg)](https://travis-ci.org/CSCfi/ansible-role-squid)
ansible-role-squid
=========

Installs and configures a Squid proxy.

Requirements
------------

get this error?
<pre>
{"failed": true}
msg: Destination /etc/squid not writable
</pre>

Set "become: yes" on the host

Role Variables
--------------

See defaults/main.yml

<pre>
internal_net: "10.0.0.0/8"
squid_extra_settings:
  - "setting1"
  - "setting2"
</pre>

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
