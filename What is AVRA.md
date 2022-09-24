# What is AVRA?
202209200054

AVRA stands for Automated Vulnerability and Risk Analysis. It is a tool created for the purpose of adding objectivity and repeatability to the cyber risk assessment (CRA) process. 

It does this by automating the following processes:
- [[System Scanning]]
- [[Automated Fact Generation|Fact Generation]]
- [[Attack Graph Generation]] - We can leverage the logic programming representation of the system to derive an attack graph, which is essentially a blueprint of the different ways in which an attacker is able to achieve some cyber effect on the system. Given our knowledge base and interaction rules, we can pose queries, such as: Can an attacker gain control over a certain node in the system? The logic programming engine will attempt to prove the truth of this query; if it is able to do so, it will generate an attack graph representation of all the conditions that need to be satisfied in order for the query to be true.
- [[Exploitation]] - It is not enough to have an attack graph listing the theoretical ways in which an attack may be carried out--we must go a step further and actually attempt to carry out the attacks described in the attack graph. To do, we leverage the [[Metasploit Framework.]] An automated exploitation tool will traverse the attack graph and marshal any necessary parameters to the Metasploit Framework so that it will actually carry out the attacks described in the attack graph. This way we can be assured that the attack graph is actually representative of attacks that are practically exploitable in the real world, not just in the realm of the theoretical.

The approach described here of using [[Logic Programming|logic programming]] to represent a system and the interactions that are possible within that system falls under the category of [[Expert Systems]].

#AVRA 
#LogicProgramming 
#Cyber