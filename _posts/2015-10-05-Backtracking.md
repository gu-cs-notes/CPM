---

title: Backtracking
layout: post

---

Various algorithms are used. 
Particularly of note are Chronological Backtracking, the algorithm for which is on the slides. 

Backtracking works on the principle of making assumptions for each variable constrained and seeing whether the constraints are fulfilled. 
If the network fails the constraints, the last variable to be assigned a value is moved to the next value in its possibility space. 
If there are no values in the possibility space that fulfil the constraints for the variable currently looked at, the algorithm *backtracks* and moves to the second last variable edited and moves to the next value in its possibility space. 
Because the search will go through all possibilities unless they are verified not to work, the search will always find a solution if one exists. 
We call searches that are guarenteed to find a solution if one exists *complete searches*. 

This search can be visualised as a tree, where each level of the tree is another variable. 
If the variables are assumed to be on a stack, and are placed on a stack when they are given a possibly-valid value, then each layer of the tree would be the variables as they are added to the stack. 
Note that varibles are always added to the stack in the same order. 

Another way to visualise this is to view the search as a graph, of past variables with instantiated variables, current variable with a vaue being checked for validity (just-assigned value), and a set of future varaibles that are waiting for values to be assigned. 

A problem with this is *thrashing*, where the system will make many changes and backtrack lots, if the vairable that needs changing is far back in the stack. This happens because the algorithm will check every value in the possibility space of each variable after that problematic variable in the stack. 

So other people can use and share the resource, and to avoid redundant effort maintaining multiple sites, throw a pull request into the gu-cs-notes.github.io repo. 


