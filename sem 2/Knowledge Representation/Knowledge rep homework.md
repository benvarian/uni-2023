## Formalise the rules and facts in first order logic
### Rules 
- Each user can follow one or more other users 
	- $\forall{X}\forall{Y} \; f(X,Y)$ $\implies$ $user(X) \land user(Y)$       
- Each user can write posts 
	- $\forall{X}\forall{Y} \; w(X,Y)$ $\implies$ $user(X) \land post(Y)$       
- Each user can see posts 
	- $\forall{X}\forall{Y} \; s(X,Y)$ $\implies$ $user(X) \land post(Y)$       
- Each user can like posts 
	- $\forall{X}\forall{Y} \; l(X,Y)$ $\implies$ $user(X) \land post(Y)$       
- Every user follows themselves 
	- $\forall{X} \; f(X,X)$ $\implies$ $user(X) \land user(X)$       
- A user can only like a post if they can see that post 
	- $\forall{X}\forall{Y} \; l(X,Y)$ $\implies$ $s(X,Y)$       
- A user can only see a post if it was written or liked by someone that they follow
	- $\forall{X}\forall{Y}\forall{Z} \; s(X,Y)$ $\implies$ $f(X,Z) \land (w(Z,Y) \lor l(Z,Y)$        

### Facts
- Jack follows Jamie 
	- $f(Jack, Jamie)$
- Jamie follows Jamal 
	- $f(Jamie,Jamal)$
- Jamal follows Jack
	- $f(Jamal, Jack$)
- Jamal Posts "Hi!"
	- $w(Jamal,Hi!)$ 
	- i couldnt get quotes to work in latex, so imagine theres quotes around Hi!
- Jamie likes Jamals post 
	- $l(Jamie,Jamal)$

## Convert the first order logic statement into a CNF knowledge base 
1. $f(X,Y)$
2. $w(X,Y)$
3. $s(X,Y)$
4. $l(X,Y)$
5. $f(X,X)$
6. $\neg l(X,Y) \lor s(X,Y)$   
7. $\neg s(X,Y) \lor f(X,Z) \land (w(Z,Y) \lor l(Z,Y)$  

## Apply casual resolution to show that Jack can see Jamal's post 
- $s(Jack,Jamal's Post)$ $\implies$ $f(Jamal,Jack) \land (w(Jamal ,Jamal's Post) \lor l(Jamal,Post)$    
- Jamal's post = "Hi!"
- $f(Jamal,Jack) = True$ 
- $w(Jamal, Jamal's Post) \lor l(Jamal, Post) = True$ 
- $\therefore$ Jack can see Jamal's Post

## Describe the statement in natural language and explain why it is intuitively valid 
- ![[Screenshot 2023-08-23 at 8.53.15 pm.png]]
- There are two people who are neighbours with each other and there is someone who knows all people in the space, if person X  is a neighbour with person Z and person Z is a neighbour of person Y

## apply the following natural deduction system to prove that it is valid!
- ![[IMG_2947 copy.jpg]]
# Please find q3 attached in the submission
- please exclude the show_string(X) function from testing as my solution doesn't require it