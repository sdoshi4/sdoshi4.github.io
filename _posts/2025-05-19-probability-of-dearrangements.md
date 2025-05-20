# Probability of Dearrangement

This is in my opinion, the most beautiful concept I learned in MATH 413: Combinatorics. The question is so simply posed, and it's incredible that the answer arises naturally. Also I couldn't explain it to Shyamala in Everitt so now I finally can!

## The question
To define a dearrangement, let's first start by defining a permutation. A permutation is a bijective mapping from one ordering of a set to another. That is,

$$\pi: S \leftrightarrow S $$ 

is a permutation. This is a pretty crappy definition in my opinion though, so let's clarify with an example. A permutation of the set $[5] = \{1, 2, 3, 4, 5\}$ could be described in the table below:

$$
\begin{array}{|c|c|}
\hline
x & \pi(x) \\
\hline
1 & 3 \\
2 & 2 \\
3 & 1 \\
4 & 5 \\
5 & 4 \\
\hline
\end{array}
$$

Notice that this is completely bijective and cardinality preserving, and just represents a different ordering of the elements in our set.

Now that we've defined a permutation, we can define a dearrangement. A dearrangement is a permutation such that no element matches to itself. More formally, a derrangement is:

$$\pi: S \leftrightarrow S \ | \  \pi(i) \neq i \quad \forall i \in S$$ 

Notice that the above permutation example is *not* a dearrangement since $2$ maps to $2$, but the permutation resulting in mapping every number $i$ to $i+1$ mod $5$ is:

$$
\begin{array}{|c|c|}
\hline
x & \pi'(x) \\
\hline
1 & 2 \\
2 & 3 \\
3 & 4 \\
4 & 5 \\
5 & 1 \\
\hline
\end{array}
$$

Great, now that we've formally defined both permutations and dearrangements, we can ask our simple question:

**What is the probability of a permutation being a dearrangement?**

We will study permutation/dearrangements of sets with cardinality $n$, namely functions on the set $[n]$. Therefore, let's define $D_n$ as the number of dearrangements of $[n]$. Our probability is $D_n$ divided by the total number of permutations. The total number of permutations is easily seen to be $n!$, since for the first element, we have $n$ choices for its mapping, then $n-1$ for the next, then $n-2$, and so on, until the last number has exactly one possible mapping. By the multiplication principle, this gives us $n!$ total permutations, so our probability is the quantity 

$$P(dearrangement) = \frac{D_n}{n!}$$

How can we now calculate $D_n$? Through the Principle of Inclusion/Exclusion (PIE)!

## Principle of Inclusion/Exclusion

This is one of the most important topics we covered in combinatorics, just because it enables you to solve so many new (and old) combinatorics problems. The general gist is you decompose the set you are trying to find, say $S$, into either the union of a bunch of (non disjoint) set, ie

$$|S| = |A_1 \cup A_2 \cup \dots \cup A_n|$$

or the set complement version of this (which we will use for this problem):

$$|S| = |A_1^c \cap A_2^c \cap \dots \cap A_n^c|$$

The Principle of Inclusion/Exclusion then states that

$$|A_1 \cup A_2 \cup \dots \cup A_n| = |A_1| + |A_2| + \dots |A_n| \quad - \quad |A_1 \cap A_2| - \dots |A_i \cap A_j| \quad  + \quad |A_i \cap A_j \cap A_k| \dots$$

Slightly more formally,

$$|A_1 \cup \dots A_n| = \sum_{i=1}^{n}{|A_i|} - \sum_{i, j}^{n}{|A_i \cap A_j|} + \sum_{i, j, k}^{n}{|A_i \cap A_j \cap A_k|} \dots  + (-1)^{n+1} |A_1 \cap A_2 \dots \cap A_n|$$

Essentially, the cardinality of the union of a bunch of sets is the sum of each of their individual cardinalities, minus the overlaps you are overcounting, then adding back the extra you took out, then minus more overlap, and so on until your set intersect terms are all $0$.

The set complement version (everything in the universe of $S$ that is NOT in any of $A_i$) is then:

