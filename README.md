*static analysis:*

[![Total alerts](https://img.shields.io/lgtm/alerts/g/sonic-net/sonic-sairedis.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/sonic-net/sonic-sairedis/alerts/)
[![Language grade: C/C++](https://img.shields.io/lgtm/grade/cpp/g/sonic-net/sonic-sairedis.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/sonic-net/sonic-sairedis/context:cpp)

*sairedis builds:*

[![master build](https://dev.azure.com/mssonic/build/_apis/build/status/Azure.sonic-sairedis?branchName=master&label=master)](https://dev.azure.com/mssonic/build/_build/latest?definitionId=12&branchName=master)
[![202205 build](https://dev.azure.com/mssonic/build/_apis/build/status/Azure.sonic-sairedis?branchName=202205&label=202205)](https://dev.azure.com/mssonic/build/_build/latest?definitionId=12&branchName=202205)
[![202111 build](https://dev.azure.com/mssonic/build/_apis/build/status/Azure.sonic-sairedis?branchName=202111&label=202111)](https://dev.azure.com/mssonic/build/_build/latest?definitionId=12&branchName=202111)
[![202106 build](https://dev.azure.com/mssonic/build/_apis/build/status/Azure.sonic-sairedis?branchName=202106&label=202106)](https://dev.azure.com/mssonic/build/_build/latest?definitionId=12&branchName=202106)
[![202012 build](https://dev.azure.com/mssonic/build/_apis/build/status/Azure.sonic-sairedis?branchName=202012&label=202012)](https://dev.azure.com/mssonic/build/_build/latest?definitionId=12&branchName=202012)
[![201911 build](https://dev.azure.com/mssonic/build/_apis/build/status/Azure.sonic-sairedis?branchName=201911&label=201911)](https://dev.azure.com/mssonic/build/_build/latest?definitionId=12&branchName=201911)

# SONiC - SAI Redis - sairedis

## Description

The SAI Redis provides a SAI redis service built on top of redis database. It contains two major components:

1) `SAI library` that puts SAI objects into the redis database.
2) `syncd` that takes the SAI objects and puts them into the ASIC.

## Getting Started

### Install

Before installing, add key and package sources:

    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    echo 'deb http://apt-mo.trafficmanager.net/repos/sonic/ trusty main' | sudo tee -a /etc/apt/sources.list.d/sonic.list
    sudo apt-get update

Install dependencies:

    sudo apt-get install redis-server -t trusty
    sudo apt-get install libhiredis0.13 -t trusty

Install building dependencies:

    sudo apt-get install libtool autoconf dh-exec autoconf-archive

There are a few different ways you can install sairedis.

#### Install from Debian Repo

For your convenience, you can install prepared packages on Debian Jessie:

    sudo apt-get install libsairedis syncd

#### Install from Source

Checkout the source: `git clone https://github.com/sonic-net/sonic-sairedis.git` and install it yourself.

You will also need SAI submodule: `git submodule update --init --recursive`

Get SAI header files into /usr/include/sai. Put the SAI header files that you use to compile
libsairedis into /usr/include/sai

Get ASIC SDK and SAI packages from your ASIC vendor and install them.

Install prerequisite packages:

    sudo apt-get install libswsscommon libswsscommon-dev libhiredis-dev libzmq3-dev libpython-dev

> Note: libswsscommon-dev requires libnl-3-200-dev, libnl-route-3-200-dev and libnl-nf-3-200-dev version >= 3.5.0. If these are not available via apt repositories, you can get them from the latest [sonic-buildimage build](https://sonic-build.azurewebsites.net/api/sonic/artifacts?branchName=master&platform=vs&format=zip&target=target%2Fdebs%2Fbuster).

Install SAI dependencies:

    sudo apt-get install doxygen graphviz aspell

You can compile and install from source using:

    ./autogen.sh
    ./configure
    make && sudo make install

You can also build a debian package using:

    ./autogen.sh
    fakeroot debian/rules binary

If you do not have libsai, you can build a debian package using:

    ./autogen.sh
    fakeroot debian/rules binary-syncd-vs

## Need Help?

For general questions, setup help, or troubleshooting:

- [sonicproject on Google Groups](https://groups.google.com/g/sonicproject)

For bug reports or feature requests, please open an Issue.

## Contribution guide

See the [contributors guide](https://github.com/sonic-net/SONiC/wiki/Becoming-a-contributor) for information about how to contribute.

All contributors must sign an [Individual Contributor License Agreement (ICLA)](https://docs.linuxfoundation.org/lfx/easycla/v2-current/contributors/individual-contributor) before contributions can be accepted. This process is managed by the [Linux Foundation - EasyCLA](https://easycla.lfx.linuxfoundation.org/) and automated
via a GitHub bot. If the contributor has not yet signed a CLA, the bot will create a comment on the pull request containing a link to electronically sign the CLA.

### GitHub Workflow

We're following basic GitHub Flow. If you have no idea what we're talking about, check out [GitHub's official guide](https://guides.github.com/introduction/flow/). Note that merge is only performed by the repository maintainer.

Guide for performing commits:

* Isolate each commit to one component/bugfix/issue/feature
* Use a standard commit message format:

>     [component/folder touched]: Description intent of your changes
>
>     [List of changes]
>
> 	  Signed-off-by: Your Name your@email.com

For example:

>     swss-common: Stabilize the ConsumerTable
>
>     * Fixing autoreconf
>     * Fixing unit-tests by adding checkers and initialize the DB before start
>     * Adding the ability to select from multiple channels
>     * Health-Monitor - The idea of the patch is that if something went wrong with the notification channel,
>       we will have the option to know about it (Query the LLEN table length).
>
>       Signed-off-by: user@dev.null


* Each developer should fork this repository and [add the team as a Contributor](https://help.github.com/articles/adding-collaborators-to-a-personal-repository)
* Push your changes to your private fork and do "pull-request" to this repository
* Use a pull request to do code review
* Use issues to keep track of what is going on
