***************************************
The homestead documentation initiative
***************************************


Purpose and Audience
=============================

This guide should serve to be an entry level for all Ethereum users and developers.
The goal is to create a documentation with information, short tutorials, and examples that will cover all of the basic and intermediate functionality of using Ethereum to interact with dapps or develop a dapp.

Any information that is overly specific, technical, or not necessary to accomplish the documentation goal will remain on the Github Wiki. It may be referenced in this guide if necessary.

Although much of the information will be similar between the Frontier Guide and the Homestead Guide, efforts need to be made to make sure the information ported over is still accurate.
This document is client agnostic and examples and tutorials may be based on any client that the author decides to write on, as long as a distinction is made as to what client is being used in the examples/tutorials.

Although overly specific and technical documentation will not be included in the first iterations of this guide, community use and popularity of this guide will dictate future decisions to move Github wiki documentation to this format.

Examples of overly specific and technical documentation include:

* ETHash, CASPER, ABI, RLP, or other technical specs.
* Full API specs for protocols. Caveat: If an example, information, or tutorial needs to reference API calls for a client or interface in order to fulfill its example it is acceptable to reference the specific call. Be sure to make a reference where the user can find remaining pieces of the specific documentation that may be on the GitHub Wiki.

Resources for examplary decumentations
================================================

Here are some examples of previous Ethereum documentation + good examples of documentation. Please add to this list.

* Solidity Docs - https://ethereum.github.io/solidity/docs/home/
* Frontier Guide - https://ethereum.gitbooks.io/frontier-guide/content/
* Gav’s TurboEthereum Guide - https://gavofyork.gitbooks.io/turboethereum/content/
* Ancient EthereumBuilder’s Guide - https://ethereumbuilders.gitbooks.io/guide/content/en/index.html
* Other Ethereum Links: https://souptacular.gitbooks.io/ethereum-tutorials-and-tips-by-hudson/content/giant_ethereum_resource_list.html
* Django Docs - https://docs.djangoproject.com/en/1.9/
* Go wiki - https://ethereum.github.io/go/docs

Restructured text markup, sphinx
=======================================

* best cheat sheet https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst
* quick reference http://docutils.sourceforge.net/docs/user/rst/quickref.html
* official cheat sheet http://docutils.sourceforge.net/docs/user/rst/cheatsheet.txt -> http://docutils.sourceforge.net/docs/user/rst/cheatsheet.html
* rst primer http://sphinx-doc.org/rest.html
* http://sphinx-doc.org/markup/inline.html
* http://sphinx-doc.org/extensions.html#builtin-sphinx-extensions
* http://pythonhosted.org/sphinxcontrib-httpdomain/
* https://pypi.python.org/pypi/sphinxcontrib-golangdomain

Compilation and deployment
=======================================

We use `make` with the autogenerated read-the-docs `Makefile` to build the doc.

..  code-block:: bash

    git clone https://github.com/ethereum/homestead-guide
    cd homestead-guide
    make html

Processing tips
=======================================

Fix section delimiter lines (always use 80-long ones to have correct length)

..  code-block:: bash

  for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\=+$/================================================================================/' > $f.o; mv $f.o $f; done; done
  for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\*+$/********************************************************************************/' > $f.o; mv $f.o $f; done
  for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\-+$/--------------------------------------------------------------------------------/' > $f.o; mv $f.o $f; done
  for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\++$/++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++/' > $f.o; mv $f.o $f; done
  for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\#+$/################################################################################/' > $f.o; mv $f.o $f; done

Migrate and convert old wiki content using pandoc

..  code-block:: bash

  git clone git@github.com:ethereum/go-ethereum.wiki.git
  git clone git@github.com:ethereum/wiki.wiki.git

  mkdir main-wiki.rst
  mkdir go-ethereum-wiki.rst

  for f in `ls wiki.wiki/*.md`; do pandoc $f -o main-wiki.rst/`basename $f .md`.rst; done
  for f in `ls go-ethereum.wiki/*.md`; do pandoc $f -o go-ethereum-wiki.rst/`basename $f .md`.rst; done

