# 💠𝗕𝗟𝗢𝗖𝗞𝗖𝗛𝗔𝗜𝗡💠

## Hyperledger Fabric Samples
you can use Fabric samples to get started working with Hyperledger Fabric, explore important Fabric features, and learn how to build applications that can interact with blockchain networks using Fabric SDKs. 

## Getting started with Fabric samples
To use the Fabric samples, you need to download the Fabric Docker images and Fabric CLI tools.

1.```bash
sudo apt install golang-go

  
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
   8.``` ipfs daemon```
 ![Screenshot (9)](https://github.com/user-attachments/assets/af70e3f9-aa99-4900-bde5-1e702faec198)

 ![Screenshot 2025-04-10 103327](https://github.com/user-attachments/assets/c0b5fd35-2348-467b-a71c-d37f6e41305c)

   9. On Browser: http://127.0.0.1:5001/webui
   10. To run ipfs daemon in background: ipfs daemon > ipfs.log 2>&1 &
   11. This is daemon ID:[1] 772
   12. Add file: echo "Hello,IPFS!" > hello.txt
   13. ```ipfs add hello.txt```
![Screenshot 2025-04-10 104119](https://github.com/user-attachments/assets/1400bd31-0ab7-480f-bb2d-a72c9f276b23)

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
  
   20.```ipfs add <videoPath>```
   ![Screenshot 2025-04-10 110430](https://github.com/user-attachments/assets/ded33e55-c2f9-4ee1-868a-aceb71be7ac0)



###Assignment
Perform encryption and privacy on IPFS through command line:
IPFS privacy and encryption
  1. echo "Hello,IPFS!" > myfile.txt
  2. ipfs add myfile.txt
  3. openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -salt -in myfile.txt -out myfile_encrypted.txt -pass pass:Yourpassword
  4. ipfs add myfile_encrypted.txt
 ![Screenshot 2025-04-10 111915](https://github.com/user-attachments/assets/7aa5d0dd-e5ac-4f05-9e4e-6cdf243d2407)

  5. cat myfile_encrypted.txt
  6. openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -in myfile_encrypted.txt -out decrypted_file.txt -pass pass:Yourpassword
  7. cat decrypted_file.txt
  8. ipfs add decrypted_file.txt

## METAMASK

We will be using MetaMask as our Ethereum wallet and browser-based interface. MetaMask allows us to manage Ethereum accounts, sign transactions, and interact with decentralized applications (dApps).
For our development and testing environment, we will use the Sepolia Test Network. Sepolia is one of Ethereum's official proof-of-stake test networks designed for testing smart contracts and blockchain interactions without using real ETH.

![Screenshot 2025-04-10 113011](https://github.com/user-attachments/assets/770966d1-5e5d-426c-912e-bae4837e526a)

### SEPOLIA FAUCET

To perform operations like deploying contracts or sending transactions on the Sepolia testnet, we need test ETH (which has no real-world value). For this, we will use the Google Cloud Web3 Faucet.

This faucet provides free Sepolia ETH for development purposes. It is hosted by Google Cloud and is accessible at the following URL:

🔗 https://cloud.google.com/application/web3/faucet/ethereum/sepolia
![Screenshot 2025-04-10 113102](https://github.com/user-attachments/assets/ae3b0aa5-490e-4d5d-94f9-5d4ae8a20951)

## SOLIDITY

Solidity is a programming language used to write smart contracts on the Ethereum blockchain

### Remix IDE
Remix IDE is a web-based tool that lets you write, compile, test, and deploy those smart contracts easily in your browser.
![Screenshot 2025-04-10 115244](https://github.com/user-attachments/assets/ff07f6ee-a723-474e-bd24-921c623dccdb)

### 1. First project on solidity
   we are going to create a application that can store information on blockchain
    -we will create a new file named simpleStorage.sol
  ### Defining a solidity version
so the first thing you are going to need in any solidity program is the SPDX License Identifier which we use because SPDX license identifiers are used to make it clear what license a piece of software is under. They are like a shorthand code that tells you the rules for using, modifying, and sharing the software. This helps everyone understand the terms quickly and easily, making it simpler to use and share open-source software. And solidity version that's always gonna be on top of your solidity code. eg.   

```// SPDX-License-Identifier: MIT ```

 ```  pragma solidity >=0.6.0 <0.9.0;```
    
  ### Defining a contract
the next thing we are going to do is defining a contract so contract is a keyword in solidity which stands for our smart contract

now we can deploy our smart contract on a simulated environment


 ![Screenshot 2025-04-10 122453](https://github.com/user-attachments/assets/d881da12-c702-44c9-ba8f-96c3fa7c030a)

we can store some value also 


 ![Screenshot 2025-04-10 122754](https://github.com/user-attachments/assets/c588a92f-95c4-4699-a260-83ccf4843091)

now after adding public in front of our favoriteNumber we can see it in our interface


 ![Screenshot 2025-04-10 123520](https://github.com/user-attachments/assets/aa14613d-6ebf-4a30-89f9-8c865937e118)

Finally, after adding more data to our contract we will deploy it on our testNetwork which is sepolia so first we will connect our metamask to our remix IDE


 ![Screenshot 2025-04-10 130822](https://github.com/user-attachments/assets/f5509382-e380-4c01-8d1a-3f8f8e6f661d)
 ![Screenshot 2025-04-10 131837](https://github.com/user-attachments/assets/495f4fee-1a0f-4d9f-83ff-24f3ae8da62f)
![Screenshot 2025-04-10 131918](https://github.com/user-attachments/assets/496191aa-3865-4a51-8ecc-bed88013d35d)






