Building locally
----------------

#.  Enter a new Alpine Linux ``chroot``, with Ansible installed and acquire
    ``root``
#.  Clone this repository to ``/builds/keith.maxwell/aports-local`` and move
    there

    ..
      mkdir /builds /builds/keith.maxwell /builds/keith.maxwell/aports-local &&
      cd /builds/keith.maxwell/aports-local &&
      git clone https://gitlab.com/keith.maxwell/aports-local .

#.  Add the private key as ``keith.maxwell@gmail.com-5a1151a5.rsa``
#.  Install build tools and add user with::

        ansible-playbook -i localhost, ./site.yaml

#.  Change the owner to ``abuild:abuild`` and match the ID of the `abuild` user
    inside this ``chroot`` to the user configured for commits:

    ..
      chown -R abuild:abuild /builds/keith.maxwell/aports-local
      vim /etc/passwd

#.  Build with ``su abuild -c 'buildrepo local'``

Manual steps
------------

First move to the directory containing the `APKBUILD`, then the steps using
``su abuild -c 'abuild <step>'`` are::

    1   checksum
    2   deps
    3   unpack
    4   prepare
    5   build
    6   check
    7   package
    8   undeps

Running ``abuild -r`` will create the ``.apk`` packages.

Main repository
---------------

To get a copy of the main Alpine Linux repository use::

    git clone --depth 1 git://git.alpinelinux.org/aports

Resources
---------

A sample_ `APKBUILD` is available:

.. code:: sh

    curl -o APKBUILD \
        https://git.alpinelinux.org/cgit/abuild/plain/sample.APKBUILD

The `APKBUILD Reference`_ is a wiki page.

The default functions can be seen in abuild.in_.

.. _APKBUILD Reference: https://wiki.alpinelinux.org/wiki/APKBUILD_Reference
.. _abuild.in: https://github.com/alpinelinux/abuild/blob/master/abuild.in
.. _sample: https://git.alpinelinux.org/cgit/abuild/log/sample.APKBUILD

https://repology.org links for new versions:

..
    ls -1 aports/local | sed 's/.*/`\0 <>`__/'

-   `beancount <https://
    repology.org/metapackage/beancount/information>`
-   `dash <https://
    repology.org/metapackage/dash/information>`__
-   `jbig2enc <https://
    repology.org/metapackage/jbig2enc/information>`__
-   `py-enchant <https://
    https://repology.org/metapackage/pyenchant/versions>`__
-   `py-ply <https://
    repology.org/metapackage/python:ply/information>`__
-   `py3-ansible-lint <https://
    repology.org/metapackage/ansible-lint/information>`__
-   `sane-backend-canon_dr <https://
    repology.org/metapackage/sane-backends/information>`__
-   `sane-frontends <https://
    repology.org/metapackage/sane-frontends/information>`__
    which incorrectly shows that a more recent version number, matching
    ``sane-backends``, is available

..
    grep pkgver= aports/local/*/APKBUILD

.. vim: ft=rst
