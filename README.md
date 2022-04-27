# 20BCE0340_TheoryDA
This Repository contains the files for the Theory DA submission on Merkle Trees

## ** **1. Introduction to Merkle Trees** **

A Merkle tree is a hash-based data structure that is a generalization of the hash list. It is a tree structure in which each leaf node is a hash of a block of data, and each non-leaf node is a hash of its children. Typically, Merkle trees have a branching factor of 2, meaning that each node has up to 2 children.

Merkle trees are used in distributed systems for efficient data verification. They are efficient because they use hashes instead of full files. Hashes are ways of encoding files that are much smaller than the actual file itself. Currently, their main uses are in peer-to-peer networks such as Tor, Bitcoin, and Git.

In various distributed and peer-to-peer systems, data verification is very important. This is because the same data exists in multiple locations. So, if a piece of data is changed in one location, it's important that data is changed everywhere. Data verification is used to make sure data is the same everywhere.
However, it is time-consuming and computationally expensive to check the entirety of each file whenever a system wants to verify data. So, this is why Merkle trees are used. Basically, we want to limit the amount of data being sent over a network (like the Internet) as much as possible. So, instead of sending an entire file over the network, we just send a hash of the file to see if it matches.

The protocol goes like this:

1.	Computer A sends a hash of the file to computer B.
2.	Computer B checks that hash against the root of the Merkle tree.
3.	If there is no difference, we're done! Otherwise, go to step 4.
4.	If there is a difference in a single hash, computer B will request the roots of the two subtrees of that hash.
5.	Computer A creates the necessary hashes and sends them back to computer B.
6.	Repeat steps 4 and 5 until you've found the data blocks(s) that are inconsistent. It's possible to find more than one data block that is wrong because there might be more than one error in the data.


Note that each time a hash is found to match, we need n more comparisons at the next level, where n is the branching factor of the tree.

This algorithm is predicated on the assumption that network I/O takes longer than local I/O to perform hashes. This is especially true because computers can run in parallel, calculating multiple hashes at once.


Because the computers are only sending hashes over the network (not the entire file), this process can go very quickly. Plus, if an inconsistent piece of data is found, it's much easier to insert a small chunk of fixed data than to completely rewrite the entire file to fix the issue.


The reason that Merkle trees are useful in distributed systems is that it is inefficient to check the entirety of file to check for issues. The reason that Merkle trees are useful in peer-to-peer systems is that they help you verify information, even if some of it come from an untrusted source (which is a concern in peer-to-peer systems).


The way that Merkle trees can be helpful in a peer-to-peer system has to do with trust. Before you download a file from a peer-to-peer source—like Tor—the root hash is obtained from a trusted source. After that, you can obtain lower nodes of the Merkle tree from untrusted peers. All of these nodes exist in the same tree-like structure described above, and they all are partial representations of the same data. The nodes from untrusted sources are checked against the trusted hash. If they match the trusted source (meaning they fit into the same Merkle tree), they are accepted and the process continues. If they are no good, they are discarded and searched for again from a different source .

## ** **Architecture of a Merkle Tree** **

So, technically, Merkle trees are data structure trees where the non-leaf node is defined as a hash value of its respective child nodes.

This also means that the Merkle tree is inverted down where the leaf nodes are the lowest node. 

**At the core of Merkle trees, we need to learn three important terms. They are as below:**

- Merkle Root
- Leaf Nodes
- Non-Leaf Nodes

If you look at the Merkle tree, it is an upside-down tree. The tree can summarize a whole set of transactions by itself. This means that the user can verify if a transaction is part of the block or not.

To make Merkle trees work, hashing is used. It simply does the hashing pairs of nodes repeatedly until only one hash value is left. The left hash value is known as Merkle Root or the Root Hash. The tree is created from the bottom up using the individual transactions hashes. The individual transaction hashes are also known as Transaction IDs. 

The leaf nodes are the nodes that contain transactional data hashes. In the case of the non-leaf nodes, they store the hash of the two previous hashes.

Another important property of Merkle trees is that it is binary in nature. This means that it requires leaf nodes to be even for it works. In case, if there is an odd number of leaf nodes, it will simply duplicate the last hash and make it even.

### **An Example**

Let’s try to understand it by taking an example.

