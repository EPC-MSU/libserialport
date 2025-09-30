# libserialport

> This is a fork of original sigrok’s libserialport library https://github.com/sigrokproject/libserialport
> 
> It was downgraded to add support for older versions of Visual Studio (2013+)

libserialport is a minimal library written in C that is intended to take care
of the OS-specific details when writing software that uses serial ports.

By writing your serial code to use libserialport, you enable it to work
transparently on any platform supported by the library.

The operations that are supported are:

- Port enumeration (obtaining a list of serial ports on the system).
- Obtaining port metadata (USB device information, Bluetooth address, etc).
- Opening and closing ports.
- Setting port parameters (baud rate, parity, etc).
- Reading, writing and flushing data.
- Obtaining error information.

libserialport is an open source project released under the LGPL3+ license.

## Status

The library should build and work on any Windows or Unix-based system. If it
does not, please submit a bug.

Enumeration is currently implemented on Windows, Mac OS X, FreeBSD and Linux.
On other systems enumeration is not supported, but ports can still be opened
by name and then used.

If you know how to enumerate available ports on another OS, please submit a bug
with this information, or better still a patch implementing it.

## Dependencies

No other libraries are required.

## Building the library

### Windows

Open `libserialport.sln` in Visual Studio 2013.

Build (**Build** > **Build Solution**)

### Linux

#### ubuntu 18

Before building check there is no brackets and other non-letter / number / underscore characters in the path to the folder.

Building instructions:

```shell
chmod +x autogen.sh
sudo apt-get install
sudo apt-get install autoconf libtool libpcap0.8 libpcap0.8-dev dos2unix 
dos2unix *
autoreconf -fi
sudo ./autogen.sh
./configure
make
sudo make install
sudo ldconfig
```

#### Debian mipsel

```shell
chmod +x autogen.sh
sudo apt-get update
sudo apt-get install install autoconf libtool libpcap0.8 libpcap0.8-dev dos2unix automake pkg-config
dos2unix *
autoreconf -fi
./autogen.sh
./configure
make
make install
sudo ldconfig
```

### Mac OS

```shell
chmod +x autogen.sh
brew install autoconf libtool libpcap0.8 libpcap0.8-dev dos2unix automake pkg-config
dos2unix *
autoreconf -fi
./autogen.sh
./configure
make
make install
```

## Prebuilt binaries

In case you just need the library binary files for your project you can find the library release for several OS version in `prebuilt` folder.

API
===

Doxygen API documentation is included.

It can also be viewed online at:

  http://sigrok.org/api/libserialport/unstable/

# Examples

* `list_ports` - does not require any arguments.
* `await_events` - requires COM-ports as arguments to track the receive data events.
* `handle_errors` - does not require any arguments.
* `port_config` - requires COM-port as argument.
* `port_info` - requires COM-port as argument. It’s recommended to test this example with ximc or urpc-based controller.
* `send_receive` - requires two connected with each other COM-ports as arguments.

### Windows

Open solution `examples/examples.sln` in Visual Studio.

Choose an example project and build it.

### Linux, Mac OS

Build and install the library.

Then:

```shell
cd examples
make 
./list_ports
```
