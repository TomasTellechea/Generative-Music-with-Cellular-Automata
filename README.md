### Generative Music with Cellular Automata

CA is a computational model that consists of a "grid" of cells. Each cell can be in one of several possible states (e.g., on or off).

**Initial States:**
An initial state is defined for the cells in the grid. This can be a random pattern or a specific configuration.

**Evolution Rules:**
Rules are established that determine how each cell's state changes based on the state of its neighboring cells. The rules are local, meaning each cell only "cares" about the state of its immediate neighbors.

**Temporal Evolution:**
The system updates in discrete time steps. In each step, all cells update simultaneously according to the evolution rules.

### CA Experiment

In this experiment, I use the Mixolydian mode in C for an ensemble consisting of flute, clarinet, bassoon, trumpet, trombone, piano, vibraphone, and strings.

**Evolution Rules:**
The evolution rules in this code are implemented within the class "CellularAutomatonNoteGenerator" and are applied at each step to update the state of the notes. There are two main rules: the "filling gaps" rule and the "mutation" rule.

1. **Filling Gaps Rule (_apply_filling_gaps_rule)**
   - **Purpose:** To activate notes in positions where there are two consecutive rests.
   - **Process:**
     - For each position in the pattern:
       - The previous and next positions are obtained, considering the pattern as circular.
       - For each note in the diatonic scale:
         - If the note is off (OFF) in the previous and current positions:
           - The note is turned on (ON) in the next position.
     - **Example:**
       - If the note C is off (OFF) at positions 3 and 4, it will be turned on (ON) at position 5.

2. **Mutation Rule (_apply_mutation_rule)**
   - **Purpose:** To introduce variability by changing active notes to a mutation state and vice versa.
   - **Process:**
     - For each position in the pattern:
       - For each note in the diatonic scale:
         - If the note is active (ON) and a random probability (MUTATION_PROBABILITY) is met:
           - The note changes to a mutation state (MUTATE).
         - If the note is in a mutation state (MUTATE) and a random probability (MUTATION_TRANSITION_PROBABILITY) is met:
           - The note changes to an active state (ON).
     - **Example:**
       - An active note C (ON) can change to a mutation state (MUTATE) with a 10% probability.
       - A note C in a mutation state (MUTATE) can change to an active state (ON) with a 50% probability.

### Musical Mapping

Applying this method to music, I have created various mappings.
- For the high strings and cello, the code is the simplest, with a single note and a single rhythmic figure representing the activated (note) or deactivated (rest) states of the matrix.
- For the other instruments, a new state called "MUTATE" is added to interact with other notes in the Mixolydian scale.
- For the clarinet, trumpet, and the right hand of the piano (one of the matrices), the rhythmic figure remains fixed, but for the other instruments, the interaction of various rhythmic figures is explored. These modifications are made through transition probabilities that were adjusted in the various matrices created.
