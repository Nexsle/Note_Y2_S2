# CSCI251 Assignment 2 Report
**Student Name:** [Your Name]
**Student Number:** [Your Student Number]

---

## Section 1: Component Implementation Details

### 1.1 Issues and Stances

#### National Issues
The simulation models five critical national issues that impact electoral divisions and party platforms:

1. **Climate Change**
   - Description: "Addressing global warming..."
   - Importance: Environmental sustainability is crucial for the nation's long-term future and affects multiple sectors including agriculture, infrastructure, and public health.

2. **Healthcare**
   - Description: "Ensuring healthcare access..."
   - Importance: Universal access to quality healthcare is fundamental to citizen wellbeing and economic productivity.

3. **Education**
   - Description: "Improving education quality..."
   - Importance: A well-educated population is essential for economic development, innovation, and social mobility.

4. **Economy**
   - Description: "Managing economic growth..."
   - Importance: Economic stability and growth determine employment rates, living standards, and national prosperity.

5. **Infrastructure**
   - Description: "Developing public facilities..."
   - Importance: Modern infrastructure supports economic activity, connectivity, and quality of life for all citizens.

#### Stance Modeling
Each stance is modeled as a two-dimensional vector using the `Stance` struct:
- **First element (significance)**: A real number in the range (0, 1] representing how important the issue is perceived to be
- **Second element (strength)**: A real number in the range (0, 1] representing the intensity of proposed measures to address the issue

**Implementation Details:**
- Stances are stored in the `Stance` struct with two `double` members: `significance` and `strength`
- Both leaders and electoral divisions maintain a `std::map<std::string, Stance>` to store their position on each of the five issues
- The two-dimensional nature of stances allows for nuanced policy positions (e.g., high significance but low strength indicates recognition of importance without aggressive action)

---

### 1.2 Political Parties

#### Party Characteristics
The simulation features three political parties, each with a leader:

1. **Progressive Alliance** - Leader: Alice Johnson
2. **Conservative Union** - Leader: Bob Smith
3. **Liberty Party** - Leader: Carol Davis

#### Leader Attributes
Each party leader has:
- **Popularity**: A value between (0, 1] representing public approval
- **Stances**: Positions on all five national issues

#### Stance Initialization
**Distribution:** Uniform random distribution
**Sampling Range:**
- Significance: (0.01, 1.0]
- Strength: (0.01, 1.0]

**Implementation Details:**
- Leader popularity is initialized using `random.GetDouble(0.5, 0.9)`, giving all leaders a moderately favorable starting approval rating (Campain.cpp:28)
- For each of the five issues, both stance dimensions are randomly sampled using `random.GetStance()`, which generates values uniformly between 0.01 and 1.0 (Random.h:18-19)
- This randomization ensures each simulation run produces different initial political landscapes
- The minimum value of 0.01 prevents division-by-zero errors in cosine similarity calculations

---

### 1.3 Electoral Divisions

#### Division Names
The simulation supports up to 10 electoral divisions with the following names:
1. Northern District
2. Central Valley
3. Coastal Region
4. Mountain Region
5. Southern Plains
6. Eastern Shore
7. Western Highlands
8. Midlands
9. Capital District
10. Rural Heartland

#### Division Attributes

**Population:**
- **Distribution:** Uniform random distribution
- **Range:** [0.5, 1.5] million
- **Implementation:** `random.GetPopulation()` samples uniformly from [0.5, 1.5] (Random.h:26-28)

**Stances:**
- **Distribution:** Uniform random distribution for both dimensions
- **Sampling Range:**
  - Significance: (0.01, 1.0]
  - Strength: (0.01, 1.0]
- **Implementation:** Each division receives randomized stances on all five issues using `random.GetStance()` (Campain.cpp:52-53)

#### Initialization Process
The number of active divisions is determined by the command-line parameter `n` (1-10 inclusive). For each active division:
1. A name is selected from the predefined list (Campain.h:23-34)
2. Population is randomly sampled from [0.5, 1.5]
3. Five stances (one per issue) are randomly initialized
4. All attributes may be modified during campaign event days

---

### 1.4 Campaign Event Days

#### Event System Overview
The campaign features a probabilistic event system where each electoral division has a 0.8 probability of experiencing exactly one event per campaign day.

#### Event Types and Probabilities
Four event types exist, each with equal probability of 0.2 (totaling 0.8):

