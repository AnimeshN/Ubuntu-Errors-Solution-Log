## Error1:Hash sum mismatch
```
Reading package lists... Done
E: Failed to fetch http://in.archive.ubuntu.com/ubuntu/dists/bionic-updates/main/binary-amd64/by-hash/SHA256/7d488f5060b8200c13e3b730fda57962d56ac4f15d4034b491bbdc5568ac602d  Hash Sum mismatch
   Hashes of expected file:
    - Filesize:557732 [weak]
    - SHA256:7d488f5060b8200c13e3b730fda57962d56ac4f15d4034b491bbdc5568ac602d
    - SHA1:7db49556db8d3cb11e738886e698a5a5d5c8bfaf [weak]
    - MD5Sum:4baef6ade28229e9b22b2d54f6fc5a6f [weak]
   Hashes of received file:
    - SHA256:4361d5af4ad1035e331fdddc7213a77bbc100a1dd13c495b0bdd83d7feb09272
    - SHA1:8b340ade6645fa175a04e5ba350db1b1fd3210d5 [weak]
    - MD5Sum:09801c06f7671d6171ae595b6352c3b6 [weak]
    - Filesize:557732 [weak]
   Last modification reported: Sat, 23 Mar 2019 00:55:13 +0000
   Release file created at: Sat, 23 Mar 2019 02:18:38 +0000
E: Failed to fetch http://in.archive.ubuntu.com/ubuntu/dists/bionic-updates/main/binary-i386/by-hash/SHA256/d556bc66ea5bd7c63c039741f5147b2d91c01e06dad2ec584f6bb3017bcaffe7  
E: Some index files failed to download. They have been ignored, or old ones used instead.
```

## Solution1
```
sudo rm -rf /var/lib/apt/lists/*
sudo apt-get update -o Acquire::CompressionTypes::Order::=gz
sudo apt-get update && sudo apt-get upgrade
```
