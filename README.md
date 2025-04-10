# Blockchain
## Hyperledger Fabric Samples
you can use Fabric samples to get started working with Hyperledger Fabric, explore important Fabric features, and learn how to build applications that can interact with blockchain networks using Fabric SDKs. 

## Getting started with Fabric samples
To use the Fabric samples, you need to download the Fabric Docker images and Fabric CLI tools.

1.```bash
sudo apt install golang-go```

  
2.docker --version
3.docker-compose -version
4.ls
5.git clone -b main https://github.com/hyperledger/fabric-samples.git
6.cd fabric-samples
7.curl -sSL https://bit.ly/2ysbOFE | bash -s
8.cd test-network
9../network.sh
10. ./network.sh up
11. ./network.sh createChannel
12. ./network.sh down
![Screenshot from 2025-04-07 14-13-14](https://github.com/user-attachments/assets/59c0e94f-690a-43a7-9d0d-e6cb4cf2b115)

![Screenshot from 2025-04-07 14-02-07](https://github.com/user-attachments/assets/6e7f6ad8-079d-4306-adca-b457d25ef317)

##IPFS
IPFS (InterPlanetary File System) is a decentralized, peer-to-peer file storage network where data is stored across multiple nodes, making it more resilient and censorship-resistant.

Key Points:
1.CID (Content Identifier): Files are uniquely identified by a hash of their content.

2.Pinning: Files are pinned to nodes to ensure they stay available.

3.Distributed Storage: Data is spread across many nodes, increasing availability.

4.Decentralized Access: Anyone can retrieve data from any node holding it, using the CID.

5.Use Cases: Web hosting, file storage, NFTs, and version control.

###Why IPFS?
Our peer-to-peer content delivery network is built around the innovation of content addressing: store, retrieve, and locate data based on the fingerprint of its actual content rather than its name or location.

![image](https://github.com/user-attachments/assets/a3ea5bb3-ed4e-4135-b233-3530834f04e0)

###Assignment
Installation of IPFS on local machine. Further, upload the files (such photos,audio,and video) on IPFS and share it with other through content identifier(i.e. hash).
Perform assessment using ubuntu WSL.

Commands(IPFS)
   1. Install the IPFS through WSL:wget
      https://dist.ipfs.tech/kubo/v0.32.1/kubo_v0.32.1_linux-amd64.tar.gz
   2. tar -xvzf kubo_v0.32.1_linux-amd64.tar.gz
   3. Kubo is a reference implementation of IPFS in Go: cd kubo
   4. ls
   5. sudo bash install.sh
   6. ipfs -version
   7. ipfs init
   8. ipfs daemon
   9. On Browser: http://127.0.0.1:5001/webui
   10. To run ipfs daemon in background: ipfs daemon > ipfs.log 2>&1 &
   11. This is daemon ID:[1] 772
   12. Add file: echo "Hello,IPFS!" > hello.txt
   13. ipfs add hello.txt
   14. ipfs cat<CID>
   15. Add a directory:
       mkdir myfolder
       echo "File 1 content" > myfolder/file1.txt
       echo "File 2 content" > myfolder/file2.txt
   16. ipfs add -r myfolder
   17. ps aux | grep ipfs
   18. kill <PID>
   19. in browser you can directly run this to see the IPFS:
       https://ipfs.io/ipfs/QRRHQWIRHIWHRIHWIEHRIWHR


###Assignment
Perform encryption and privacy on IPFS through command line:
IPFS privacy and encryption
  1. echo "Hello,IPFS!" > myfile.txt
  2. ipfs add myfile.txt
  3. openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -salt -in myfile.txt -out myfile_encrypted.txt -pass pass:Yourpassword
  4. ipfs add myfile_encrypted.txt
  5. cat myfile_encrypted.txt
  6. openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -in myfile_encrypted.txt -out decrypted_file.txt -pass pass:Yourpassword
  7. cat decrypted_file.txt
  8. ipfs add decrypted_file.txt




