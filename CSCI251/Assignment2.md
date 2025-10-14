Student id: 8199644
Student name: Long Vu Nguyen
# CSCI251 Assignment 2 Report
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
- Stances are stored in the `Stance` struct with two members: `significance` and `strength`
- Both leaders and electoral divisions maintain a `std::map` to store their position on each of the five issues
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
- Significance: (0, 1.0]
- Strength: (0, 1.0]

**Implementation Details:**
- Leader popularity is initialized using values between `(0.5-0.9)`
- For each of the five issues, both stance dimensions are randomly sampled, which generates values uniformly between 0.01 and 1.0 
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
- **Range:** \[0.5, 1.5] million
- **Implementation:**  samples uniformly from \[0.5, 1.5] 

**Stances:**
- **Distribution:** Uniform random distribution for both dimensions
- **Sampling Range:**
  - Significance: (0, 1.0]
  - Strength: (0, 1.0]
- **Implementation:** Each division receives randomized stances on all five issues
#### Initialization Process
The number of active divisions is determined by the command-line parameter `n` (1-10 inclusive). For each active division:
1. A name is selected from the predefined list
2. Population is randomly sampled from \[0.5, 1.5]
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

2. **Leader Stance Shift Event** (Probability: 0.2)
   - **Type:** Leader-related
   - **Effect:** Modifies leader stances on a randomly selected issue

3. **Division Stance Shift Event** (Probability: 0.2)
   - **Type:** Issue-related
   - **Effect:** Alters the division's stance on a randomly selected issue

4. **Population Change Event** (Probability: 0.2)
   - **Type:** Issue-related
   - **Effect:** Adjusts the division's population

#### Event Execution Rules
**1. Popularity Change Event**
- **Target:** All party leaders in the affected division
- **Modification:** Each leader's popularity changes by a random amount in \[-0.1, 0.1]
- **Bounds Enforcement:** Resulting popularity clamped to (0, 1] range

**2. Leader Stance Shift Event**
- **Target:** All party leaders' stance on one randomly selected issue
- **Modification:**
  - Significance changes by random amount in \[-0.1, 0.1]
  - Strength changes by random amount in \[-0.1, 0.1]
- **Issue Selection:** Random index between 0 and 4
- **Bounds Enforcement:** Both dimensions clamped to (0, 1] range

**3. Division Stance Shift Event**
- **Target:** The division's stance on one randomly selected issue
- **Modification:**
  - Significance changes by random amount in \[-0.15, 0.15]
  - Strength changes by random amount in \[-0.15, 0.15]
- **Issue Selection:** Random index between 0 and 4
- **Bounds Enforcement:** Both dimensions clamped to (0, 1] range
- 
**4. Population Change Event**
- **Target:** The division's population
- **Modification:** Population changes by random amount in \[-0.2, 0.2]
- **Bounds Enforcement:** Resulting population clamped to \[0.5, 1.5] range

---

### 1.5 Election Day
#### Voting Score Calculation
The voting score for each leader in each division is calculated using a weighted formula combining two factors:
**Formula:**
```
Score = A × (Stance-and-Population Factor) + B × (Leader Popularity)
```
#### Coefficient Values
- **A (Stance-and-Population weight):** 0.7
- **B (Popularity weight):** 0.3
#### Stance-and-Population Factor Calculation
**Step 1: Calculate Cosine Similarity for Each Issue**
For each of the five issues, compute the cosine similarity between the leader's stance and the division's stance:


$$\text{Cosine Similarity} =\frac{ x_{1}y_{1}+x_{2}y_{2}}{\sqrt{ x_{1}^2+x_{2}^2 }\times\sqrt{ y_{1}^2 +y_{2}^2 }}$$


Where:
- (x₁, x₂) = leader's stance (significance, strength)
- (y₁, y₂) = division's stance (significance, strength)

**Step 2: Calculate Average Cosine Similarity**
```
Average Cosine = (Sum of 5 cosine similarities) / 5
```

**Step 3: Multiply by Population**
```
Stance-and-Population Factor = Average Cosine × Population
```
---

## Section 2: UML Class Diagram
![[uml.bmp]]