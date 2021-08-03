## ABE Installation Instructions

+ [GMP](https://gmplib.org/)
+ [PBC](https://crypto.stanford.edu/pbc/download.html)
+ [CHARM](https://github.com/JHUISI/charm)
+ [ABE-python](https://github.com/sagrawal87/ABE)

+ My configurations:
    - ubuntu 20.04
    - openssl (1.1.1f-1ubuntu2.4)
    - python 3.7.11 (sets virtual env)
    - gmp-6.2.1
    - pbc-0.5.14
    - charm-v0.50

+ Result:
    - **SUCCESS** <3
    - Time stamp: 2021/8/3 10:38:50

+ **Note:** If you are lazy, I have provided download saves in my repository
+ **Note:** I considered that python versions which is 3.8+ may encounter error during ***make***
+ **Note:** Many of instructions were compiled from below two references
+ **References:** [Link1](https://lrusso96.github.io/blog/cryptography/2021/03/04/charm-setup.html) (English) and [Link2](http://cxyzjd.com/article/qq_34018719/115007249) (Simplified Chinese)

#### Prerequisites ([gmp](https://gmplib.org/), [pbc](https://crypto.stanford.edu/pbc/download.html), [charm](https://github.com/JHUISI/charm))

1. Before installing, you will need (*if you have already installed one of them before, just skip it*)
    - [ ] sudo apt-get install m4
    - [ ] sudo apt-get install -y flex
    - [ ] sudo apt-get install bison
    - [ ] sudo apt-get install -y openssl
    - [ ] sudo apt-get install -y libssl-dev

2. First, we started from gmp (***gmp-6.2.1.tar.zst*** for example)
    + Enter super user mode ~optional~
        ```shell
        sudo su    # or you add 'sudo' in front of every command below
        ````
    + Expand ***.tar.zst***
        ```shell
        apt get install zstd    # skip if you have already installed before
        tar -I zstd -xvf gmp-6.2.1.tar.zst
        ````
    + Configure and install and check
        ```shell
        cd gmp-6.2.1
        ./configure
        make
        make install
        make check
        ````
    + Some dependencies should be installed finally
        ```shell
        apt-get install -y libgmp10 libgmp-dev
        ````
    - [ ] gmp installation complete

3. Second, we then downloaded pbc library *source code* (***pbc-0.5.14.tar.gz*** for example)
    + Expand ***.tar***
        ```shell
        tar -xvf pbc-0.5.14.tar.gz
        ````
    + Configure and install and check
        ```shell
        cd pbc-0.5.14
        ./configure
        make
        make install
        make check    # optional
        ````
    - [ ] pbc installation complete

4. Some dependencies required before getting into charm (*if you have already installed one of them before, just skip it*)
    + Add python PPA sources and download python 3.7 and dev
        ```shell
        sudo add-apt-repository ppa:deadsnakes/ppa
        sudo apt update
        sudo apt install python3.7 python3.7-dev
        ```
    + Set-up a python 3.7 environment (**py37** for example, you can rename **py37** as you want)
        ```shell
        sudo apt install virtualenv
        virtualenv -p /usr/bin/python3.7 py37
        source py37/bin/activate
        ```
    + Now your PS will look like this
        ```shell
        (py37) user@Ubuntu-20.04:~ $
        ```
    + *Step 5 should be operated under this python environment (py37)*

5. Last, access **charm** github project **v0.50** *(Version 0.50 is required if your openssl version is 1.1 or above)*<br>Some improvements detailed in [official documentation](https://jhuisi.github.io/charm/updates_050.html)
    + v0.50 is not released currently, so we just git clone it from this [repository](https://github.com/JHUISI/charm)
        ```shell
        git clone https://github.com/JHUISI/charm.git
        ````
    + Install all the other dependencies and configure and install and test
        ```shell
        cd charm
        pip install -r requirements.txt
        ./configure.sh
        cd ./deps/pbc && make && sudo ldconfig && cd -    # this command seems downloading pbc-0.5.14.tar.gz again, maybe we can skip it, but I'm not sure with that
        make
        make install && sudo ldconfig    # is lowercase letter 'L', neither number 1 nor uppercase letter 'i'
        make test    # test your charm installation
        ````
    + After tests, it will show message look like
        ```shell
        ===================================== 185 passed, 3 skipped, 6 warnings in 18.36s ======================================
        ```
    + Congratulation <3
    - [ ] Charm installation complete

#### Attribute-Based Encryption python3 ([ABE](https://github.com/sagrawal87/ABE))

+ See [official documentation](https://github.com/sagrawal87/ABE#readme)
+ **NOTE:** we **won't** execute following command
    ```shell
    pip install -r requirements.txt    # this will install charm-crypto in old version 0.43
    ```
+ First, we git clone from this [repository](https://github.com/sagrawal87/ABE)
    ```shell
    git clone https://github.com/sagrawal87/ABE.git
    ````
+ Compile and install
    ```shell
    make && pip install .
    ````
+ Test ABE using **samples/main.py**
    ```shell
    python samples/main.py
    ```
+ You can easily modify samples/main.py to try any scheme you wish.
- [ ] ABE installation complete

### Congratulation! Welcome to world of cryptography
