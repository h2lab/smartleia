
[![GitHub license](https://img.shields.io/github/license/h2lab/smartleia)](https://github.com/h2lab/smartleia/blob/master/LICENSE.bsd3) [![Debian package](https://img.shields.io/debian/v/smartleia/unstable)](https://tracker.debian.org/pkg/smartleia) ![Build status](https://github.com/h2lab/smartleia/actions/workflows/main.yml/badge.svg) [![Sonarcloud Status](https://sonarcloud.io/api/project_badges/measure?project=h2lab_smartleia&metric=alert_status)](https://sonarcloud.io/dashboard?id=h2lab_smartleia)


# SmartLeia

This repository holds the source of the python package used to drive the LEIA
smartcard reader. With it, you will be able to:

    - Connect to the LEIA board
    - Choose parameters for the PSS/PTS negotiation
    - Send APDUs and receive the corresponding responses
    - Activate the DFU mode to download new firmware
    - Start a [Virtual SmartCard](https://frankmorgner.github.io/vsmartcard/) 
      client to use LEIA as a real smartcard reader (through pcscd)

The smartleia package should be compatible with **Python 3.6 and newer**.

## Installation

### From apt

If you use debian or ubuntu, smartleia should be packaged (in the
recent versions of the distros). Simply try:

```sh
apt install smartleia
```

### From git


You may need to use the last version of python builtin's setuptools to install
smartleia from git:

```sh
python -m pip install --upgrade pip setuptools wheel
```

```sh
git clone https://github.com/h2lab/smartleia
cd smartleia
pip install --user .;
```

## Using smartleia with PCSC

It is possible to use smartleia in a PCSC mode, where
it communicates with the PCSC daemon so that you can
use your existing tools (such as `opensc`) to communicate
with the smartcard transparently. Using this mode will require
the installation of `vsmartcard-vpcd` and `vsmartcard-vpicc`,
either from the sources in the [vsmartcard](https://github.com/frankmorgner/vsmartcard)
repository, or from your distro packages (this should be
packaged in recent debian and ubuntu distros):


```sh
apt install vsmartcard-vpcd vsmartcard-vpicc
```

Then, you can lauch PCSC daemon in a terminal:
```sh
pcscd -fad
```

And launch smartleia in PCSC relay mode:
```sh
python3 -m smartleia
```

Of course, you should have your LEIA (or equivalent) board
plugged in using USB as well as a smart card present in the
connector. PCSC should spot a new ATR if everything went fine.
