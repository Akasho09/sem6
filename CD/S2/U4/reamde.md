## Intermediate Code Generation 

### three Address Code Gen Rules 
![akash](<Screenshot 2025-04-08 at 10.44.16 PM.png>)

## Quards , Triples and Indirect Triples TAC
![alt text](<Screenshot 2025-04-08 at 10.53.35 PM.png>) 
![alt text](<Screenshot 2025-04-08 at 10.53.52 PM.png>)

## BackPatching 
![alt text](<Screenshot 2025-04-08 at 11.18.25 PM.png>)
![alt text](<Screenshot 2025-04-08 at 11.39.22 PM.png>)
![alt text](<Screenshot 2025-04-09 at 12.05.08 AM.png>)
- Triple Representation: Index		            Operator	Arg1	Arg2
                        100	                    <	a	b
       	                101	                    ifTrue	(100)	—
	                    102	                    goto	—	110
	                    103	                    >	c	d
	                    104	                    ifTrue	(103)	—
	                    105	                    goto	—	110
	                    106	                    -	b	c
	                    107	                    ^	(106)	4
	                    108	                    :=	(107)	—
	                    109	                    <	i	n
	                    110	                    ifTrue	(109)	—
	                    111	                    goto	—	114
	                    112                 +	i	2
	                    113	                    :=	(112)	—
	                    114	                    goto	—	109