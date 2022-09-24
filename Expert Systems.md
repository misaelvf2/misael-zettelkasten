# Expert Systems
202209200113

The term "expert system" is one that was commonly used in the context of [[Traditional AI]]. Traditional AI, contrasted with modern [[Machine Learning]] approaches, is concerned with endowing software-based agents with the ability to reason about the world (or a particular problem domain). 

Rather than relying on statistical patterns (as in modern ML approaches), traditional AI uses systems of logic to derive answers from first principles. These first principles, as well as the rules for how we can derive higher-order principles, are encoded with statements in some logic programming language.

In an expert system, we try to encode as many of these first principles and rules as possible about a given knowledge domain.

For example, if our domain of interest were air traffic control, then we would write all sorts statements about who are the actors in the domain of air traffic control?; how do they interact?; what are the procedures and business rules? Everything that a human expert might conceivably be expected to know about the domain is all encoded in our system by means of logic programming statements.

This logic programming representation of the domain is now our expert system. We can pose questions to our expert system--the same kinds of questions we might pose to a human expert. The advantage of the expert system, of course, is that it is able to reason about the problem with much higher precision and at a much greater level of depth than a human could. This is the core of the appeal of expert systems.

[[Advantages of Expert Systems]]
[[Disadvantages of Expert Systems]]

#AVRA 
#LogicProgramming
#TraditionalAI