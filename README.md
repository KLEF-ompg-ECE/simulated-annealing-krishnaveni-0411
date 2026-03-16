# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Krishnaveni Pola  
**Student ID    :** 2310040013  
**Date Submitted:** 16-03-2026  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
count_clashes() measures the number of clashes in the timetable. A clash occurs when a student has two exams assigned t same slot.
A perfect timetable has no clashes. (clashes = 0)
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
generate_neighbor() function creates a new "neighbor" timetable, which is a slightly modified version of the current one. It randomly selects one exam and moves it to a new, different, randomly selected time slot.
Helps us to explore different possible schedules.

```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to move to the newly generated timetable. If delta < 0, the new timetable is better (fewer clashes) and is always accepted. If it's worse, it is still accepted with a probability of math.exp(-delta / T). 
This occasional acceptance of worse solutions allows the algorithm to escape local optima and explore the search space instead of getting stuck.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed | 1379 |
| Clashes at iteration 1 | 12|
| Final best clashes | 3|
| Did SA reach 0 clashes? (Yes / No) | No |

**Copy the printed timetable output here:**
```
Final Timetable
------------------------------------------
  Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics
------------------------------------------
  Total clashes : 3
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The plot shows a steep drop in clashes during the initial iterations, with the most significant improvements happening very early on. The curve then flattens out for the latter part.
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        |     8         |      31              |       NO           |
| 0.95        |     3         |      135             |       NO           |
| 0.995       |     3         |      1379            |       NO           |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
When the cooling rate is fast (0.80), the temperature drops to the minimum almost immediately (31 iterations). This gives the algorithm very little time to explore, causing it to get stuck in a local minimum with a high number of clashes (8). 
Slower cooling rates (0.95 and 0.995) keep the temperature higher for longer, allowing for many more iterations (135 and 1379 respectively). This extended time allows the algorithm to escape local minima and find much better overall solutions.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
 Both 0.95 and 0.995 tied for the lowest clashes (3), but 0.95 could be considered best overall because it found the same quality solution much faster (135 iterations vs 1379)
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3 | Slow cooling allows for thorough exploration and a low-clash final schedule. |
| 2 — Cooling rate | cooling_rate = 0.95 | 3 | A moderately slow cooling rate finds the optimal solution much more efficiently than very slow cooling (0.995). |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
The most important thing I learned about Simulated Annealing is the critical role of the cooling rate in balancing exploration and efficiency. If the temperature drops too quickly, the algorithm gets trapped in a local minimum with poor results. However, if it drops too slowly, it wastes computational time.
```

---

## Submission Checklist

- [ ] Student name and ID filled in
- [ ] Q1, Q2, Q3 answered
- [ ] Experiment 1: table filled, timetable pasted, plot observation written
- [ ] Experiment 2: results table filled (3 rows), observation and answer written
- [ ] Summary table completed and reflection written
- [ ] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
