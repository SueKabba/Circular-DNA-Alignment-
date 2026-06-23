# Computational Approach for Aligning Circular DNA Sequences

**Developed by:** Sue Kabba and Ashley Kubyako

**Course Project:** BNFO 301 Group Project

---

## 🧬 The Problem: Circular Breakpoints
Circular chromosomes (like those found in plasmids or bacteria) pose a unique challenge for traditional sequence alignment tools. Because they lack a fixed biological starting point, they are typically stored as linear strings by introducing an arbitrary breakpoint. 

When different researchers choose different breakpoints, homologous regions appear completely misaligned—even if the genetic sequences are identical. Standard global alignment algorithms (like Needleman-Wunsch) assume strict linear consistency and fail to account for these shifts.

## ⚙️ Our Solution: Two-Pass Rotation Search
To solve this, we developed a **rotation-based alignment approach** in Python. The algorithm fixes one sequence as a static reference and systematically rotates the second sequence using string slicing to simulate alternative breakpoints. 

To optimize performance and avoid slow brute-force calculations, we implemented a **Heuristic Two-Pass Strategy**:
1. **Coarse Search:** Rotates the sequence in larger increments to quickly isolate a promising alignment window.
2. **Fine Search:** Narrowly tests rotations one base pair at a time within that window to lock onto the optimal alignment.

Once the ideal rotation is identified, the final global alignment is confirmed.

---

## 🛠️ Code Architecture & Key Functions
The implementation is entirely modular and structured across four core Python functions:

| Function | Description | Merit|
| :--- | :--- | :--- |
| `needlemanWunsch(seq1, seq2)` | Implements global alignment via dynamic programming using a 2D scoring matrix. | Guarantees the absolute optimal linear global alignment given a scoring scheme. |
| `circularAlignment(seq1, seq2, ...)` | Handles circular breakpoint correction using the two-pass coarse/fine slicing strategy. | Efficiently identifies the optimal breakpoint alignment without testing every single rotation. |
| `progressiveMSA(sequences)` | Builds a Multiple Sequence Alignment progressively by aligning new sequences back to an evolving reference. | Simple and computationally efficient for handling multiple circular elements. |
| `printMSA(msa)` | Computes sequence identity percentage and outputs aligned sequences in a clean, human-readable format. | Provides clear visual verification of final alignment accuracy. |

### Defaut Scoring Parameters Used
* **Match:** `+2` 
* **Mismatch:** `-1` 
* **Gap Open:** `-2`
* **Gap Extend:** `-1`

---

## 📊 Performance & Limitations
* **Sequence Tolerance:** Successfully tolerates up to ~10% mismatches and minor length variations.
* **Heuristic Trade-off:** While highly efficient, the two-pass search is a heuristic step and may occasionally miss the absolute global optimum in highly chaotic sequences.