1. **Popularity Change Event** (Probability: 0.2)
   - **Type:** Leader-related
   - **Effect:** Adjusts leader popularity for all three party leaders
   - **Implementation:** Events.cpp:19-45

2. **Leader Stance Shift Event** (Probability: 0.2)
   - **Type:** Leader-related
   - **Effect:** Modifies leader stances on a randomly selected issue
   - **Implementation:** Events.cpp:48-79

3. **Division Stance Shift Event** (Probability: 0.2)
   - **Type:** Issue-related
   - **Effect:** Alters the division's stance on a randomly selected issue
   - **Implementation:** Events.cpp:106-132

4. **Population Change Event** (Probability: 0.2)
   - **Type:** Issue-related
   - **Effect:** Adjusts the division's population
   - **Implementation:** Events.cpp:81-104

#### Event Execution Rules

**1. Popularity Change Event**
- **Target:** All party leaders in the affected division
- **Modification:** Each leader's popularity changes by a random amount in [-0.1, 0.1]
- **Bounds Enforcement:** Resulting popularity clamped to (0, 1] range (Party.cpp:16-24)
- **Uncertainty:** The random change ensures different outcomes on each execution

**2. Leader Stance Shift Event**
- **Target:** All party leaders' stance on one randomly selected issue
- **Modification:**
  - Significance changes by random amount in [-0.1, 0.1]
  - Strength changes by random amount in [-0.1, 0.1]
- **Issue Selection:** Random index between 0 and 4 (Events.cpp:54-55)
- **Bounds Enforcement:** Both dimensions clamped to (0, 1] range (Party.cpp:38-54)
- **Uncertainty:** Random changes and random issue selection create variability

**3. Division Stance Shift Event**
- **Target:** The division's stance on one randomly selected issue
- **Modification:**
  - Significance changes by random amount in [-0.15, 0.15]
  - Strength changes by random amount in [-0.15, 0.15]
- **Issue Selection:** Random index between 0 and 4 (Events.cpp:112-113)
- **Bounds Enforcement:** Both dimensions clamped to (0, 1] range (Division.cpp:42-58)
- **Uncertainty:** Larger range (±0.15) than leader events reflects greater volatility in public opinion

**4. Population Change Event**
- **Target:** The division's population
- **Modification:** Population changes by random amount in [-0.2, 0.2]
- **Bounds Enforcement:** Resulting population clamped to [0.5, 1.5] range (Division.cpp:23-30)
- **Uncertainty:** Random change ensures demographic variations between simulation runs

#### Event Selection Mechanism
For each division on each event day:
1. Generate random number `roll` uniformly from [0, 1]
2. Calculate cumulative probability across events
3. Execute first event where `cumulative probability > roll`
4. If `roll > 0.8`, no event occurs (20% chance)
5. Implementation in Campain.cpp:87-106

This approach ensures:
- Exactly one event per division (if any)
- Equal 0.2 probability for each event type
- 0.2 probability of no event
- Different event patterns each simulation run

---

### 1.5 Election Day

#### Voting Score Calculation

The voting score for each leader in each division is calculated using a weighted formula combining two factors:

**Formula:**
```
Score = A × (Stance-and-Population Factor) + B × (Leader Popularity)
```

#### Coefficient Values
- **A (Stance-and-Population weight):** 0.4
- **B (Popularity weight):** 0.6
- **Constraint:** A + B = 1, and A > B (violated in implementation - see note below)
- **Implementation:** Campain.h:20-21

**Note:** The current implementation uses A=0.4 and B=0.6, but the specification requires A > B. The intended design prioritizes stance alignment with the electorate over pure popularity, but the implementation reverses this. For specification compliance, values like A=0.6, B=0.4 would be more appropriate.

#### Stance-and-Population Factor Calculation

**Step 1: Calculate Cosine Similarity for Each Issue**

For each of the five issues, compute the cosine similarity between the leader's stance and the division's stance:

```
Cosine Similarity = (x₁·y₁ + x₂·y₂) / (√(x₁² + x₂²) · √(y₁² + y₂²))
```

Where:
- (x₁, x₂) = leader's stance (significance, strength)
- (y₁, y₂) = division's stance (significance, strength)

**Implementation:** Campain.cpp:288-306

**Step 2: Calculate Average Cosine Similarity**
```
Average Cosine = (Sum of 5 cosine similarities) / 5
```

