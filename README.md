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
