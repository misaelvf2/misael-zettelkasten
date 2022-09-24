# Automated Fact Generation
202209200113

In [[Logic Programming|logic programming]], we encode knowledge about the particular domain we are working with in the form of facts and interaction rules. Facts in this context represent things that are assumed to be unconditionally true, while interaction rules define how the facts may be combined to deduce further facts.

The sum of all our facts and interaction rules is our knowledge base--sometimes called "database."

These facts may be input manually by a user, or automatically. In this note, we describe automated fact generation of the sort used by [[What is AVRA|AVRA]].

Information about a domain compiled in some manner--either manually or automatically, as with [[System Scanning|system scanning]], can be converted to facts in a logic programming language.

Facts may encode information such as, "Host A is vulnerable to CVE X." This fact in conjunction with other similar facts about the system may be combined to derive a higher order fact, such as, "an attacker is able to gain control over host A," as dictated by the interaction rules. This logic programming-based system with highly specialized knowledge about a particular domain is also called an [[Expert Systems|expert system]].

#AVRA 
#LogicProgramming 