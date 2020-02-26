# NetCatSecure# SNC -- Secure Net Cat Utility
SNC is a Python script that utilizes Pycrytodome to receive and deliver encrypted messages. Using a shared key, these messages can then be decrypted using AES256-GCM.
- The following assumes you are running the latest version of Python3.

# Pycryptodome
Pycryptodome will be required to use snc's AES MODE_GCM encryption/decryption. The program will not work without it.


Installation:
```
pip3 install pycryptodome
```
Check:
```
python3 -m Crypto.SelfTest
```


# Arguments
```
Usage: snc [-h] --key KEY [--listen LISTEN] [hostname] [portNumber]

positional arguments:
  hostname                          List hostname 
  portNumber                        List port number

optional arguments:

  -h, --help                        Show this help message and exit
  --key KEY, -k KEY                 List encryption key
  --listen LISTEN, -l LISTEN        Listen for port number
```

# How to ...
The script will need to be running from both the Server and Client-side, to send and receive messages. Both sides will require a shared key.

Example:

```
Host
./snc --key THISISAKEY -l 133 < sent_file.txt

client
./snc --key THISISAKEY 127.0.0.1 133 > recieved_file.txt
```

The script will also support bi-lateral movement and can send and receive data at the same time.

Example:
```
Host
./snc --key THISISAKEY -l 133 < sent_file.txt > server.txt

client
./snc --key THISISAKEY 127.0.0.1 133 > recieved_file.txt < client.txt
```
# Notice
*When Sending data from the the Server side, the Server will close as soon as all data has been sent and/or decrypted.
Additional time might need to be given to allow the Client to decrypt the receiving ciphers. (It is unlikely that a timeout has occurred.)
If you are sending a larger file from the Client side, the Client will wait until the Server has decrypted all data before closing.
In this case both will close at the same time. Text files have been tested as large as 5mb.
