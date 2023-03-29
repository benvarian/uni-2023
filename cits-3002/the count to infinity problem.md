
- serious problem with distance vectoring which is it requires them all to be modified in networks where the reliability is uncertain 
- ![[Screenshot 2023-03-29 at 12.11.27 pm.png]]
- in part a we assume that router A is intially down - all others routers record an infinite distanct to router A
- when router A returns, each other router eventually hears of its return, one router at a time good news travel fast 
- However, consider the dual problem in (b). Router A is initially up. All other routers know the distance to A. Now, router A crashes - router B first senses that A is now an infinite distance away. However, B is excited to learn that router C is a distance of 2 to A, and so B chooses to now send traffic to A via C (a distance of 3).
- At the next exchange, C notices that its 2 neighbours each have a path to A of length 3. C now records its path to A, via B, with a distance of 4. At the next exchange, B has direct path to A (of infinite distance), or one via C with a distance of 4. B now records its path to A is via C with a distance of 5.....