# N Queens
 N Queens problem with GA in python

A n*n grid with n queens placed on it in separate rows as follows:

No | 1 | 2 | 3 | 4 | 5
---|---|---|---|---|---
1 | - | Q | - | - | -
2 | - | - | - | - | Q
3 | - | - | Q | - | -
4 | Q | - | - | - | -
5 | - | - | - | Q | -

is represented as a one-dimensional array as: **[2, 5, 3, 1, 5]** 

Where the jth value represents in which column the queen is placed in jth row.

With this representation we are eliminating the possibility of placing two queens in a row. All such states would definitely not be the goal state.

**Goal State: 1Dimensional orientation of a n*n grid where no queens attack each other.**

Variables:
1. n: represents the size of the grid
2. pop_limit: represents size of population
3. generations: number of generations to compute, if stopping criterion is limited to this way
4. top_best: number of fittest survivors to select from population
5. random_offspring_lim: number of iterations after which a random population should be added to avoid a local optimal solution
6. queenpop: population set of chromosomes
7. queenspace: list of tuples with first element as the chromosome and second element as the fitness value of the chromosome.
8. mutation_probability: Probability with which mutation will occur in a child.
9. biasing_value: The value defines how much genes of a child will be biased toward a parent. Ranging from [1, biasing_value] the child will inherit 50% - 90% of a parent’s traits.


**Methodology:**
1. Gene(g): Position of a queen in a row. g∈[1,n]
2. Chromosome(c): 1 dimensional array representing the state of a n*n grid, as stated in assumptions.
3. Stop Criterion: a) Number of generations. b) Till goal state is reached
4. Duplicates: Absolutely no duplicates allowed.
5. Initial Population: A population limit of pop_limit is placed in queenpop and respective fitness values are computed and queenspace is finally populated.
6. Fitness Function: Total number of queens under attack is used as a fitness function. Value 0 is at goal states, a smaller value is more desirable.
7. Selection: Top top_best elements are chosen from a sorted (fitness value based) queenspace, and rest are discarded.
8. Crossover: Two random parents are selected from individuals that survived selection. Child will have crossed over genes from both these parents. Genes will be biased towards one parent or the other as described in biasing_value definition.
9. Mutation: With a chance of mutation_probability, the child can have a random gene mutated by a random value ranging from [0, n-1]



Value of n | Time taken to find solution (seconds) | Generations
---|---|---
4|0.00298|0
8|0.12294|5
16|0.97943|210
32|9.41359|891
64|53.85712671279907|1254

**Time Complexity:**
1. Fitness function computes number of clashing queens in O(n) time.
2. initialize(): takes O(n*pop_limit) time, i.e. quadratic One of the cost heavy function is initialize, which is called at the start and at random offspring generation. The function is computation heavy and generation halts at intervals of random offspring generation.

**Space Complexity:**
1. Fitness function requires O(n) storage.
2. genetic(): requires O(pop_limit) space at best. This is linear as well.
