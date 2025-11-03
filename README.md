# A/B Testing Simulation: A Deep Dive into Statistical Power

### The Goal

Ever launched an A/B test where you *knew* the new version was better, but the results came back "inconclusive"?

This project digs into *why* that happens. I built a complete A/B test simulation from scratch to explore the statistics that drive a successful test. My goal was to move beyond just using a library and instead understand the *exact* relationship between **sample size** (how many users) and **statistical power** (our ability to detect a real winner).

---

### Key Findings & Business Impact

My simulation centered on a realistic scenario: **Version A** has a 20% conversion rate, and **Version B** has a 22% rate. Here's what I found.

**(Here's where you'll put your plot. Just replace the line below with `![Statistical Power vs Sample Size Plot](plot.png)` after you've saved a screenshot of your graph as `plot.png` in your folder.)**
<img width="855" height="547" alt="image" src="https://github.com/user-attachments/assets/5c9b434a-9342-41bb-a6b1-074c52efe1f6" />

### ****

1.  **Finding 1: Small Tests are Unreliable.** The plot shows that with a small sample (e.g., under 1,500 users), our statistical power is low. This means we have a high chance of *failing to detect the 2% improvement*, even though it's real. A business acting on this would wrongly conclude the new feature isn't worth it.

2.  **Finding 2: Power Shows You What's "Good Enough".** The "elbow" of the curve shows exactly how many users we need to be confident. This simulation proves *why* we must calculate sample size *before* a test—it stops us from wasting time and resources.

3.  **Finding 3: Bayesian Methods are More Intuitive.** The traditional z-test gives a p-value, which is hard to explain. My Bayesian simulation (using the Beta distribution) answered a much clearer question: **"What's the *probability* that B is actually better than A?"** This is a metric you can take directly to a product manager to make a decision.

---

### How It Works: The Technical Details

Here is the process I followed in the notebook:

* **1. Synthetic Data Generation:** Used `np.random.binomial` to simulate user clicks for Version A (20% conversion) and Version B (22% conversion) over various sample sizes.

* **2. Built a Frequentist Test from Scratch:** I coded a `two_z_test` function that calculates the z-score and p-value for a two-proportion test, replicating the logic of standard testing libraries.

* **3. Simulated for Statistical Power:** I ran the `two_z_test` function 5,000 times for *each* sample size (from 200 to 5,000 users). The "Power" (y-axis) is the percentage of those 5,000 tests that correctly rejected the null hypothesis (i.e., they "found" the 2% lift).

* **4. Calculated Required Sample Size:** I also implemented the formula to calculate the *exact* sample size needed to achieve a standard 80% power, proving the results of the simulation.

* **5. Implemented a Bayesian Approach:** As an alternative, I used `np.random.beta` to model the posterior distributions for A and B. This allowed me to calculate `P(B > A)` directly.

---

### How to Use This Project

1.  Clone this repository.
2.  Open the `a_b_testing.ipynb` file in Jupyter Lab, VS Code, or Google Colab.
3.  Run the cells from top to bottom to see all the simulations and generate the plot.
4.  You can easily change the conversion rates (`pa` and `pb`) at the top of the notebook to see how a smaller or larger difference would impact the results!

### Technologies Used

* Python
* NumPy
* Pandas
* Matplotlib
* SciPy
