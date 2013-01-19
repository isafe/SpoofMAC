# SpoofMAC - Spoof your MAC address in Mac OS X

I made this because changing your MAC address in Mac OS X is harder than it
should be. The biggest annoyance is that the Wi-Fi card (Airport) needs to be
*manually* disassociated from any connected networks in order for the change
to be applied correctly. Doing this manually every time is tedious and lame.

Instead of doing that, just run this Python script and change your MAC address
in one command.

# Installation

You can install from pypi using `easy_install` or `pip`:

```
pip install SpoofMAC
easy_install SpoofMAC
```

or clone/download the repository and install with `setup.py`. Ex:

```
git clone git://github.com/feross/SpoofMAC.git
cd SpoofMAC
python setup.py install
```

# Usage

SpoofMAC installs a command-line script called `spoof-mac`. You can always
see up-to-date usage instructions by typing `spoof-mac --help`.

## Examples

Some short usage examples.

### List available devices, but only those on wifi:

```
spoof-mac list --wifi
- "Wi-Fi" on device "en0" with MAC address 70:56:51:BE:B3:6F
```

### Randomize Wireless MAC address

You can use the hardware port name, such as:
```
spoof-mac randomize wi-fi
```

or the device name, such as:

```
spoof-mac randomize en0
```

### Reset device to its original MAC address

While not always possible (because the original physical MAC isn't
available), you can try setting the MAC address of a device back
to its burned-in address using `reset`:

```
spoof-mac reset wi-fi
```

(older versions of OS X may call it "airport" instead of "wi-fi")

## Optional: Run automatically at startup

OS X doesn't let you permanently change your MAC address. Every time you restart your computer, your address gets reset back to whatever it was before. Fortunately, SpoofMAC can easily be set to run at startup time so your computer will always have the MAC address you want.

### Startup Installation Instructions

Run the following commands in Terminal:

```bash
# Clone the code
mkdir ~/Scripts
git clone https://github.com/feross/SpoofMAC.git ~/Scripts/SpoofMAC

# Copy files to the OS X startup folder
cd ~/Scripts/SpoofMAC
sudo mkdir /Library/StartupItems/SpoofMAC
sudo cp misc/SpoofMAC misc/StartupParameters.plist /Library/StartupItems/SpoofMAC

# Set file permissions
cd /Library/StartupItems/SpoofMAC
sudo chown root:wheel SpoofMAC StartupParameters.plist
sudo chmod 0755 SpoofMAC
sudo chmod 0644 StartupParameters.plist

# Delete
rm -rf ~/Scripts/SpoofMAC
```

By default, the above will randomize your MAC address on computer startup. You can change the command that gets run at startup by editing the `/Library/StartupItems/SpoofMAC/SpoofMAC` file.

```bash
sudo vim /Library/StartupItems/SpoofMAC/SpoofMAC
```

## Changelog

- 1.1.0 Fix regression: List command now shows current MAC address (feross)
- 1.0.0 Complete rewrite to conform to PEP8 (tyler).
- pre-1.0 Original version (feross).

## Contributors

- Feross Aboukhadijeh <http://feross.org>
- Tyler Kennedy <http://www.tkte.ch>

*Improvements welcome! (add yourself to the list)*

## MIT License

Copyright (c) 2011-2013

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
