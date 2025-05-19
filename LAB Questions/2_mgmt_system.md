# Student Records Management System
This contract stores student records (name and roll number). We use a struct for a student and a mapping(uint => Student) 
to retrieve records by a numeric key (e.g. an auto-incremented ID or roll number). Only the contract owner can add records, demonstrated with an onlyOwner modifier:
  - Data storage: We define struct Student { string name; uint rollNumber; } and a mapping(uint => Student).
  - Add/retrieve: A function addStudent (restricted to the owner) lets one add a student. A getStudent view function 
    returns stored data for a given ID.
  - Access control: We set owner = msg.sender in the constructor and use a modifier to restrict addStudent

## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StudentRecords {
    struct Student {
        string name;
        uint rollNumber;
    }
    address public owner;
    uint public nextId;
    mapping(uint => Student) public students;  // map record ID to Student

    // Modifier to restrict functions to only the contract deployer
    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this");
        _;
    }

    constructor() {
        owner = msg.sender;  // deployer is the owner
    }

    // Owner adds a new student record
    function addStudent(string memory _name, uint _rollNumber) public onlyOwner {
        students[nextId] = Student(_name, _rollNumber);
        nextId++;
    }

    // Retrieve a student record by its ID
    function getStudent(uint id) public view returns (string memory name, uint rollNumber) {
        Student storage s = students[id];
        return (s.name, s.rollNumber);
    }
}

```
## Deployment

![Screenshot from 2025-05-19 16-30-44](https://github.com/user-attachments/assets/6d984760-545f-45cb-ba8d-7d0a6c617e36)

![Screenshot from 2025-05-19 16-32-30](https://github.com/user-attachments/assets/0e62d2d8-c6f8-43e9-84bd-b22885add4ee)

![Screenshot from 2025-05-19 17-01-37](https://github.com/user-attachments/assets/8d835a71-31c9-45a8-a413-22b42f226a5e)

