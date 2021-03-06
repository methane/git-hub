Using github from the CLI
=========================

:command:`git hub` lets you use your github account from the command line.
Among other things, it lets you create and fork repositories, or file pull
requests.

Install info
------------
To install the latest released version::

    pip install hub

To install the latest development version::

    pip install http://seveas.net/git-hub

Basic usage
-----------
The first time you use :command:`git hub`, it will ask you for your github
username and password. It then requests (and stores) an API authentication
token, so you can always revoke access from your `profile page`_.

The authentication token is stored in :file:`~/.githubconfig`. Never share this
token with anyone as it gives full access to your github account.

.. describe:: git hub whoami

A simple command to try out is :command:`git hub whoami`, which tells you what
github thinks about who you are. For example::

  dennis@lightning:~$ git hub whoami
  Github user: seveas
  GitHub password:
  [1;4mDennis Kaarsemaker[0m
  Profile   https://github.com/seveas
  Email     dennis@kaarsemaker.net
  Blog      http://www.kaarsemaker.net
  Location  Amsterdam
  Company   Booking.com
  Repos     36 public, 0 private
  Gists     4 public, 0 private
  RSA key   ...N0nFw3oW5l (Dennis)

.. describe:: git hub whois

If you want to see this information about other users, use :command:`git hub whois`::

  dennis@lightning:~$ git hub whois sigmavirus24
  [1;4mIan Cordasco[0m
  Profile   https://github.com/sigmavirus24
  Email     graffatcolmingov@gmail.com
  Blog      http://www.coglib.com/~icordasc/blog
  Repos     21 public, 0 private
  Gists     9 public, 0 private

.. describe:: git hub repos [<user>...]

List all repositories owned by a user, by default you.

.. describe:: git hub add-public-keys [<key>...]

Add SSH public keys (default: :file:`~/.ssh/*.pub`) to your account.

.. describe:: git hub public-keys <user>

Display all public keys of a user, in a format that can be added to
:file:`~/.authorized_keys`.

.. _`profile page`: https://github.com/settings/applications

Interacting with repositories
-----------------------------

.. describe:: git hub create [-d <description>]

Create a repository on github for your current repository. An optional
description can be given too. After running this command, a repository will be
created on github and your local repository will have github as remote
"origin", so :command:`git push origin master` will work.

.. describe:: git hub set-origin

Fix the configuration of your repository's remotes. Remote "origin" will be set
to your github repository. If that repository is a fork, remote "upstram" will
be set to the repository you forked from.

.. describe:: git hub clone <repo>

Clone a github repository by name (e.g. seveas/hacks) or URL. If it's a fork,
the "upstream" origin will be set up too.

.. describe:: git hub fork <repo>

Fork another person's git repository on github and clones that repository
locally. Repo can be specified as a (git) url or simply username/repo. Like
with set-origin, the "origin" and "upstream" remotes will be set up too.

.. describe:: git hub forks

List all forks of this repository, highlighting the original repository.

.. describe:: git hub add-remote [<user>]

Add a users fork as a remote using the user's login as name for the remote.

.. describe:: git hub browse

Browse the repository on GitHub

.. describe:: git hub mirror [<repo>]

Mirror a repository from github. This is similar to clone, but clones into a
bare repository and maps all remote refs to local refs. When run without
argument, the current repository will be updated.

.. describe:: git hub hooks

Show all service hooks for this repository.

.. describe:: git hub add-hook <name> [<setting>...]

Add a hook to this repository with the appropriate settings. Settings can be
found in the hooks page on github. One setting all hooks accept is
:data:`events`, a comma-separated list of events this hook will be triggered
for. A list of all events can be found on the `GitHub API page`_

.. describe:: git hub edit-hook <name> [<setting>...]

Edit one or more settings for a hook.

.. describe:: git-hub remove-hook <name>

Remove a service hook.

.. _`GitHub API page`: http://developer.github.com/v3/repos/hooks/

Issues and pull requests
------------------------

.. describe:: git hub issues [--parent] [<filter>...]

List all open issues. You can specify `filters`_ to filter issues. When you
specify :option:`--parent`, list all open issues for the parent repository.

.. describe:: git hub issue [--parent] <issue>...

Shows details about the mentioned issue numbers. As with :option:`issues`, you
can use the :option:`--parent` option to use the parent repository.

.. describe:: git hub pull-request [--issue <issue>] <yours:theirs>

Files a pull request to merge branch "yours" (default: the current branch) into
the upstream branch "theirs" (default: master). Like for a commit message, your
editor will be opened to write a pull request message. The comments of said
message contain the shortlog and diffstat of the commits that you're asking to
be merged. Note that if you use any characterset in your logs and filenames
that is not ascii or utf-8, git hub will misbehave.

If you specify an issue number, that issue will be turned into a pull request
and you will not be asked to write a pull request message.

.. _`filters`: http://github3py.readthedocs.org/en/latest/repos.html#github3.repos.Repository.list_issues

Gists
-----

.. describe:: git hub gist [-d <description>] <file>...

Creates a gist (with optional description) from the named files. If you specify
:file:`-` as filename, :file:`stdin` will be used, making it easy to pipe
command output to github, for example: :command:`fortune | git hub gist -`

.. describe:: git hub gists [<user>]

List your gists, or those created by another user.

Other
-----
.. describe:: git hub ignore [<lang>...]

Github provides :file:`.gitignore` templates for various languages and
environments. This command will let you quickly grab them and add them to your
:file:`.gitignore`. For example: :command:`git hub ignore Python C`

.. describe:: git hub network

Generates a graphviz graph of people following you, people you follow or people
who's repositories you've forked. For example::

  git hub network | dot -T png -Grankdir=LR > network.png

Here's mine:

.. image:: _static/network.png
