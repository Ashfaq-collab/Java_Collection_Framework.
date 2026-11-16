# Quantitative Aptitude – Complete Notes

## Topics Covered
1. Average
2. Profit and Loss
3. Simple Interest (SI)
4. Compound Interest (CI)
5. Time, Speed and Distance

---

# 1. AVERAGE

## Formula

Average = Sum of all values / Total number of values

### Example

Find the average of 10, 20, 30, 40 and 50.

Sum = 10 + 20 + 30 + 40 + 50 = 150

Total numbers = 5

Average = 150 / 5 = **30**

### Java Program

```java
int sum = 10 + 20 + 30 + 40 + 50;
int count = 5;

double average = (double) sum / count;

System.out.println(average); // 30.0
```

---

# 2. PROFIT AND LOSS

## Basic Terms

- **Cost Price (CP):** Price at which an item is purchased.
- **Selling Price (SP):** Price at which an item is sold.
- **Profit:** When SP > CP.
- **Loss:** When CP > SP.
- **Marked Price (MP):** Price displayed on the product.
- **Discount:** Reduction in marked price.

## Basic Formulas

Profit = SP - CP

Loss = CP - SP

Profit Percentage = (Profit / CP) × 100

Loss Percentage = (Loss / CP) × 100

## Selling Price Formulas

When profit percentage is given:

SP = CP × (100 + Profit%) / 100

When loss percentage is given:

SP = CP × (100 - Loss%) / 100

## Cost Price Formulas

When profit percentage is given:

CP = SP × 100 / (100 + Profit%)

When loss percentage is given:

CP = SP × 100 / (100 - Loss%)

## Discount Formulas

Discount = MP - SP

Discount Percentage = (Discount / MP) × 100

Selling Price = MP × (100 - Discount%) / 100

## Successive Discount

Equivalent Discount = a + b - (a × b / 100)

Example:

Two successive discounts of 20% and 10%.

D = 20 + 10 - (20 × 10 / 100)

D = 30 - 2 = **28%**

## Important Shortcut Formulas

1. Profit x%:

   SP : CP = (100 + x) : 100

2. Loss x%:

   SP : CP = (100 - x) : 100

3. Two articles sold at the same selling price, one at x% profit and another at x% loss:

   Overall Loss% = x² / 100

4. Price increases by x% and then decreases by x%:

   Net Loss% = x² / 100

## Example

CP = ₹500, SP = ₹600

Profit = 600 - 500 = ₹100

Profit% = (100 / 500) × 100

**Answer = 20% Profit**

---

# 3. SIMPLE INTEREST (SI)

Simple Interest is calculated only on the original principal amount.

## Basic Terms

- P = Principal
- R = Rate of interest per annum
- T = Time in years
- SI = Simple Interest
- A = Final Amount

## Important Formulas

### 1. Simple Interest

SI = (P × R × T) / 100

### 2. Amount

A = P + SI

### 3. Principal

P = (SI × 100) / (R × T)

### 4. Rate

R = (SI × 100) / (P × T)

### 5. Time

T = (SI × 100) / (P × R)

## Example

Principal = ₹5,000

Rate = 10%

Time = 2 years

SI = (5000 × 10 × 2) / 100

SI = ₹1,000

Amount = 5000 + 1000

**Answer = ₹6,000**

---

# 4. COMPOUND INTEREST (CI)

Compound Interest is calculated on the principal amount as well as the accumulated interest.

## Important Formulas

### 1. Compound Amount

A = P × (1 + R/100)^T

### 2. Compound Interest

CI = A - P

Or,

CI = P × [(1 + R/100)^T - 1]

## Different Compounding Periods

### 1. Annually

A = P × (1 + R/100)^T

### 2. Half-yearly

A = P × (1 + R/200)^(2T)

### 3. Quarterly

A = P × (1 + R/400)^(4T)

## Different Rates for Different Years

A = P × (1 + R1/100) × (1 + R2/100)

For more years, continue multiplying the respective yearly factors.

## Important Shortcut Formulas

### 1. Difference Between CI and SI for 2 Years

CI - SI = P × (R/100)²

### 2. Difference Between CI and SI for 3 Years

CI - SI = P × (R/100)² × (3 + R/100)

### 3. CI for 2 Years

CI = P × [2R/100 + R²/10000]

### 4. CI for 3 Years

CI = P × [(1 + R/100)³ - 1]

### 5. Population Growth

