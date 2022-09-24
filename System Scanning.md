# System Scanning
202209200113

System scanning is a process used to determine the characteristics of a system. The scanning may be passive or active. The particular characteristics may vary depending on the problem domain. In this note, I will describe scanning in the context of a traditional computer system.

The characteristics of a traditional computer system may include the following:
- Installed software packages and programs
- Running software processes
- The users of the system
- Vulnerabilities in the system

The characteristics above refer to node-level information--that is, information relating to a single host in the system. However, we can also gather information relating to a network of such hosts. In this case, characteristics will include the following:
- How are the nodes interconnected?
- Which nodes can communicate with which other nodes?
- What protocols can they use to communicate?
- What communication links are prohibited--e.g., by a firewall rule?

In [[What is AVRA]], we describe the AVRA system and process. The system scanning described in this note is just one of the processes automated by AVRA.

#AVRA