![Architecture](https://github.com/SoumodeepChakraborty/20BCE0340_TheoryDA/blob/main/Merkle.1jpg.png)

Here, we see that four transactions have taken place in the block. These transactions are named X, Y, Z, and W. The transactions are then hashed and then stored in leaf nodes which we name as Hash X, Hash Y, Hash Z, and Hash W.

Once done, the leaf nodes of Hash X, Y, Z, and W are again hashed and created into a combined hash of XY and ZW. Finally, these two hashes are used to create the Merkle Root or Root Hash.

The whole process of hashing can be done on a very large data set which makes the Merkle Trees data structure useful in the case of decentralized networks.

As we discussed earlier, hashing algorithms usage depends on the implementation. However, one of the most common hash functions that are used includes the SHA-2 cryptographic hash function. 

So, a transaction can be verified if the previous transactions are verifiable, thanks to the hash values.



Here, we see that four transactions have taken place in the block. These transactions are named X, Y, Z, and W. The transactions are then hashed and then stored in leaf nodes which we name as Hash X, Hash Y, Hash Z, and Hash W.

Once done, the leaf nodes of Hash X, Y, Z, and W are again hashed and created into a combined hash of XY and ZW. Finally, these two hashes are used to create the Merkle Root or Root Hash.

The whole process of hashing can be done on a very large data set which makes the Merkle Trees data structure useful in the case of decentralized networks.

As we discussed earlier, hashing algorithms usage depends on the implementation. However, one of the most common hash functions that are used includes the SHA-2 cryptographic hash function. 

So, a transaction can be verified if the previous transactions are verifiable, thanks to the hash values.

## ** **3.Algorithm** **

### **Find Operation in Merkle Tree**

This function is used to **check whether the given key is present** in the Merkle tree or not. If it is present then it will return that node else it will return null.

Step 1: We will take tree and key as parameters.

Step 2: If the tree is null then we will return null.

Step 3: If the tree->key is equal to the key we will return the tree.

Step 4: If the key is smaller than tree->key then we will return find(tree->left, key)

Step 5: else return find(tree->right, key)


### **Add Operation in Merkle Tree**

This function is used to **add a node** into the Merkle tree.

Algorithm to add a node in Merkle tree.

Step 1: We will take key and value as parameters.

Step 2: Take the hash(key) and store it in a variable called index.

Step 3: store (struct node*) arr[index].head in a pointer called tree of datatype node.

Step 4: create a new node with its key as key and value as value and both links as null.

Step 5: If the tree is null then assign the new node to the head and increment the size by 1.

Step 6: If the tree is not null then we will check if the key is already present in the tree using the find function.

Step 7: If the key is already present in the tree then we will update the value.

Step 8: If it is not present in the tree then we will use the insert function to insert the element.

**Algorithm of insert function.**

Step 1: It will take tree and item pointers of node data type as parameters.

Step 2: If item->key is smaller than tree->key and tree->left is null then assign the item to tree->left.

Step 3: If item->key is smaller than tree->key and tree->left is not null then call insert function with tree->left and item as parameters.

Step 4: If item->key is greater than tree->key and tree->right is null then assign the item to tree->right.

Step 5: If item->key is greater than tree->key and tree->right is not null then call insert function with tree->right and item as parameters.

### **Delete Operation in Merkle Tree**

This function is used to **delete a node from Merkle tree.** If the key given is present in the Merkle tree then it will delete the node from the tree.

Algorithm to delete a node in Merkle tree.

Step 1: We will take a key as a parameter.

Step 2: Take the hash(key) and store it in a variable called index.

Step 3: store (struct node*) arr[index].head in a pointer called tree of datatype node.

Step 4: If the tree is null then the key is not present.

Step 5: If the tree is not null then we will check if the key is already present in the tree using the find function.

Step 6: If the find function returns null then the key is not present in the tree.

Step 7: If it is not null then we will use the remove function to delete the element.

**Algorithm of remove function.**

Step 1: It will take tree and key as parameters.

Step 2: If the tree is null then return null.

Step 3: If the key is smaller than the tree->key then tree->left is equal to remove(tree->left, key) and return tree.

Step 4: If the key is greater than the tree->key then tree->right is equal to remove(tree->right, key) and return tree.

Step 5: else if the tree->left is equal to null and the tree->right is equal to null then decrement the size and return tree->left.

Step 6: else if the tree->left is not equal to null and the tree->right is equal to null then decrement the size and return tree->left.

Step 7: else if tree->left is equal to null and tree->right is not equal to null then decrement the size and return tree->right.

Step 8: else assign tree->left to a pointer called left of data type node.

Step 9: While left->right is not equal to null, left is equal to left->right.

Step 10: tree->key is equal to left->key.

Step 11: tree->value is equal to left->value.

Step 12: tree->left is equal to remove(tree->left, tree->key).

Step 13: Return tree.

## ** **Illustrate the Steps of the Algorithm** ** 

A Merkle tree is constructed by recursively hashing pairs of nodes until there is only one hash.

![Image of Merkle Tree](https://github.com/SoumodeepChakraborty/20BCE0340_TheoryDA/blob/main/Merkle.jpg)

a, b, c, and d are some data elements (files, JSON, etc) and H is a hash function.

a hash function acts as a “digital fingerprint” of some piece of data by mapping it to a simple string with a low probability that any other piece of data will map to the same string.

Each node is created by hashing the concatenation of its “parents” in the tree.

#### Note: Merkle tree are mostly a binary tree but there are also Trees. Platforms like Ethereum use nonbinary tree.


## ** **Create and Verify the Merkle Tree** **
### Files added to the Repository


## ** **References** **
1. ![google link](https://101blockchains.com/merkle-trees/)
2. ![google link](https://www.geeksforgeeks.org/introduction-to-merkle-tree/#:~:text=Merkle%20tree%20also%20known%20as,as%20far%20left%20as%20possible.)
3. ![google link](https://brilliant.org/wiki/merkle-tree/)
