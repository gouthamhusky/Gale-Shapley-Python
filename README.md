# Gale-Shapley-Python


## Introduction

What is the **Stable Matching Problem**?

The [Gale-Shapley algorithm](https://en.wikipedia.org/wiki/Gale%E2%80%93Shapley_algorithm) was introduced to address the popular Stable Matching Problem. In simple terms, we have two pairs of sets, for example men and women who need to be paired upto to form a stable configuration. A stable pair (a, b) is a pair with one element from each set such that both a and b cannot do better than their current match.
The applications of this algorithm are widespread, for example assigning students to their future universities, internet services finding the right user to connect to and so on.

## Key Terms

The key thing to understand about this algorithm are:


1. Define a **preference order**: one of the main componennts of the algorithm is preference order. i.e. each member of a set gets to rank all the members of the other set in the order in their order of preference.


2. A **Perfect Matching** will always be formed: It is one in which, for example if we were to consider the matching between men and women, assuming its monogamous:
 - Each man gets exactly one woman
 - Each Woman gets exactly one man
 
 3. Establishing a criteria for the term **'Stability'**: Given a matching M, an unmatched pair (m, w) is said to be unstable if m and w prefer each other to their current partners. In this case, each one of them could do better by breaking off their current tentative engagements.
 
 4. **Stable matching**: a set of matchings with no unstable pairs
 
 
 ## The algorithm
 
 To put it briefly, the Gale-Shapley algorithm is a propose and reject algorithm that guarantees to find a stable matching.
 Here is a pseudo-code of the algorithm:
  ```
  Initialize all m ∈ M and w ∈ W to free
  while ∃ a free man m who still has a woman w to propose to {
      w = first woman on m’s list to whom m has not yet proposed
      if (w is free)
         (m, w) become engaged
      else {
          if w prefers m to m'
              m' becomes free
              (m, w) get engaged 
          else
              (m', w) remain engaged
      }
  }
  ```
 
 ## The Implementation
 
We take the example of simulating playoffs of a random tournament in this case.
- Each team defines a preference order like `{'TeamA1': deque(['TeamE2', 'TeamF2', 'TeamD3', 'TeamF3', 'TeamE1', 'TeamF1', 'TeamD1', 'TeamD2'])`. A dequeue is used so that we can pop from the left to get our most preferred team to match up against at any given moment
- Initially, all the teams from set A are yet to be matched. While there is atleast one team in set A yet to be matched we run our algorithm
- We define a set element to store our stable configuration as its built/
- Pop out an element from set A (say a) and pop its most preferred matchup (say b). If b:
  1. Does not exist in the current matching: form pair (a, b)
  2. Does exist in the current matching:  If **b** prefers **a** over its current pairing (say a'), then (a, b) will be formed and **a'** will be added back to **remaining_a**. Else nothing will happen as b is happy with its choice, so add **a** back to **remaining_a**.
- Return the final set which contains all the stable pairs


**Note**: function `gale_shapley()` is the implemenation. Rest of the cells contain declaration of sets of different sizes to test out the code

## Miscellaneous
- Other cells to test the algorithm with a growing set size are added and a plot of running time with different set sizes is derived as well