Final Population = P × (1 + R/100)^T

### 6. Depreciation

Final Value = P × (1 - R/100)^T

## Example

Principal = ₹5,000

Rate = 10%

Time = 2 years

A = 5000 × (1 + 10/100)²

A = 5000 × 1.21

A = ₹6,050

CI = 6050 - 5000

**Answer = ₹1,050**

---

# 5. TIME, SPEED AND DISTANCE

## Basic Formulas

### 1. Speed

Speed = Distance / Time

### 2. Distance

Distance = Speed × Time

### 3. Time

Time = Distance / Speed

## Unit Conversions

| Conversion | Formula |
|---|---|
| km/hr to m/sec | Multiply by 5/18 |
| m/sec to km/hr | Multiply by 18/5 |
| km to metres | Multiply by 1000 |
| metres to km | Divide by 1000 |
| Hours to seconds | Multiply by 3600 |
| Seconds to hours | Divide by 3600 |

### Example 1

Convert 72 km/hr into m/sec.

72 × 5/18 = **20 m/sec**

### Example 2

Convert 15 m/sec into km/hr.

15 × 18/5 = **54 km/hr**

## Average Speed Formulas

### 1. Basic Average Speed

Average Speed = Total Distance / Total Time

### 2. Equal Distances at Two Different Speeds

Average Speed = (2 × x × y) / (x + y)

### 3. Equal Time at Two Different Speeds

Average Speed = (x + y) / 2

### 4. Three Equal Distances

Average Speed = (3 × x × y × z) / (xy + yz + zx)

## Relative Speed

| Situation | Formula |
|---|---|
| Opposite directions | x + y |
| Same direction | x - y |
| Meeting time (opposite) | Distance / (x + y) |
| Catching time (same) | Distance / (x - y) |

## Train Problems

| Situation | Formula |
|---|---|
| Train crossing a pole | Train Length / Speed |
| Train crossing a platform | (Train Length + Platform Length) / Speed |
| Two trains crossing in opposite directions | (L1 + L2) / (S1 + S2) |
| Two trains crossing in same direction | (L1 + L2) / (S1 - S2) |

**Important:** Convert speed into metres per second when train lengths are in metres.

## Boats and Streams

| Concept | Formula |
|---|---|
| Downstream Speed | Boat Speed + Stream Speed |
| Upstream Speed | Boat Speed - Stream Speed |
| Boat Speed | (Downstream + Upstream) / 2 |
| Stream Speed | (Downstream - Upstream) / 2 |

## Speed and Time Shortcut Formulas

### 1. Speed Increases by x%

New Time = Old Time × 100 / (100 + x)

### 2. Speed Decreases by x%

New Time = Old Time × 100 / (100 - x)

### 3. Time Reduction When Speed Increases by x%

Time Reduction% = [x / (100 + x)] × 100

### 4. Time Increase When Speed Decreases by x%

Time Increase% = [x / (100 - x)] × 100

---

# 6. QUICK FORMULA REVISION

| Topic | Important Formula |
|---|---|
| Average | Sum / Number of values |
| Profit | SP - CP |
| Loss | CP - SP |
| Profit % | (Profit / CP) × 100 |
| Loss % | (Loss / CP) × 100 |
| Discount | MP - SP |
| Successive Discount | a + b - ab/100 |
| Simple Interest | PRT/100 |
| SI Amount | P + SI |
| Compound Amount | P(1 + R/100)^T |
| Compound Interest | A - P |
| SI-CI Difference (2 years) | P(R/100)² |
| Speed | Distance / Time |
| Distance | Speed × Time |
| Time | Distance / Speed |
| Equal Distance Average Speed | 2xy/(x+y) |
| Relative Speed (Opposite) | x + y |
| Relative Speed (Same) | x - y |
| Downstream | B + S |
| Upstream | B - S |

---

# 7. PLACEMENT APTITUDE PREPARATION

Recommended order of study:

1. Average
2. Profit and Loss
3. Simple Interest
4. Compound Interest
5. Time, Speed and Distance
6. Problems on Trains
7. Boats and Streams
8. Time and Work
9. Pipes and Cisterns

## Preparation Tips

- Memorize the important formulas.
- Practise 20–30 questions daily.
- Start with easy problems.
- Gradually move to medium and difficult problems.
- Practise solving questions without looking at formulas.
- Revise mistakes regularly.

**Goal: Build strong quantitative aptitude skills for fresher placement and technical interviews.**