**Step 3: Multiply by Population**
```
Stance-and-Population Factor = Average Cosine × Population
```

Where Population is the division's population value from [0.5, 1.5]

**Complete Calculation:** Campain.cpp:268-286

#### Winner Determination

**Division Level:**
- For each division, calculate scores for all three leaders
- Leader with highest score wins that division
- Ties: First party in iteration order wins (implementation detail)

**National Level:**
- Count divisions won by each party
- Party with most division wins forms government
- If multiple parties tie for most wins: Hung parliament declared

**Implementation:** Campain.cpp:171-266

---

## Section 2: UML Class Diagram

```
┌─────────────────────────────────┐
│          <<struct>>             │
│            Issue                │
├─────────────────────────────────┤
│ + issueName: std::string        │
│ + description: std::string      │
├─────────────────────────────────┤
│ + Issue(name, desc)             │
└─────────────────────────────────┘


┌─────────────────────────────────┐
│          <<struct>>             │
│            Stance               │
├─────────────────────────────────┤
│ + significance: double          │
│ + strength: double              │
├─────────────────────────────────┤
│ + Stance(sig, str)              │
└─────────────────────────────────┘


┌─────────────────────────────────────┐
│              Random                 │
├─────────────────────────────────────┤
│ - rd: std::random_device            │
│ - gen: std::mt19937                 │
├─────────────────────────────────────┤
│ + Random()                          │
│ + GetDouble(min, max): double       │
│ + GetStance(): Stance               │
│ + GetPopularity(): double           │
│ + GetPopulation(): double           │
│ + EventOccurs(prob): bool           │
└─────────────────────────────────────┘


┌──────────────────────────────────────────┐
│                Party                     │
├──────────────────────────────────────────┤
│ - name: std::string                      │
│ - popularity: double                     │
│ - leader: std::string                    │
│ - stances: map<string, Stance>           │
├──────────────────────────────────────────┤
│ + Party(name, leader)                    │
│ + SetStance(issue, stance): void         │
│ + GetStance(issue): Stance               │
│ + AdjustStance(issue, sig, str): void    │
│ + GetPopularity(): double                │
│ + SetPopularity(pop): void               │
│ + GetName(): std::string                 │
│ + GetLeader(): std::string               │
└──────────────────────────────────────────┘


┌──────────────────────────────────────────┐
│              Division                    │
├──────────────────────────────────────────┤
│ - name: std::string                      │
│ - population: double                     │
│ - stances: map<string, Stance>           │
├──────────────────────────────────────────┤
│ + Division(name, pop)                    │
│ + SetStance(issue, stance): void         │
│ + GetStance(issue): Stance               │
│ + GetName(): std::string                 │
│ + GetPopulation(): double                │
│ + AdjustPopulation(change): void         │
│ + AdjustStance(issue, sig, str): void    │
└──────────────────────────────────────────┘


┌──────────────────────────────────────────────────────┐
│           <<abstract>>                               │
│               Event                                  │
├──────────────────────────────────────────────────────┤
│ # name: std::string                                  │
│ # probability: double                                │
│ # random: Random*                                    │
├──────────────────────────────────────────────────────┤
│ + Event(name, prob, random)                          │
│ + GetProbability(): double                           │
│ + GetName(): std::string                             │
│ + Execute(div, parties, issues): void = 0            │
└──────────────────────────────────────────────────────┘
                         △
                         │
         ┌───────────────┼───────────────┬─────────────┐
         │               │               │             │
┌────────────────┐ ┌─────────────┐ ┌────────────┐ ┌──────────────┐
│ Popularity     │ │   Leader    │ │ Population │ │   Division   │
│     Event      │ │   Stance    │ │   Event    │ │   Stance     │
│                │ │   Event     │ │            │ │   Event      │
├────────────────┤ ├─────────────┤ ├────────────┤ ├──────────────┤
│ + Popularity   │ │ + Leader    │ │ + Popula   │ │ + Division   │
│   Event(r)     │ │   Stance    │ │   tion     │ │   Stance     │
│                │ │   Event(r)  │ │   Event(r) │ │   Event(r)   │
│ + Execute(...) │ │ + Execute   │ │ + Execute  │ │ + Execute    │
│   : void       │ │   (...):    │ │   (...):   │ │   (...):     │
│                │ │   void      │ │   void     │ │   void       │
└────────────────┘ └─────────────┘ └────────────┘ └──────────────┘


┌───────────────────────────────────────────────────────┐
│                   Campain                             │
├───────────────────────────────────────────────────────┤
│ - issues: vector<Issue>                               │
│ - parties: vector<Party>                              │
│ - divisions: vector<Division>                         │
│ - events: vector<Event*>                              │
│ - random: Random                                      │
│ - numberOfDivision: int                               │
│ - numberOfDays: int                                   │
│ - coeffA: double                                      │
│ - coeffB: double                                      │
│ - DIVISION_NAMES: vector<string>                      │
│ - PARTY_INFO: vector<pair<string, string>>            │
├───────────────────────────────────────────────────────┤
│ - InitializeIssue(): void                             │
│ - InitializeParty(): void                             │
│ - InitializeDivision(): void                          │
│ - InitializeEvent(): void                             │
├───────────────────────────────────────────────────────┤
│ + Campain(numDiv, numDays)                            │
│ + DisplayIssues(): void                               │
│ + DisplayInitialState(): void                         │
│ + DisplayPartyReport(): void                          │
│ + DisplayNationalReport(): void                       │
│ + RunCampain(): void                                  │
│ + RunEventDay(dayNum): void                           │
│ + RunElectionDay(): void                              │
│ + DisplayWinner(wins): void                           │
│ + CalculateScore(party, div): double                  │
│ + CalculateCosineSimilarity(s1, s2): double           │
└───────────────────────────────────────────────────────┘


Relationships:
═════════════

Campain ◇────── Issue           (composition, 1 to 5)
Campain ◇────── Party           (composition, 1 to 3)
Campain ◇────── Division        (composition, 1 to 10)
Campain ◇────── Event*          (composition, 1 to 4)
Campain ◆────── Random          (composition, 1 to 1)

Party   ◆────── Stance          (composition, 1 to 5)
Division ◆───── Stance          (composition, 1 to 5)

Event   ────▷   Random          (dependency/association)
Event   ────▷   Division        (dependency - parameter)
Event   ────▷   Party           (dependency - parameter)
Event   ────▷   Issue           (dependency - parameter)

PopularityEvent      ──────|>  Event  (inheritance)
LeaderStanceEvent    ──────|>  Event  (inheritance)
PopulationEvent      ──────|>  Event  (inheritance)
DivisionStanceEvent  ──────|>  Event  (inheritance)
```

