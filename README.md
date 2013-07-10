Signed Shell
------------

This is a minialmist attempt at adding security arround shell scripts. It relies
on checking GPG signatures applied to script files.

It currently has been tested w/ bash, python, and perl.

This was primarily inspired by a description a tool in use at Yahoo!, from a
issue of Login;. I can no longer find the issue, and so wrote this as a
quick and dirty subsitute.


Performance
===========
This implementation in not intended to be ultra performant. I've not done any
bench marking, but it shoud add significant overhead to execution.

Bash
====
I've done a lot to make this very bash friendly. Support for source is there,
but buy its nature is insecure. I've added a tool to verify the injected bash
code, but its up to the user to force verification of code before sourcing the
file

Purpose
-------

The idea here is to limit privileged access to the "signed" program. Which
would make some minimal guarentees that the users script has been approved by
a trusted party.

Requirements
------------
This requires that you have a gpg.

Limitations
-----------

This is does not have support for a more advanced feature like includes. Modules
and other such files are not verified, and if signed will not load properly. I
will try to address this type of functionality later, but it is likely language
specific.

The "signed" shell itself is vulnerable to modifications, and system level
check should be put in place to manage security.

Usage
-----

sign_script
-----------
Signing a script is as easy as running:
`sign_script filename`

This will sign the script with your default GPG key, and create a new file
called `filename.signed`.

Running a Singed Script
-----------------------
Scripts will execute when run like so:
  ./script.signed
or:
  signed filename


verify_bash_header
------------------
In order to handle source execution from bash scripts, unsigned bash is
injected into the area above the clear-signature. verify_bash_header
should securely check this, provided you run a signed version with the
correct md5sum. It returns 0 if it matches and 1 if it does not.

Usage would be as follows:
  verify_bash_header <filename>
  if [ $? -ne 0 ] ; then
    exit 1
  fi
  source <filename>

This script should be signed with your own key in order to make it secure. You can sign it like so:
  # sign_script verify_bash_header
