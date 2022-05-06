---
layout: default
title: Uploading Certificates to NB-IoT
has_children: false
permalink: /docs/power-comm/uploading-certs
parent: Power and Communication
has_toc: false
nav_order: 3
---

# Uploading Certificates to NB-IoT

Certificates are required for communication with AWS. Each device has its own certificates and keys
which are provided by the cloud team.

The NB-IoT module contains a 15MB filesystem where these certificates are stored. When using the
built-in SSL support provided by these modules, it looks in this filesystem to find the keys and
certificates required for connection. As these modules are unique to each device, these files must 
be loaded seperately for each module.

The files required for connection are loaded through the AT-Command modem interface. Inside the firmware 
repository is a python script which will load these from a folder. Instructions on how to use this script
are below.


## Accessing the modem interface on your PC

The easiest way to access the modem is to use an arduino sketch to pass-through the UART channel to your PC. 
This is the easiest option since all the hardware required is already available.

**Note:** the sketch referenced here works *only* on the arduino zero board, and not the UNO.

Inside of the firmware repository is an arduino sketch located in "prototypes/AT_Tester/". To access the modem,
upload this sketch to your board with the NB-IoT hat connected. This will pass through a 115200 baud UART channel
to your PC through the USB port on the zero.

## Running the upload script

In order to run the script you must have python installed and the pyserial library. How to install these are not
explained here.

The python script is located in the firmware repository as "certupload.py". This script takes two arguments. 

The first argument is the serial port which your arduino board is connected to, this is the same one used 
with the "serial monitor" feature inside of the arduino IDE. 

The second argument is a directory containing keys and certificates you wish to upload. The script will look for
the following files, which are all provided by AWS (Some files contain a long device ID at the start of the filename,
just remove this before running the script):

 - AmazonRootCA1.pem
 - AmazonRootCA3.pem
 - certificate.pem.crt
 - private.pem.key
 - public.pem.key

{: .fs-6 .fw-300 }