$$|S \setminus (A_1 \cup A_2 \dots \cup A_n)| = |A_1^c \cap A_2^c \cap \dots \cap A_n^c| = |S| - |A_1| - |A_2| - \dots |A_n| \quad + \quad |A_1 \cap A_2| + \dots |A_i \cap A_j| \quad  - \quad |A_i \cap A_j \cap A_k| \dots$$

*Note:* The proof of PIE involves seeing how much each element of S contributes to the LHS and RHS of the set-complement version of PIE. You case on if $x \in S$ is in $m$ of the sets $A_1, A_2, \dots A_n$, where if $m=0$, you contribute 1 to both sides, and if $m > 0$ you contribute 0 to both sides.

THe power of PIE lies in simplifying challenging combinatorics problems into choosing the right sets $A_i$ to apply PIE to count your set $S$. That's exactly what we will now do.

## Solving the Problem

Let's reformulate our set $D_n$ into the set difference of our universe (all permutations) and a bunch of forbidden sets $A_i$ (this is exactly set complement PIE).

So $S$ is the set of all permutations, and we already know $|S| = n!$

What are our $A_i$'s? What must dearrangements not have? An element that maps to itself! So if we have $n$ elements, we can have:

$$A_i = \{\pi \in S \ | \ \pi(i) = i \} \quad \forall 1 \le i \le n$$

This line is extremely important, so make sure you understand it.

Because then $D_n$ is all the elements in S that don't fall in any single $A_i$ or...

$$|D_n| = |S \setminus (A_1 \cup A_2 \dots \cup A_n)|$$

See how we can apply PIE now!

$$|D_n| = |S| - |A_1| - |A_2| - \dots |A_n| \quad + \quad |A_1 \cap A_2| + \dots |A_i \cap A_j| \quad  - \quad |A_i \cap A_j \cap A_k| \dots$$

Now we just have to find the cardinalities of our sets containing $A_i$'s. For all $|A_1|, |A_2|, \dots |A_n|$ we have exactly one element with a pre-determined mapping, so going through $n-1$ undetermined elements, we have a total number of $(n-1)!$ permutations. Applying the same logic to $|A_i \cap A_j|$, we have two predetermined elements, giving us $(n-2)!$ permutations. This continues down to $|A_1 \cap A_2 \dots \cap A_n|$ where every element is determined, so you only have one mapping, the identity permutation. 

The next question is how many sets do we have with $1$ $A_i$ in them, $2$ $A_i$'s (intersected together), $k$ $A_i$'s, etc. This can easily be seen to be $n\choose k$ since this is how many ways we can chose $k$ of the $n$ $A_i$'s

Plugging in our set cardinalities, as well as how many times we get each set size (in terms of how many $A_i$'s make up that term), we get:

$$D_n = n! - \binom{n}{1}(n-1)! + \binom{n}{2}(n-2)! - \cdots + (-1)^{n} \binom{n}{n} 0!$$

$$D_n = n! - \frac{n!}{(n-1)!1!}(n-1)! + \frac{n!}{(n-2)!2!}(n-2)! - \frac{n!}{(n-3)!3!}(n-3)! + \dots$$

$$D_n = n! - \frac{n!}{1!} + \frac{n!}{2!} - \frac{n!}{3!} + \dots$$

Remember we are trying to find $P(dearrangement) = \frac{D_n}{n!}$ so:

$$P(dearrangement) = 1 - \frac{1}{1!} + \frac{1}{2!} - \frac{1}{3!} + \dots$$

This looks vaguely familiar. The factorials in the denominators of each term reminds me of the taylor expansion of $e^x \approx 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \dots$

And if we plug in $-1$ we get:

$$1 - \frac{1}{1!} + \frac{1}{2!} - \frac{1}{3!} + \dots$$

Exactly $P(dearrangement)!!$

$$\boxed{P(dearrangement) = e^{-1}}$$

This is absolutely absurd if you think about it. Using the Principal of Inclusion/Exclusion, we were able to find a sequence that represented the probability of a dearrangement occuring, and this sequence happens to be the Taylor expansion of $e^x$ at -1, implying that as $n$ approaches infinity, the probability of a dearrangement occuring is somehow $\frac{1}{e}$!?!?! How $e$ of all numbers naturally shows up in this probability is still crazy to me, and that's why this was my favorite thing I learned from Combo! (Shoutout Prof Yong, Jen, and Srihari)

$$\square$$