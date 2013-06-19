Signed Shell
------------

This is a minialmist attempt at adding security arround shell scripts. It relies
on checking GPG signatures applied to script files.

It currently has been tested w/ bash, python, and perl.

This was primarily inspired by a description a tool in use at Yahoo!, from a
issue of Login;. I can no longer find the issue, and so wrote this as a
quick and dirty subsitute.

Purpose
-------

The idea here is to limit privileged access to the "signed" program. Which
would make some minimal guarentees that the users script has been approved by
a trusted party.

Limitations
-----------

This is does not have support for a more advanced feature like includes. Modules
and other such files are not verified, and if signed will not load properly. I
will try to address this type of functionality later, but it is likely language
specific.

The "signed" shell itself is vulnerable to modifications, and system level
check should be put in place to manage security.