### Class Diagram Explanation

**Core Classes:**

1. **Campain** (Note: spelled "Campain" in code, should be "Campaign")
   - Central orchestrator class managing the entire simulation
   - Contains collections of all major entities (issues, parties, divisions, events)
   - Implements the main workflow: initialization → event days → election day

2. **Party**
   - Represents a political party with a leader
   - Maintains popularity rating and stances on all issues
   - Provides methods to adjust attributes during campaign events

3. **Division**
   - Represents an electoral division
   - Maintains population and stances on all issues
   - Provides methods to adjust attributes during campaign events

4. **Event** (Abstract Base Class)
   - Defines interface for all event types
   - Pure virtual `Execute()` method implemented by derived classes
   - Four concrete event classes inherit from Event

**Supporting Structures:**

5. **Issue** - Simple struct holding issue name and description
6. **Stance** - Simple struct with two doubles (significance, strength)
7. **Random** - Utility class encapsulating random number generation

**Design Patterns:**

- **Strategy Pattern**: Event hierarchy with polymorphic Execute() method
- **Composition**: Campain class contains aggregations of all major components
- **Encapsulation**: Private data members with public getter/setter methods
- **Template Method**: Event base class defines structure, subclasses implement specifics

---

## Additional Notes

### Code Organization
The implementation follows object-oriented principles with:
- Separate header (.h) and implementation (.cpp) files
- Proper encapsulation of data members
- Clear separation of concerns across classes
- No standalone functions (all functionality wrapped in classes)

### Compilation
The program compiles as executable `APE` and runs with:
```
./APE n m
```
Where `n` = number of divisions (1-10) and `m` = number of campaign days (1-30)

### Known Issues
1. Coefficient A=0.4 < B=0.6 violates specification requirement (A > B)
2. Typo: "Campain" instead of "Campaign" throughout codebase
3. Error message on line 22 of main.cpp says "Division count invalid" when it should say "Day count invalid"

