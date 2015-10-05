---

title: Backtracking
layout: page
sidebar: true

---


<p class="message">
Note: these notes are incomplete! I'm not sure why we use conflict sets in CBJ. If anyone can enlighten me as to how these improve on Chronological Backtracking, please send a pull request or enlighten me!
</p>



Various algorithms are used. 
Particularly of note are Chronological Backtracking and CBJ, the algorithms for which are on the slides. 

## Chronological backtracking

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

Some things to think about when considering the implementations of these algotithms:

- Maybe we should consider representing variables in an order that isn't lexicographical? 
	- For example, ordering them in order of the number of constraints they have, so that the most constraining variables can be dealt with first?
- How do we represent constraints?
	- What *are* they?
- Chronological backtracking is pretty dumb
  - Actually, it's *really* dumb. 
	- It'll eventually find a solution, but it's slow and it's entirely unoptimised. It's just a *method*, without any reasoning behind it. 
	- Chronological backtracking isn't intelligent about what causes conflicts
	  - This means it can't target the problematic variables and resolve their constraints quickly
  - There's no inference or propogation either, so possibility spaces are never trimmed


## CBJ

A constraint satisfaction problem finds a configuration of values that satisfy a tripe of variables, domains, and constraints. 

When finding those values via chronological backtracking, sometimes we end up trying many possible configurations due to a single variable's constraints that is far down the stack of variables with values assigned. If the variable is the first to get a value, but is constrained by the last few variables, then in Chronological Backtracking, we would try every possible configuration of values of variables between those last variables and the first one. 

For a possibility set of *n* for each of *m* variables, we have *(M-1)^N* tests to make before we begin changing the first variable again. That's a lot of thrashing. 

CBJ attempts to minimise thrashing caused by this lack of contextual awareness by updating conflict sets for each node. 

In CBJ, we backtrack as normal, but keep track of the conflicts caused by every backtrack by backtracking to the last node to have a problem, rather than the last visited node. When we visit this node, we make the conflict set of that node the union of the conflict set of the other node and this node, minus the conflicting node itself. 

This is the program learning the cause of conflicts, then avoiding changing values not relevant to the root of the problem. In this way, CBJ attempts to minimise thrashing. 

Notably, CBJ is essentially chronological backtracking, except rather than moving through nodes in chronological order of when they were last visited, CBJ jumps back to the node causing a conflict when backtracking. 

Backtracking search is like a "crippled" CBJ; it just moves to the previous variable, not the conflicting variable. 


---

## Summary

Two algorithms worth knowing:

1. Chronological Backtracking
2. CBJ

Chronological backtracking assigns values to variables, and on each assignment, it checks that that value doesn't break a constraint. If any constraints are broken given the current configuration of values, the next value in the node's possibility space is chosen. If all possibilities are exhausted, the algorithm *backtracks* to the last visited node and moves to the next value in that node's possibility space. While this is guarenteed to find a solution, it certainly doesn't guarentee finding it quickly. 

CBJ is a vaguely intelligent version of Chronological Backtracking: it changes the values of the nodes causing the conflict, so the roots of problems are attacked early on. A simple couple of midifications to Chronological Backtracking are required to implement CBJ: 

- When a conflict arises, move back to the other node involved in the conflict
- Update the conflict set of the node being moved to as the union of the two involved nodes' conflict sets, minus the node being moved to


<p class="message">
What's the conflict set used for? Where does it come into the algorithm?
</p>
