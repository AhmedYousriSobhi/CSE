# ML-Zytona — Complete Exam Answers

> Compiled from: Fall 2018 · Fall 2020 · Spring/Summer 2021–2022 · Fall 2021–2023 · Spring 2025

---

## Table of Contents

1. [Eigen Decomposition & SVD](#1-eigen-decomposition--svd)
2. [Perceptron](#2-perceptron)
3. [Activation Functions](#3-activation-functions)
4. [Neural Networks](#4-neural-networks)
5. [BackPropagation](#5-backpropagation)
6. [Optimization](#6-optimization)
7. [NN Training Process](#7-nn-training-process)
8. [CNN](#8-cnn)
9. [CNN Architectures](#9-cnn-architectures)
10. [RNN – LSTM](#10-rnn--lstm)
11. [Attention – Transformers – Autoencoders](#11-attention--transformers--autoencoders)
12. [GAN Related](#12-gan-related)

---

## 1. Eigen Decomposition & SVD

### Q1 — Fall 2018 F

**Question:** X = [[6,−3],[−2,7],[−4,5],[6,−3]]. PCA from 2D→1D. (1) Covariance matrix & eigenvectors. (2) Project 4 points. (3) Prove right singular vectors of X are eigenvectors of the covariance matrix.

---

**Part 1 — Covariance Matrix**

Compute the sample mean (data is NOT centered):

$$\mu = \frac{1}{4}\sum x_i = [1.5,\ 1.5]^T$$

Center the data: $\tilde{X} = X - \mathbf{1}\mu^T$

$$\tilde{X} = \begin{bmatrix}4.5 & -4.5 \\ -3.5 & 5.5 \\ -5.5 & 3.5 \\ 4.5 & -4.5\end{bmatrix}$$

Sample covariance:

$$\Sigma = \frac{1}{n-1}\tilde{X}^T\tilde{X} = \begin{bmatrix}30.33 & -26.33 \\ -26.33 & 24.33\end{bmatrix}$$

Eigenvalues from $\det(\Sigma - \lambda I) = 0$:

$$\lambda_1 \approx 54.13,\quad \lambda_2 \approx 0.53$$

Principal eigenvector (unit): $v_1 \approx [0.737,\ -0.676]^T$

---

**Part 2 — Projection**

Project each original (un-centered) point $x$ onto $v_1$: coordinate $= x^T v_1$

| Point | Projection $x^T v_1$ |
|-------|----------------------|
| [6, −3] | $6(0.737) + (-3)(-0.676) \approx 6.45$ |
| [−2, 7] | $-2(0.737) + 7(-0.676) \approx -6.21$ |
| [−4, 5] | $-4(0.737) + 5(-0.676) \approx -6.33$ |
| [6, −3] | $\approx 6.45$ |

---

**Part 3 — Proof**

Let $X = U\Sigma V^T$ be the SVD. The sample covariance matrix is:

$$C = \frac{1}{n-1}X^TX = \frac{1}{n-1}(U\Sigma V^T)^T(U\Sigma V^T) = \frac{1}{n-1}V\Sigma^2 V^T$$

since $U^TU = I$. Therefore:

$$C \cdot v_i = \frac{1}{n-1}V\Sigma^2 V^T v_i = \frac{\sigma_i^2}{n-1} v_i$$

Every right singular vector $v_i$ with singular value $\sigma_i$ is an eigenvector of $C$ with eigenvalue $\lambda_i = \sigma_i^2/(n-1)$. $\square$

---

## 2. Perceptron

### Q1 — Fall 2018 M

**Question:** Classify points inside the diamond $\{(\pm1,0),(0,\pm1)\}$ as C1, exterior as C2.

**Answer:**

The L1-ball (diamond) satisfies four half-plane constraints. Use 4 hidden threshold neurons:

- $h_1 = \text{step}(1 - x_1 - x_2)$
- $h_2 = \text{step}(1 - x_1 + x_2)$
- $h_3 = \text{step}(1 + x_1 - x_2)$
- $h_4 = \text{step}(1 + x_1 + x_2)$

Output neuron (AND gate): fires when all 4 active → weights all 1, bias $= -3.5$.

**Verification:**
- $(0,0)$: all constraints satisfied → all hidden = 1 → **C1 ✓**
- $(0,5)$: $1 - 0 - 5 = -4 < 0$ → $h_1 = 0$ → output = 0 → **C2 ✓**

---

### Q2 — Fall 2018 F

**Question:** $y = 1$ if $x_2 \geq |x_1|$. (1) No hidden layer? (2) Neuron for $x_2 \geq x_1$. (3) Two-layer net.

**Part 1:** No. The boundary $x_2 = |x_1|$ is a V-shape — non-linear. A single-layer perceptron can only form one linear boundary.

**Part 2:** For $x_2 \geq x_1$, i.e., $x_2 - x_1 \geq 0$:

$$z = -x_1 + x_2,\quad y = \text{step}(z),\quad w_1=-1,\ w_2=+1,\ b=0$$

**Part 3:** $|x_1| \leq x_2$ means $x_1 \leq x_2$ AND $-x_1 \leq x_2$:

- $h_1 = \text{step}(x_2 - x_1)$ — detects $x_1 \leq x_2$
- $h_2 = \text{step}(x_2 + x_1)$ — detects $-x_1 \leq x_2$
- Output: $\text{step}(h_1 + h_2 - 1.5)$ — fires only when both active

---

### Q3 — Fall 2020 F

**Question:** Shallow NN with 5 nodes for multiclassification. (a) Perceptron loss + derivatives. (b) SVM criterion.

**Part a — Perceptron Multiclass Loss:**

Let $w_k \in \mathbb{R}^d$ for each class $k$, $\hat{y} = \arg\max_k w_k^T x$.

$$L = -\sum_{x \in \mathcal{Y}} w_{t(x)}^T x \quad \text{(sum over misclassified samples)}$$

Gradients for each misclassified sample:

$$\frac{\partial L}{\partial w_k} = -\sum_{x: t(x)=k} x \quad \text{(true class)}, \qquad \frac{\partial L}{\partial w_k} = +\sum_{x: \hat{y}=k} x \quad \text{(predicted class)}$$

**Update rule:** for each misclassified $(x, t, \hat{y})$:

$$w_t \leftarrow w_t + \rho x, \qquad w_{\hat{y}} \leftarrow w_{\hat{y}} - \rho x$$

**Sizes:** $w_k \in \mathbb{R}^{d \times 1}$, $W = [w_1|\cdots|w_5] \in \mathbb{R}^{d \times 5}$

**Part b — SVM Criterion:**

$$L_{\text{SVM}} = \sum_{k \neq t} \max(0,\ 1 + w_k^T x - w_t^T x)$$

Gradient for violating classes: $\frac{\partial L}{\partial w_k} = +x$, $\frac{\partial L}{\partial w_t} = -(\text{\# violating classes}) \cdot x$. SVM enforces a margin of 1; perceptron uses 0-1 loss.

---

### Q4 — Fall 2020 F

**Question:** Linear classifier for C1: $(2,1)^T$; C2: $(0,1)^T$, $(-1,1)^T$.

**Answer:** Since all points have $x_2 = 1$, the data varies only along $x_1$. Place boundary at $x_1 = 1$ (midpoint between $x_1 = 0$ and $x_1 = 2$):

$$g(x) = x_1 - x_2 + 0.5$$

- $(2,1)$: $2 - 1 + 0.5 = 1.5 > 0$ → **C1 ✓**
- $(0,1)$: $0 - 1 + 0.5 = -0.5 < 0$ → **C2 ✓**
- $(-1,1)$: $-1 - 1 + 0.5 = -1.5 < 0$ → **C2 ✓**

---

### Q5 — Fall 2020 F

Same as Q1. Diamond region, same 4-neuron architecture. Verify $(0,0) \to C1$, $(0,5) \to C2$. ✓

---

### Q6 — Fall 2020 M

**Question:** Risk of training for very many iterations to minimize training error?

**Answer:** **Overfitting.** The model memorizes noise and idiosyncrasies in the training set, losing generalization ability. Training error → 0 but test error rises. The decision boundary becomes tuned to training examples rather than the underlying distribution.

---

### Q7 — Fall 2020 M

**Question:** Why use learning rate $\rho$ in the perceptron algorithm?

**Answer:** The learning rate $\rho$ controls the **step size** of each weight update. Without it, a single misclassified point can overcorrect — swinging the boundary too far and causing oscillation or divergence. $\rho$ dampens corrections, enabling smoother convergence and stability when the same point is repeatedly misclassified.

---

### Q8 — Fall 2020 F & Summer 2022 F

**Question:** Why are non-linearities necessary in a neural network?

**Answer:** Without non-linearities, every layer is a linear map. A composition of linear functions is itself linear:

$$W_L(\cdots W_2(W_1 x)\cdots) = W^* x$$

No matter how many layers, the network collapses to a single linear transformation. Non-linear activations break this collapse, enabling the network to approximate arbitrarily complex functions (Universal Approximation Theorem) and capture non-linear patterns in data.

---

### Q9 — Spring 2022 M

**Question:** Heaviside step function $f(x) = \mathbf{1}[x \geq 0]$ with Adam optimizer — good idea?

**Answer:** **No.** The Heaviside function has **zero gradient almost everywhere** and is undefined at $x = 0$. Backpropagation requires $\partial f / \partial x$, which is zero everywhere — gradients vanish immediately and Adam (or any gradient-based optimizer) cannot update weights. Training fails completely. Use ReLU, Leaky ReLU, sigmoid, or tanh instead.

---

### Q10 — Summer 2022 M

**Question:** Binary classification: class 0 (interior rectangle), class 1 (surrounding). 2→4→1 perceptron network.

**Answer:** The inner class 0 region is bounded by four sides (approximate from the plot: $0.9 \leq x_1 \leq 2.2$, $1.2 \leq x_2 \leq 2.1$). Four hidden neurons:

- $h_1 = \text{step}(x_1 - 0.9)$, $h_2 = \text{step}(2.2 - x_1)$, $h_3 = \text{step}(x_2 - 1.2)$, $h_4 = \text{step}(2.1 - x_2)$

Output: $y = \text{step}(h_1 + h_2 + h_3 + h_4 - 3.5)$ — fires (class 0) only when all 4 constraints are satisfied.

---

### Q11 — Summer 2022 M

**Question:** Can the perceptron algorithm solve XNOR?

**Answer:** A **single-layer perceptron cannot** solve XNOR. The truth table (1 when inputs agree) is not linearly separable — the class-1 points (0,0) and (1,1) lie at opposite corners of the unit square.

**Multi-layer solution (inspection):**

- $h_1 = \text{step}(x_1 + x_2 - 0.5)$ — detects "at least one is 1"
- $h_2 = \text{step}(-x_1 - x_2 + 1.5)$ — detects "at most one is 1"
- Output: $\text{step}(h_1 + h_2 - 1.5)$

The perceptron algorithm on a single layer would not converge (data not linearly separable). The inspection solution differs from an algorithm-derived one.

---

### Q12 — Fall 2023 M

**Question:** Points inside a unit cube → class 1. Design perceptron NN.

**Answer:** A 3D unit cube (e.g., $0 \leq x_1, x_2, x_3 \leq 1$) has 6 faces → 6 hidden threshold neurons:

- $h_1 = \text{step}(x_1)$, $h_2 = \text{step}(1-x_1)$
- $h_3 = \text{step}(x_2)$, $h_4 = \text{step}(1-x_2)$
- $h_5 = \text{step}(x_3)$, $h_6 = \text{step}(1-x_3)$

Output: $y = \text{step}(h_1+h_2+h_3+h_4+h_5+h_6 - 5.5)$

**Architecture:** Input (3) → Hidden (6, step functions) → Output (1, step function)

---

## 3. Activation Functions

### Q1 — Fall 2020 F & Summer 2022 F

**Question:** Which activations lead to vanishing gradients: Sigmoid, tanh, ReLU, Leaky-ReLU?

**Answer:**

- **Sigmoid → YES.** Saturates at both ends; derivative $\sigma(1-\sigma) \leq 0.25$. Gradients shrink exponentially through layers.
- **tanh → YES.** Saturates at $\pm 1$; derivative $1 - \tanh^2(x) \leq 1$, approaches 0 at saturation.
- **ReLU → Partial.** Gradient = 1 for $x > 0$ (no vanishing), but = 0 for $x \leq 0$ — neurons permanently die and propagate zero gradient ("dying ReLU").
- **Leaky-ReLU → No.** Gradient = 1 for $x > 0$, $\alpha$ (small positive) for $x \leq 0$. No saturation, no dead neurons.

---

### Q2 — Fall 2021 F

**Question:** Negative consequence of ReLU's non-negative output. Alternatives?

**Answer:**

**Negative consequence — Dying ReLU:** If a neuron's pre-activation is always negative (large negative bias or bad initialization), ReLU always outputs 0. The gradient is also 0, so weights never update — the neuron is permanently dead.

**Alternatives:** Leaky ReLU ($\alpha x$ for $x \leq 0$), ELU (exponential for negatives), PReLU (learnable $\alpha$), GELU/Swish (used in transformers).

---

### Q3 — Spring 2022 M

**Question:** (1) Jacobian of tanh. (2) Saturated units problem. (3) Optimization advantage of tanh over sigmoid.

**Part 1:**

For elementwise $y = \tanh(z)$:

$$\frac{\partial y}{\partial z} = \text{diag}(1 - \tanh^2(z_1),\ \ldots,\ 1 - \tanh^2(z_n)) = \text{diag}(1 - y_1^2,\ \ldots,\ 1-y_n^2)$$

**Part 2:**

Saturation occurs when $|x|$ is large — both sigmoid and tanh output near their extremes with derivatives → 0. Backpropagated gradients through saturated units ≈ 0, starving upstream weights. **Switching from sigmoid to tanh does NOT fix saturation** — tanh also saturates at $\pm 1$.

**Part 3:**

tanh is **zero-centered** (outputs $\in [-1, 1]$) while sigmoid outputs $\in [0,1]$ are always positive. With positive-only activations, all weight gradients in a layer have the same sign → **zig-zagging in optimization** (can only move in axis-aligned diagonal directions). tanh's zero-centered outputs allow mixed-sign gradients → more direct optimization paths.

---

### Q4 — Spring 2025 F

**Question:** Why can deep ReLU networks be more effective than shallow networks?

**Answer:** Deep ReLU networks can represent **exponentially more linear regions** than shallow ones with the same parameter count. Each additional ReLU layer folds and partitions the input space, creating exponentially more complex piecewise-linear boundaries. Beyond capacity: depth enables **hierarchical feature learning** — early layers capture low-level patterns (edges, textures), later layers combine them into abstract concepts, ideal for high-dimensional structured data.

---

### Q5 — Spring 2025 F

**Question:** Advantages of ReLU over sigmoid?

**Answer:**

1. **No vanishing gradient (active region):** Gradient = 1 for $x > 0$, no exponential shrinkage.
2. **Sparsity:** Outputs exactly 0 for $x \leq 0$ — sparse activations, computationally efficient, implicit regularization.
3. **Computational simplicity:** $\max(0, x)$ — no exponentials needed.
4. **Faster convergence:** Constant gradient in active region enables faster training in deep networks.
5. **No output saturation (positive side):** Unbounded above — no saturation for positive inputs.

---

## 4. Neural Networks

### Q1 — Fall 2021 F (Early Stopping)

**Fill-in blanks:**

1. Y-axis: **Error / Loss**
2. X-axis: **Number of epochs / Training iterations**
3. Y-axis value: **Minimum validation error**
4. X-axis value: **Early stopping point**
5. Upper curve (rising): **Validation / Test error**
6. Lower curve (falling): **Training error**

---

### Q2 & Q3 — Fall 2021 F

**Question:** What is overfitting? All methods to avoid it?

**Overfitting:** The model learns the training data too well — including noise — and generalizes poorly. Training error ≪ test error.

**Methods to avoid:**

1. More training data / data augmentation
2. Early stopping
3. L1/L2 regularization (weight penalties)
4. Dropout
5. Reduce model complexity (fewer layers/neurons)
6. Batch normalization
7. Cross-validation
8. Ensemble methods

---

### Q5 — Fall 2020 F & Summer 2022 F

**Question:** Why Xavier initialization? Why important?

**Answer:** Xavier initialization sets: $W \sim \mathcal{U}\left[-\sqrt{\frac{6}{n_{in}+n_{out}}},\ +\sqrt{\frac{6}{n_{in}+n_{out}}}\right]$

It ensures **variance of activations and gradients is approximately equal across layers**. Without it:
- Weights too large → sigmoid/tanh saturate → zero gradients → training fails.
- Weights too small → signals attenuate exponentially (vanishing signal/gradient).

Xavier keeps activation and gradient magnitudes healthy in both forward and backward passes from the first iteration.

> For ReLU, He initialization (variance $= 2/n_{in}$) is preferred since ReLU zeros out half the units.

---

### Q6 — Fall 2020 F & Summer 2022 F

**Question:** Is Batch Normalization linear or non-linear?

**Answer:** BatchNorm: $y = \gamma \cdot \frac{x - \mu_B}{\sigma_B} + \beta$

- **Linear in $x$ at test time:** $\mu_B$ and $\sigma_B$ are fixed running averages. The operation is affine: $y = \frac{\gamma}{\sigma_B}x + \left(\beta - \frac{\gamma\mu_B}{\sigma_B}\right)$.
- **Non-linear in $x$ at training time:** $\mu_B$ and $\sigma_B$ depend on the current batch, which includes $x$ itself → non-linear relationship.

**Conclusion: linear at test time, non-linear at training time.**

---

### Q7 — Fall 2021 F

**Question:** Derivatives of BatchNorm w.r.t. $\gamma$ and $\beta$.

Forward: $\hat{x}_i = (x_i - \mu)/\sigma$, $y_i = \gamma\hat{x}_i + \beta$.

$$\frac{\partial L}{\partial \gamma} = \sum_i \frac{\partial L}{\partial y_i} \cdot \hat{x}_i$$

$$\frac{\partial L}{\partial \beta} = \sum_i \frac{\partial L}{\partial y_i}$$

$$\frac{\partial L}{\partial \hat{x}_i} = \frac{\partial L}{\partial y_i} \cdot \gamma$$

$$\frac{\partial L}{\partial x_i} = \frac{1}{\sigma}\left[\frac{\partial L}{\partial \hat{x}_i} - \frac{1}{m}\sum_j \frac{\partial L}{\partial \hat{x}_j} - \hat{x}_i \cdot \frac{1}{m}\sum_j \frac{\partial L}{\partial \hat{x}_j}\hat{x}_j\right]$$

---

### Q8 — Spring 2021 F & Fall 2023 F

**Question:** Why is a deep NN with linear activations and no bias equivalent to a shallow NN?

**Answer:** A composition of linear transformations is linear:

$$f(x) = W_L \cdots W_2 W_1 x = W^* x$$

where $W^* = W_L \cdots W_1$ is a single matrix. No matter how many layers, the composite is a single linear map — equivalent to one layer with weight $W^*$.

---

### Q9

**Question:** 4-3-1 NN, sigmoid activations, all weights and biases = 0. Output?

**Answer:** All neurons compute $z = W \cdot \mathbf{0} + 0 = 0$, and $\sigma(0) = 0.5$.

- Hidden layer: all 3 neurons output **0.5**
- Output neuron: $z = W \cdot [0.5, 0.5, 0.5]^T = 0$ (weights are zero) → $\sigma(0) = $ **0.5**

Output is **0.5**, regardless of input. This illustrates the symmetry-breaking failure.

---

### Q10

**Question:** Prove ReLU is non-linear (superposition theorem).

**Answer:** A function $f$ is linear if $f(\alpha x + \beta y) = \alpha f(x) + \beta f(y)$. Counterexample with $x = -1$, $y = 1$, $\alpha = \beta = 1$:

$$\text{LHS: } \text{ReLU}(-1+1) = \text{ReLU}(0) = 0$$
$$\text{RHS: } \text{ReLU}(-1) + \text{ReLU}(1) = 0 + 1 = 1$$

$\text{LHS} \neq \text{RHS}$ → ReLU violates superposition → **ReLU is non-linear.** $\square$

---

### Q11 — Spring 2025 F

**Question:** Convergence condition of the perceptron algorithm?

**Answer:** **Perceptron Convergence Theorem:** The algorithm converges (finds a separating hyperplane) in a finite number of steps **if and only if the data is linearly separable**.

If there exists $w^*$ with $y_i(w^{*T}x_i) \geq \gamma > 0$ for all $i$, then the perceptron makes at most $(R/\gamma)^2$ mistakes, where $R = \max\|x_i\|$.

---

### Q12 & Q18 — Spring 2025 F / Fall 2023 F

**Question:** 2-2-1 NN, tanh, all weights and biases = 0.1. Input $[0.5, -0.5]$.

**Hidden Layer:**

$$z_{h1} = z_{h2} = 0.1(0.5) + 0.1(-0.5) + 0.1 = 0 + 0.1 = 0.1$$
$$h_1 = h_2 = \tanh(0.1) \approx 0.0997$$

**Output Layer:**

$$z_{out} = 0.1(0.0997) + 0.1(0.0997) + 0.1 = 0.01994 + 0.1 = 0.11994$$
$$\text{output} = \tanh(0.11994) \approx \mathbf{0.1194}$$

---

### Q13 — Fall 2023 F

**Question:** Trained with dropout but forgot to divide by $p$. Fix at test time?

**Answer:** Without dividing by $p$ during training, the network learned with activations scaled by $p$ relative to inference. **Fix at test time:** multiply all activations (or weights) by $p$ before inference. This compensates for the missing scaling factor and restores the correct expected activation magnitude.

---

### Q14 — Fall 2018 M & Fall 2020 F

**Question:** Why can't a multilayer network with zero initial weights learn?

**Answer:** **Symmetry Problem.** With all weights = 0, every neuron in a layer produces identical pre-activations (all zero) and identical outputs. During backpropagation, all neurons receive identical gradients and update identically — remaining forever symmetric. An $N$-neuron layer effectively behaves like a 1-neuron layer and cannot learn distinct features. This is the **symmetry breaking failure**.

---

### Q15 — Fall 2020 F

**Question:** Loss function almost completely flat at the start of training. Possible causes?

**Answer:**

- **Saturated activations:** Weights initialized too large → sigmoid/tanh saturate → near-zero gradients.
- **Vanishing gradients:** Too many layers with saturating activations.
- **Dead ReLU neurons:** Large negative biases kill all neurons from initialization.
- **Learning rate too small:** Gradients exist but updates are negligibly small.
- **Zero weight initialization:** Symmetric gradients cancel.
- **Wrong loss function:** Loss doesn't carry meaningful gradient for the task.

---

### Q16 — Spring 2022 M

**Question:** Linear hidden layer ($h = cx$), sigmoid output. (1) Express $P(y=1|x,w)$. (2) Equivalent no-hidden-layer net. (3) Can all linear multi-layer nets be collapsed?

**Part 1:**

$$P(y=1|x,w) = \sigma\!\left(w_7 \cdot c(w_3x_1+w_5x_2+w_1) + w_8 \cdot c(w_4x_1+w_6x_2+w_2) + w_9\right)$$

This is a sigmoid of a linear function of $x$ → **linear decision boundary**.

**Part 2:** Since the hidden layer is linear, it can be absorbed into the output weights. The equivalent no-hidden-layer network has weights $\tilde{w}_i = c \sum_j w_{j,\text{out}} \cdot w_{ij,\text{hidden}}$.

**Part 3:** **Yes.** Any composition of linear layers is itself a single linear layer. Depth without non-linearity provides no additional representational power.

---

### Q17 — Fall 2023 F

**Question:** Training vs test error curves as sample size increases. (1) Which is training error? (2) What does the gap represent?

**Answer:**

1. **Curve (ii)** (lower, starts low, may rise slightly) = **Training error.** Curve (i) (upper, starts high, falls) = **Test error.**
2. The gap represents the **generalization gap** — how much worse the model performs on unseen data. Large gap = overfitting. The gap narrows as training set size grows (more representative sample of the data distribution).

---

## 5. BackPropagation

### Q1 — Fall 2018 F (Car Driving NN)

**Architecture:** 4096+1 input → 2048 hidden (ReLU) → 2 output. Notation: $x$ (input+bias), $g = Vx$, $h = r(g)$ (ReLU), $z = Wh$, $J = \frac{1}{2}|y-z|^2$.

**Part 1 — Parameter Count:**

$$\text{Input→Hidden: } (4096+1) \times 2048 = 8{,}390{,}656$$
$$\text{Hidden→Output: } (2048+1) \times 2 = 4{,}098$$
$$\text{Total} = \mathbf{8{,}394{,}754}$$

**Part 2 — $\partial J / \partial W_{ij}$:**

$$\frac{\partial J}{\partial z} = -(y-z) \in \mathbb{R}^{2\times1}$$
$$\frac{\partial J}{\partial W_{ij}} = \frac{\partial J}{\partial z_i} \cdot h_j$$

**Part 3 — Outer Product:**

$$\frac{\partial J}{\partial W} = \frac{\partial J}{\partial z} \cdot h^T = -(y-z) \cdot h^T \quad [2 \times 2049]$$

**Part 4 — $\partial J / \partial V_{ij}$:**

$$\frac{\partial J}{\partial h} = W^T \frac{\partial J}{\partial z}$$
$$\frac{\partial J}{\partial g} = \frac{\partial J}{\partial h} \odot r'(g) \quad \text{(ReLU mask: 1 if } g>0\text{)}$$
$$\frac{\partial J}{\partial V} = \frac{\partial J}{\partial g} \cdot x^T \quad [2048 \times 4097]$$

---

### Q3 — Summer 2022 M & Fall 2023 M

**Graph:** $h_1 = w_1x_1$, $h_2 = w_2x_2$, $h = h_1+h_2$, $y = \sigma(h)$, $e = y-t$, $l = e^2$. Forward values: $h=0.8$, $y=0.55$, $e=-0.45$, $l=0.20$.

$$\frac{\partial l}{\partial e} = 2e = -0.90$$
$$\frac{\partial l}{\partial y} = -0.90 \cdot 1 = -0.90$$
$$\frac{\partial l}{\partial h} = \frac{\partial l}{\partial y} \cdot y(1-y) = -0.90 \times 0.55 \times 0.45 \approx -0.2228$$
$$\frac{\partial l}{\partial w_1} = \frac{\partial l}{\partial h} \cdot x_1 = -0.2228 \times 2 = -0.4456$$
$$\frac{\partial l}{\partial w_2} = \frac{\partial l}{\partial h} \cdot x_2 = -0.2228 \times 3 = -0.6684$$

Key: sigmoid derivative $\sigma'(h) = y(1-y)$.

---

### Q4 — Spring 2025 F

**Graph:** $z = (x-y)/\sigma(x)$, where $x = ab$, $y = b+c$, $\sigma = \text{sigmoid}(x)$.

$$\frac{\partial z}{\partial x} = \frac{1}{\sigma} - \frac{(x-y)(1-\sigma)}{\sigma} \quad \text{(x appears in both numerator and } \sigma\text{)}$$
$$\frac{\partial z}{\partial y} = -\frac{1}{\sigma}$$
$$\frac{\partial z}{\partial a} = \frac{\partial z}{\partial x} \cdot b, \quad \frac{\partial z}{\partial b} = \frac{\partial z}{\partial x} \cdot a + \frac{\partial z}{\partial y} \cdot 1, \quad \frac{\partial z}{\partial c} = \frac{\partial z}{\partial y} = -\frac{1}{\sigma}$$

---

### Q5 — Fall 2020 F & Summer 2022 F

**Question:** Gradient through tanh — smaller, equal, or larger?

**Answer:** tanh derivative: $1 - \tanh^2(x) \in (0, 1]$.

- **Equal (= 1):** only when $x = 0$
- **Smaller (< 1):** for all $x \neq 0$
- **Never larger:** tanh can only attenuate, never amplify, the gradient.

---

## 6. Optimization

### Q1 — Fall 2020 F (1-1-1 NN with learnable slope)

**Computational graph:** $x \to [g = Vx + b_v] \to [h = \text{ReLU}(g)] \to [n = Wh + b_w] \to [z = \alpha n] \to L$

**Learnable params:** $V, W, \alpha, b_v, b_w$

**Backprop rules:**

$$\frac{\partial L}{\partial \alpha} = \frac{\partial L}{\partial z} \cdot n, \quad \frac{\partial L}{\partial W} = \frac{\partial L}{\partial n} \cdot h^T$$
$$\frac{\partial L}{\partial h} = \frac{\partial L}{\partial n} \cdot W, \quad \frac{\partial L}{\partial g} = \frac{\partial L}{\partial h} \odot \mathbf{1}[g > 0]$$
$$\frac{\partial L}{\partial V} = \frac{\partial L}{\partial g} \cdot x^T, \quad \frac{\partial L}{\partial b_v} = \frac{\partial L}{\partial g}, \quad \frac{\partial L}{\partial b_w} = \frac{\partial L}{\partial n}$$

---

### Q2 — Spring 2021 F & Fall 2023 F

**Question:** SGD batch size behavior.

**Part 1 (small batches):** Small batches produce noisy gradient estimates. As batch size increases in the small regime, gradient estimates become more accurate → fewer iterations needed to reach target loss. This is the **linear scaling regime**.

**Part 2 (large batches):** At large batch sizes, gradient estimates are already very accurate — more samples don't reduce variance meaningfully. The bottleneck shifts to the optimization landscape geometry. Iterations-to-convergence plateaus — this is the **saturation regime**.

---

### Q3 — Spring 2021 F, Spring 2022 F, Fall 2023 F

**Model:** $z = w_0 + w_1x + w_2x^2$, $y = 1 + e^z$, $J = \frac{1}{2}(\log y - \log t)^2$.

**Backprop rules (each referencing previously computed values):**

$$\frac{\partial J}{\partial (\log y)} = \log y - \log t$$
$$\frac{\partial J}{\partial y} = \frac{\log y - \log t}{y}$$
$$\frac{\partial J}{\partial z} = \frac{\partial J}{\partial y} \cdot e^z = \frac{(\log y - \log t)}{y} \cdot e^z$$
$$\frac{\partial J}{\partial w_2} = \frac{\partial J}{\partial z} \cdot x^2$$

---

### Q4 — Spring 2021 F, Spring 2022 F, Fall 2023 F

**Question:** Why is L2 called "weight decay"? L4 update rule.

**L2 weight decay:** Update rule with L2 penalty ($\Omega = \|\theta\|^2$, gradient $= 2\alpha w_1$):

$$w_1 \leftarrow w_1 - \mu\frac{\partial J}{\partial w_1} - \mu\alpha w_1 = (1-\mu\alpha)w_1 - \mu\frac{\partial J}{\partial w_1}$$

The factor $(1-\mu\alpha) < 1$ multiplies $w_1$ at every step — shrinking (decaying) weights toward zero independently of the loss gradient. Hence "weight decay."

**L4 Regularization:** $\Omega = \|\theta\|_4^4 = \sum w_i^4$, gradient $= 4w_1^3$:

$$w_1 \leftarrow w_1 - \mu\frac{\partial J}{\partial w_1} - 4\mu\alpha w_1^3$$

L4 penalizes large weights more aggressively (cubic decay rate vs linear in L2).

---

### Q5 — Fall 2023 M

**Question:** Momentum: $\delta w_t = \alpha\Delta w_{t-1} - \eta\nabla w_t$, $\eta=1$, $\alpha=0.9$. Fraction of $\nabla w_1$ in $\Delta w_k$?

**Answer:** With $\eta = 1$: $\Delta w_1 = -\nabla w_1$. After $k$ iterations, $\nabla w_1$ contributes via repeated $\alpha$ multiplication:

$$\text{Contribution} = -\nabla w_1 \cdot \alpha^{k-1} = -\nabla w_1 \cdot 0.9^{k-1}$$

The fraction of $\nabla w_1$ in $\Delta w_k$ is $\mathbf{\alpha^{k-1} = 0.9^{k-1}}$. Older gradients decay exponentially — recent gradients dominate.

---

### Q6 — Fall 2023 M

**Graph:** $h_1 = xy$, $h_2 = yz$, $h = h_1 h_2$, $g = h^2$. Values: $x=3, y=2, z=1$, $h_1=6$, $h_2=2$, $h=12$, $g=144$.

$$\frac{\partial g}{\partial h} = 2h = 24, \quad \frac{\partial g}{\partial h_1} = 24 \cdot h_2 = 48, \quad \frac{\partial g}{\partial h_2} = 24 \cdot h_1 = 144$$
$$\frac{\partial g}{\partial x} = 48 \cdot y = 96, \quad \frac{\partial g}{\partial z} = 144 \cdot y = 288$$
$$\frac{\partial g}{\partial y} = 48 \cdot x + 144 \cdot z = 144 + 144 = 288$$

---

### Q8 — Fall 2018 M

**Question:** Global vs local minima. How to detect and fix local minima in BP networks?

**Answer:**

- **Global minimum:** The single lowest point of the loss surface — optimal solution.
- **Local minimum:** Lower than immediate neighbors but not globally lowest — network can get stuck.

**Detection:** Train multiple times from different random initializations. Significantly varying results indicate local minima traps.

**Fixes:** Multiple random restarts; SGD noise to escape shallow minima; momentum; learning rate schedules (warm restarts); simulated annealing.

> In high-dimensional spaces, true local minima are rare — most critical points are saddle points.

---

### Q10 — Fall 2020 F

**Question:** SGD vs modern optimizers (Adam/RMSProp) at saddle and local minima.

| Scenario | SGD | Adam/RMSProp |
|----------|-----|--------------|
| Saddle points | Near-zero gradient → stalls. Stochastic noise may help escape slowly. | Adaptive rates rescale per-parameter; momentum provides gradient memory → faster escape. |
| Local minima | May trap. Stochastic noise can escape shallow ones. | Also susceptible, but momentum and adaptive rates help navigate. In deep nets, both find similar quality minima. |

---

### Q11 — Fall 2021 F

**Question:** What is a saddle point? SGD advantage/disadvantage?

**Saddle point:** A critical point (gradient = 0) that is a local minimum in some dimensions and a local maximum in others.

**SGD Advantage:** Stochastic noise in gradient estimates rarely hits the exact zero-gradient point — perturbations can push it along descending directions, enabling escape.

**SGD Disadvantage:** On extended flat plateaus near saddle points, near-zero gradients mean extremely slow traversal — can take very many iterations.

---

## 7. NN Training Process

### Q1 — Spring 2021 F & Fall 2023 F

**Part 1 — Tuning on training set:** Model will overfit. Hyperparameters are chosen to maximize training performance, potentially selecting an overly complex model. Test error is much higher with no reliable estimate of generalization.

**Part 2 — Tuning on validation set:** After many trials, hyperparameters become optimized for the specific validation set (overfitting the validation set). Test error may still exceed validation error. A held-out **test set** must be used only once for final evaluation.

---

### Q2 — Spring 2021 F & Fall 2023 F

**Question:** Dog/cat images ordered: all dogs first, then cats. Must shuffle?

**Answer:** **Yes — the friend is right.** For mini-batch gradient descent, each batch would contain only one class → biased gradient estimates → oscillatory updates. Shuffling ensures each mini-batch is a representative sample of both classes → unbiased gradients. (Ordering doesn't matter for full-batch GD, but mini-batch is always used in practice.)

---

### Q3

**Question:** Triangle $(1,1),(-1,1),(0,-1)$ — classify interior as class 1. Design perceptron NN.

Three edge constraints (check each half-plane points inward):

- $h_1 = \text{step}(1 - x_2)$ — below $y = 1$
- $h_2 = \text{step}(2x_1 - x_2 + 1)$ — right of left edge
- $h_3 = \text{step}(-2x_1 - x_2 + 1)$ — left of right edge

Output: $\text{step}(h_1+h_2+h_3-2.5)$

**Architecture:** Input (2) → Hidden (3) → Output (1)

---

### Q5 — Fall 2021 F

**Question:** Why does dropout act as a regularizer?

**Answer:**

1. **Prevents co-adaptation:** Neurons cannot rely on specific partners always being present → each learns independently useful features.
2. **Implicit ensemble:** Each training pass trains a different subnetwork. Test time approximates averaging exponentially many subnetworks → reduces variance.
3. **Weight constraints:** Cannot grow arbitrarily large to compensate for absent partners → similar effect to L2 regularization.

---

### Q6 — Fall 2021 F, Summer 2022 F, Fall 2023 F

**Question:** What features of ResNet alleviate vanishing gradients?

**Answer:** **Skip (residual) connections.** Output: $F(x) + x$ instead of $F(x)$. During backprop:

$$\frac{\partial L}{\partial x} = \frac{\partial L}{\partial (F(x)+x)} \cdot \left(\frac{\partial F}{\partial x} + I\right)$$

The identity matrix $I$ ensures gradient always has a direct path backward — even if $\partial F/\partial x \approx 0$, gradient flows through the $+I$ term. Prevents exponential decay across many layers.

---

### Q7 — Fall 2023 M

**Question:** "Backpropagated gradient through tanh is always ≤ upstream gradient in magnitude."

**Answer:** tanh derivative: $\frac{\partial}{\partial x}\tanh(x) = 1 - \tanh^2(x) \in (0, 1]$ for all $x$.

Backprop: downstream = upstream $\times (1-\tanh^2(x))$.

Since the multiplier is always $\leq 1$, the downstream magnitude cannot exceed upstream. Equals 1 only at $x = 0$, strictly less everywhere else. tanh always attenuates (never amplifies) the gradient. $\square$

---

### Q8 — Spring 2022 F

**Question:** Risk of tuning hyperparameters using a test dataset?

**Answer:** **Data leakage / test set contamination.** The test set no longer simulates unseen data — choices are optimized for it specifically. The model may perform well on that test set but poorly in production. You lose the ability to measure true generalization.

---

### Q9 — Spring 2022 F

**Question:** Why does dropout improve performance? When to use it?

**Answer:** Dropout reduces overfitting via the regularization mechanisms described in Q5. Use it when:

- Large networks with many parameters relative to training data
- Fully connected layers (less common in conv layers due to weight sharing)
- Significant gap between training and validation accuracy

**Avoid when:** Dataset is very small (noise dominates), model is already underfitting, or at inference time (scale by $p$ instead).

---

### Q10 — Spring 2022 F

**Question:** Typical goal of good weight initialization?

**Answer:**

1. **Preserve signal variance across layers** — activations should neither explode nor vanish in the forward pass.
2. **Preserve gradient variance across layers** — gradients remain similarly scaled throughout backward pass.
3. **Break symmetry** — different neurons must start with different weights to learn different features.

Goal: keep activation and gradient magnitudes in a healthy, stable range from the very first pass, enabling stable and fast convergence.

---

### Q11 — Spring 2022 F

**Question:** Label 4 learning rate curves.

| Curve behavior | Label |
|----------------|-------|
| Spikes/diverges immediately | Very high learning rate |
| Drops fast then oscillates/diverges | High learning rate |
| Smooth convergence to low loss | Optimal learning rate |
| Very slow, barely decreasing | Low learning rate |

---

### Q12 — Spring 2022 F

**Question:** Batch normalization: training vs. test time.

| Aspect | Training | Test time |
|--------|----------|-----------|
| Mean $\mu$ | Current mini-batch | Fixed running average |
| Variance $\sigma^2$ | Current mini-batch | Fixed running average |
| $\gamma, \beta$ | Learned via backprop | Fixed |
| Nature | Non-linear (stats depend on batch) | Linear deterministic transform |

---

### Q14 — Fall 2023 M

**Question:** All sigmoid activations, weights initialized large positive. Good idea?

**Answer:** **Bad idea.** Large positive weights drive pre-activations to large positive values → sigmoid saturates near 1 → derivative $\sigma(1-\sigma) \approx 0$ → gradients vanish from the start → training fails. Additionally, all neurons saturate in the same direction (symmetry not broken), compounding the problem. Use Xavier/He initialization with small random weights.

---

### Q15 — Fall 2020 F

**Question:** Large gap between training and test accuracy — how to reduce?

**Answer:** Large gap indicates overfitting. Remedies:

- More training data or data augmentation
- L1/L2 regularization
- Dropout
- Early stopping
- Reduce model complexity (fewer layers/neurons)
- Batch normalization
- Cross-validation for hyperparameter selection

---

## 8. CNN

### Q1 — Spring 2021 F & Fall 2023 F (LeNet)

**Architecture:** Input 32×32 → C1: 6@28×28 → S2: 6@14×14 → C3: 16@10×10 → S4: 16@5×5 → C5: 120 → F6: 84 → Output: 10

**1. Filter size in C1:**
$32 - 28 + 1 = 5$ → **5×5 filter** (25 inputs per neuron)

**2. Parameters in C1:**
$6$ maps $\times$ $(5\times5 + 1) = 6 \times 26 = \mathbf{156}$

**3. Parameters in C3 (full connection):**
$16$ maps $\times$ $(6 \times 5\times5 + 1) = 16 \times 151 = \mathbf{2{,}416}$

**4. Parameters in F6:**
$120 \times 84 + 84 = 10{,}080 + 84 = \mathbf{10{,}164}$

---

### Q2 — Spring 2021 F (Convolution as FC Layer)

**Conv:** input $x=(x_1,x_2,x_3)$, kernel $(2,-1)$, output length 4, verify: $x=(1,2,3) \to y=(2,3,4,-3)$.

$$W = \begin{bmatrix} 2 & -1 & 0 \\ 0 & 2 & -1 \\ 0 & 0 & 2 \\ -1 & 0 & 0 \end{bmatrix}$$

Check: $W[1,2,3]^T = [2-2, 0+4-3, 0+0+6, -1]^T$... the weight matrix encodes the shifting kernel with circular wrap for the 4th output.

---

### Q3 — Fall 2018 F (100×100 → 100 feature maps)

| Case | Parameters |
|------|------------|
| 1. Conv, filter = 100×100 (same size as input) | $100 \times (100\times100\times1 + 1) = \mathbf{1{,}000{,}100}$ |
| 2. Conv, 10×10 filters, stride 5. Output: $19\times19$ | $100 \times (10\times10 + 1) = \mathbf{10{,}100}$ |
| 3. Locally connected, 10×10, stride 5 | $100 \times 19\times19 \times (10\times10+1) = \mathbf{3{,}646{,}100}$ |
| 4. Conv, 10×10 filters, stride 1. Output: $91\times91$ | $100 \times (10\times10+1) = \mathbf{10{,}100}$ |

> Locally connected layers have MORE parameters than conv layers of same filter size because filters are NOT shared across positions.

---

### Q4 — Fall 2018 F

**More parameters:** Higher capacity, can represent complex functions. Risk: overfitting, slower training, more memory.

**Fewer parameters:** Better generalization, faster training, lower memory. Risk: underfitting — insufficient capacity (high bias).

The optimal lies at the **bias-variance tradeoff** sweet spot.

---

### Q5 — Fall 2018 F

**Answer:** Local receptive fields capture **spatial locality.** Natural images have strong local correlations — edges, textures, shapes span multiple adjacent pixels. Filters larger than 1×1 detect these local spatial patterns. 1×1 filters only combine channel information, missing spatial structure entirely. Filters smaller than the full image ensure **parameter sharing**: the same pattern detector is applied everywhere, exploiting the translation invariance of natural image statistics.

---

### Q7 — Fall 2020 F

| Layer | Activation map | Weights | Biases |
|-------|---------------|---------|--------|
| Input | 128×128×3 | 0 | 0 |
| CONV-9-32 | 120×120×32 | $9\times9\times3\times32 = 77{,}760$ | 32 |
| POOL-2 | 60×60×32 | 0 | 0 |
| CONV-5-64 | 56×56×64 | $5\times5\times32\times64 = 51{,}200$ | 64 |
| POOL-2 | 28×28×64 | 0 | 0 |
| CONV-5-64 | 24×24×64 | $5\times5\times64\times64 = 102{,}400$ | 64 |
| POOL-2 | 12×12×64 | 0 | 0 |
| FC-3 | 3 | $12\times12\times64\times3 = 27{,}648$ | 3 |

---

### Q8 & Q14 — Fall 2020 F

**Invariant to:** Translation (approximately, via pooling).

**NOT invariant to:** Rotation or scale. A standard CNN with one conv layer does not capture rotated or scaled versions of the same feature without augmentation or specialized architectures.

---

### Q10 — Spring 2022 F

Input $96\times128\times128$, filter $128\times96\times7\times7$, stride=2, pad=3:

$$H_{out} = \left\lfloor\frac{128 + 2(3) - 7}{2}\right\rfloor + 1 = 64, \quad W_{out} = 64$$

**Output: $128 \times 64 \times 64$**

---

### Q11 — Spring 2022 F & Summer 2022 F

4 consecutive 3×3 conv layers, stride=1, no pooling. Receptive field after layer $n$: $RF = n(k-1) + 1 = 2n+1$. At $n=4$:

$$RF = 4(3-1)+1 = \mathbf{9\times9}$$

---

### Q13 — Summer 2022 F

RGB 256×256 → Conv 3×3, stride=1 → Pool 3×3, stride=2.

A pool unit looks at a 3×3 region of conv output. Each conv pixel sees 3×3 of the input. Total input extent:

$$RF = 3 \times 1 + (3-1) = 5 \quad \Rightarrow \quad \mathbf{5\times5} \text{ receptive field}$$

---

## 9. CNN Architectures

### Q1 — Spring 2022 F

| Aspect | GoogLeNet (Inception) | ResNet |
|--------|----------------------|--------|
| Key innovation | Inception modules — parallel 1×1, 3×3, 5×5 filters within one block | Residual (skip) connections: output = $F(x) + x$ |
| Depth | 22 layers (auxiliary classifiers to fight vanishing gradients) | 50/101/152+ layers |
| Parameter efficiency | 1×1 convolutions reduce dimensions before expensive filters (~5M params) | Bottleneck blocks (1×1, 3×3, 1×1) |
| Vanishing gradient fix | Auxiliary classifiers inject gradient mid-network | Skip connections provide direct gradient highway |
| Improvement over VGG | Much fewer params with comparable accuracy | Enables training of arbitrarily deep nets (solved degradation problem) |

---

## 10. RNN – LSTM

### Q1 — Spring 2021 F & Summer 2022 F

$h_0=1$, $x_1=x_2=10$, $y_1=y_2=5$, $W_h=1$, $W_x=0$, $W_y=2$.

**Part 1 — Forward pass:**

$$h_1 = W_h h_0 + W_x x_1 = 1 + 0 = 1, \quad \hat{y}_1 = W_y h_1 = 2$$
$$h_2 = W_h h_1 + W_x x_2 = 1, \quad \hat{y}_2 = W_y h_2 = \mathbf{2}$$

**Part 2 — Total loss:**

$$L_1 = (2-5)^2 = 9, \quad L_2 = (2-5)^2 = 9, \quad L_{total} = \mathbf{18}$$

**Part 3 — $\partial L/\partial h_1$:**

$$\frac{\partial L}{\partial h_1} = \underbrace{\frac{\partial L_1}{\partial \hat{y}_1} W_y}_{\text{via } \hat{y}_1} + \underbrace{\frac{\partial L_2}{\partial \hat{y}_2} W_y \cdot W_h}_{\text{via } h_2}$$
$$= 2(2-5)(2) + 2(2-5)(2)(1) = -12 + (-12) = \mathbf{-24}$$

---

### Q2 — Spring 2025 F

**LSTM equations:**

$$i_t = \sigma(W_i x_t + U_i h_{t-1} + b_i) \quad \text{(input gate)}$$
$$f_t = \sigma(W_f x_t + U_f h_{t-1} + b_f) \quad \text{(forget gate)}$$
$$o_t = \sigma(W_o x_t + U_o h_{t-1} + b_o) \quad \text{(output gate)}$$
$$\tilde{c}_t = \tanh(W_c x_t + U_c h_{t-1} + b_c) \quad \text{(cell candidate)}$$
$$c_t = f_t \odot c_{t-1} + i_t \odot \tilde{c}_t \quad \text{(cell state)}$$
$$h_t = o_t \odot \tanh(c_t) \quad \text{(hidden state)}$$

**Forget gate role:** $f_t \in (0,1)$ scales $c_{t-1}$ element-wise. When $f_t \approx 1$, the cell remembers past information (long-term dependency preserved). When $f_t \approx 0$, past is forgotten. The multiplicative $\odot$ interaction means $c_t$ can flow across many steps with minimal decay when $f_t \approx 1$ — the key to long-range dependencies vanilla RNNs cannot capture.

---

### Q3 — Spring 2025 F

**LSTM fails to learn beyond 5 time steps. Two reasons:**

1. **Forget gate saturates to 0:** If forget gate biases are initialized poorly, the gate closes early and zeros out long-range cell states. **Solution:** Initialize forget gate biases to 1 (Jozefowicz et al., 2015) so the gate starts open.

2. **Insufficient model capacity:** Hidden state too small to encode all necessary history. **Solution:** Increase hidden state dimension, use stacked (multi-layer) LSTMs, or add attention mechanisms that directly access past states.

---

### Q4 — Spring 2025 F

| Aspect | LSTM | GRU |
|--------|------|-----|
| Gates | 3: input, forget, output | 2: reset, update |
| States | Separate $c_t$ and $h_t$ | Single $h_t$ |
| Parameters | 4 weight matrices | 3 weight matrices (~25% fewer) |
| Training speed | Slower | Faster |
| Performance | Marginally better on complex long-range tasks | Comparable on most tasks |

**Choose GRU in resource-constrained settings** because it achieves similar performance with ~25% fewer parameters and faster computation.

---

### Q5 — Spring 2025 F

**Question:** Why do vanilla RNNs suffer from vanishing gradients?

**Answer:** BPTT requires:

$$\frac{\partial h_t}{\partial h_0} = \prod_{t=1}^{T} \frac{\partial h_t}{\partial h_{t-1}} = \prod_{t=1}^{T} W_{hh}^T \cdot \text{diag}(\tanh'(\cdot))$$

Each factor has eigenvalues scaled by $W_{hh}$'s spectrum and $\tanh' \in (0,1]$. If spectral radius $< 1$: gradients decay exponentially → zero (vanishing). If $> 1$: they explode.

**Effect on long-term dependencies:** Gradients at step $T$ w.r.t. early inputs are negligibly small → the network cannot learn to use information from far back. Only recent steps (a few) are effectively trainable.

---

### Q6 — Spring 2025 F

**Question:** ReLU instead of tanh in RNN — benefits and drawbacks?

**Benefits:** ReLU gradient = 1 for $x > 0$ (no shrinkage), potentially alleviating vanishing gradient. Computationally cheaper.

**Drawbacks:**

- **Exploding gradients dominant:** Without saturation, repeated $W_{hh}$ multiplications cause unbounded growth if spectral radius $> 1$.
- **Hidden state explosion:** No upper bound on $h_t$ → numerical instability across time steps.
- **No bounded memory:** tanh's $\pm 1$ bound provides stable hidden states; ReLU has no such bound.

In practice: clip gradients and use LSTM/GRU instead.

---

### Q7 — Spring 2025 F

**BPTT derivation for $\partial L_t / \partial W_{hh}$:**

$$\frac{\partial L_t}{\partial W_{hh}} = \sum_{k=1}^{t} \frac{\partial L_t}{\partial h_t} \cdot \left(\prod_{j=k+1}^{t} \frac{\partial h_j}{\partial h_{j-1}}\right) \cdot \frac{\partial h_k}{\partial W_{hh}}$$

where $\frac{\partial h_j}{\partial h_{j-1}} = W_{hh}^T \cdot \text{diag}(1 - h_j^2)$ and $\frac{\partial h_k}{\partial W_{hh}} = h_{k-1}^T$.

The product term shows exponential decay/explosion with $t-k$, explaining vanishing/exploding gradients.

---

### Q8 — Fall 2023 F [VIP] GRU

**1. Proof: $\sigma(x) + \sigma(-x) = 1$**

$$\sigma(x) + \sigma(-x) = \frac{1}{1+e^{-x}} + \frac{1}{1+e^x} = \frac{1+e^x + 1+e^{-x}}{(1+e^{-x})(1+e^x)} = \frac{2+e^x+e^{-x}}{2+e^x+e^{-x}} = 1 \quad \square$$

**2. Update gate $z_t \approx 0$ → state not updated significantly?** **True.** $h_t = (1-z_t)h_{t-1} + z_t\tilde{h}_t \approx h_{t-1}$. The unit carries forward the previous state unchanged.

**3. Update $\approx 1$, reset $\approx 0$ → remembers past state?** **False.** When $z_t \approx 1$: $h_t \approx \tilde{h}_t$. When $r_t \approx 0$: $\tilde{h}_t = \tanh(Wx_t + r_t \odot Uh_{t-1}) \approx \tanh(Wx_t)$ — past state $h_{t-1}$ is zeroed out (reset). The unit **forgets** the past and updates entirely from new input.

**4. When to use Bidirectional RNN:** When the output depends on both past AND future context. Examples: NLP (NER, POS tagging, MT — a word's meaning depends on what follows), speech recognition. Requires the full sequence to be available at inference time (not applicable to streaming/online tasks).

---

### Q9 — Fall 2018 F

**1. RNN advantage over window-based model:** A window-based model can only see a fixed-size context of $K$ words. An RNN processes sequences of arbitrary length, theoretically capturing dependencies spanning the entire document. Critical for long sentences where sentiment depends on words far apart (e.g., complex negation, sarcasm).

**2. LSTM gradient $\partial J / \partial U^{(c)}$ (chain rule form):**

$$\frac{\partial J}{\partial U^{(c)}} = \frac{\partial J}{\partial h_t} \cdot \frac{\partial h_t}{\partial c_t} \cdot \frac{\partial c_t}{\partial \tilde{c}_t} \cdot \frac{\partial \tilde{c}_t}{\partial U^{(c)}} + \frac{\partial J}{\partial h_t} \cdot \frac{\partial h_t}{\partial c_t} \cdot \frac{\partial c_t}{\partial c_{t-1}} \cdot \frac{\partial c_{t-1}}{\partial \tilde{c}_{t-1}} \cdot \frac{\partial \tilde{c}_{t-1}}{\partial U^{(c)}}$$

**Which part mitigates vanishing gradient:** The term $\frac{\partial c_t}{\partial c_{t-1}} = f_t$. Unlike the tanh Jacobian chain in vanilla RNNs, the cell state gradient is multiplied by the forget gate value. When $f_t \approx 1$, gradients flow back through $c_t \to c_{t-1}$ with factor $\approx 1$ — no exponential decay — enabling the model to learn the long-range dependencies needed for correct sentiment classification.

---

## 11. Attention – Transformers – Autoencoders

### Q1

**Flaw of encoder-decoder without attention:** The encoder compresses the entire source sentence into a single fixed-length context vector (the final hidden state). For long sentences, this bottleneck causes information loss — the decoder cannot selectively access relevant parts of the source.

**How attention fixes it:** Instead of a single vector, attention computes a weighted combination of ALL encoder hidden states at each decoding step. The decoder dynamically retrieves relevant information from the most relevant source positions (e.g., the word being translated), eliminating the fixed-size bottleneck and dramatically improving translation quality for long sequences.

---

### Q2 — Spring 2021 F

**Using an autoencoder for denoising:**

1. **Prepare data:** Take clean images $\{x\}$. Add Gaussian noise: $\tilde{x} = x + \varepsilon$, $\varepsilon \sim \mathcal{N}(0, \sigma^2 I)$.
2. **Train:** Input noisy $\tilde{x}$, train to reconstruct clean $x$. Loss: $L = \|\hat{x} - x\|^2$.
3. **Inference:** Feed noisy image → encoder maps to latent code capturing clean structure → decoder reconstructs denoised image.

The bottleneck prevents the identity function on noise, forcing the network to learn the underlying clean signal manifold.

---

### Q3 — Spring 2025 F

**Undercomplete autoencoder:** Latent space dimension $d_z < d_x$ (input dimension). The bottleneck forces compression.

**Overcomplete autoencoder:** $d_z \geq d_x$. Without regularization, can learn the identity function (copy input verbatim) — no useful representation learned.

**Why undercomplete is useful:** The compression constraint forces the latent code to capture only the most essential structure (principal axes of variation). Analogous to PCA — learns a compact, low-dimensional manifold representation. This compact code generalizes better and is useful as a feature extractor.

---

### Q4 — Spring 2025 F

Encoder: $z = \sigma(Wx+b)$, decoder: $\hat{x} = \sigma(W'z+b')$, $L = \|x - \hat{x}\|^2$.

$$\delta_d = -2(x - \hat{x}) \odot \hat{x}(1-\hat{x}) \quad \text{(decoder delta)}$$
$$\frac{\partial L}{\partial z} = W'^T \delta_d$$
$$\delta_e = \frac{\partial L}{\partial z} \odot z(1-z) \quad \text{(encoder delta)}$$
$$\frac{\partial L}{\partial W} = \delta_e \cdot x^T \quad \text{(outer product, shape: } d_z \times d_x\text{)}$$

---

### Q5 — Spring 2025 F

**Autoencoder for anomaly detection:**

Train on normal data only. At test time, compute reconstruction error $\|x - \hat{x}\|$ for each sample:

- **Normal samples:** Resemble training data → well-reconstructed by learned latent space → **low error**.
- **Anomalies:** Structurally different → poor reconstruction → **high error**.

Threshold on reconstruction error distinguishes normal from anomalous.

**Assumptions:**
- Anomalies are rare in training (AE trained predominantly on normal data)
- Anomalies are structurally different enough to reconstruct poorly
- Latent space is compact enough not to generalize to out-of-distribution samples

---

### Q6 — Fall 2018 F (Sparse Autoencoder)

**Standard gradients:**

$$\frac{\partial J^{(i)}}{\partial W^d_{kl}} = -2(x^{(i)}_k - \hat{x}^{(i)}_k) \cdot z^{(i)}_l$$

$$\frac{\partial J^{(i)}}{\partial s^{(i)}_j} = \left[\sum_k \frac{\partial J^{(i)}}{\partial \hat{x}^{(i)}_k} W^d_{kj}\right] \cdot z^{(i)}_j(1-z^{(i)}_j)$$

$$\frac{\partial J^{(i)}}{\partial W^e_{kl}} = \frac{\partial J^{(i)}}{\partial s^{(i)}_k} \cdot x^{(i)}_l$$

**Sparse penalty gradients:** $J_\text{sparse} = J + \beta\sum_j\left[\rho\log\frac{\rho}{\hat{\rho}_j} + (1-\rho)\log\frac{1-\rho}{1-\hat{\rho}_j}\right]$ where $\hat{\rho}_j = \frac{1}{N}\sum_i z^{(i)}_j$.

$$\frac{\partial J_\text{sparse}}{\partial W^d_{kl}} = \frac{\partial J}{\partial W^d_{kl}} \quad \text{(sparsity doesn't depend on } W^d\text{)}$$

$$\frac{\partial J_\text{sparse}}{\partial W^e_{kl}} = \frac{\partial J}{\partial W^e_{kl}} + \beta\sum_j\left(-\frac{\rho}{\hat{\rho}_j} + \frac{1-\rho}{1-\hat{\rho}_j}\right)\frac{\partial \hat{\rho}_j}{\partial W^e_{kl}}$$

**Relations to PCA:**
- Both learn compact low-dimensional representations of data
- A linear AE trained with MSE learns the same subspace as PCA
- Non-linear AEs generalize PCA to non-linear manifolds
- Unlike PCA, AEs can learn overcomplete and sparse representations

---

## 12. GAN Related

### Q1 — Fall 2021 F, Summer 2022 F, Fall 2023 F

**1. Early in training — D(G(z)) closer to 0 or 1?**

**Closer to 0.** The generator produces noise-like outputs, obviously fake. The discriminator easily learns to classify them as fake → $D(G(z)) \to 0$.

**2. Which cost function?**

**Non-saturating cost:** $J^{(G)} = -\frac{1}{m_g}\sum \log(D(G(z^{(i)})))$

With the saturating cost $\log(1-D(G(z)))$: when $D(G(z)) \approx 0$ early in training, gradient $\approx 0$ → generator receives no useful signal. The non-saturating cost gives large gradient when $D(G(z))$ is small — exactly when the generator most needs to learn.

**3. GAN trained when D(G(z)) ≈ 1?** **False.** At equilibrium, the optimal discriminator assigns equal probability to real and fake: $D^*(x) = 0.5$ everywhere. $D(G(z)) \approx 0.5$ signals convergence, not $\approx 1$.

---

### Q2 — Spring 2021 F

**1. Cost function for generator in practice:**

$$J^{(G)} = -\frac{1}{m_g}\sum_{i=1}^{m_g}\log(D(G(z^{(i)})))$$

**2. Why not $J^G = -J^D$?**

The minimax generator loss $\log(1-D(G(z)))$ **saturates early in training** when $D$ easily detects fakes ($D(G(z)) \approx 0$) → gradient $\approx 0$ → generator cannot improve. The non-saturating version $-\log(D(G(z)))$ provides large gradient when $D(G(z))$ is small — the critical period when the generator most needs to update.

---

### Q3 — Spring 2025 F

**GAN minimax objective:**

$$\min_G \max_D V(D,G) = \mathbb{E}_{x \sim p_\text{data}}[\log D(x)] + \mathbb{E}_{z \sim p_z}[\log(1-D(G(z)))]$$

**Discriminator $D$:** Maximizes $V$ — assigns $D(x) \to 1$ for real, $D(G(z)) \to 0$ for generated. Goal: correctly classify real vs fake.

**Generator $G$:** Minimizes $V$ — makes $D(G(z)) \to 1$ to fool the discriminator. Goal: generate indistinguishable samples.

**Why zero-sum:** $J^D + J^G = 0$ in the minimax formulation. Every gain for $D$ is a loss for $G$ — the game is purely competitive with no cooperative component.

---

### Q4 — Spring 2025 F

**Proof: optimal discriminator $D^*(x) = \frac{p_\text{data}(x)}{p_\text{data}(x) + p_g(x)}$**

For fixed $G$, maximize $V$ over $D$ pointwise:

$$V = \int \left[p_\text{data}(x)\log D(x) + p_g(x)\log(1-D(x))\right]dx$$

Maximize integrand $f(D) = a\log D + b\log(1-D)$ where $a = p_\text{data}(x)$, $b = p_g(x)$:

$$\frac{df}{dD} = \frac{a}{D} - \frac{b}{1-D} = 0 \implies a(1-D) = bD \implies D^* = \frac{a}{a+b} = \frac{p_\text{data}(x)}{p_\text{data}(x)+p_g(x)} \quad \square$$

---

### Q5 — Spring 2025 F

**Why $-\log(D(G(z)))$ instead of $\log(1-D(G(z)))$?**

Early in training, $D$ is strong and $D(G(z)) \approx 0$:

| Loss | Gradient when $D(G(z)) \to 0$ |
|------|-------------------------------|
| $\log(1-D(G(z)))$ | $\approx \nabla_G \log(1) = 0$ — **flat, no signal** |
| $-\log(D(G(z)))$ | **Large gradient** — strong learning signal |

The non-saturating objective provides **large gradients precisely when the generator is weakest**, enabling effective early learning. Both share the same Nash equilibrium, but non-saturating converges much more reliably in practice.

---

### Q6 — Spring 2022 F

**Primary goal of the discriminator:**

Maximize $P(\text{real}|x)$ — correctly classify real vs generated samples. Probabilistically: estimate $P(y=\text{real}|x) = D(x)$, aiming for $D(x) \approx 1$ for $x \sim p_\text{data}$ and $D(G(z)) \approx 0$ for generated samples.

---

### Q7 — Spring 2022 F

**When GAN is fully trained, $D(G(z))$ is close to:**

**0.5.** At equilibrium $p_g = p_\text{data}$, so:

$$D^*(x) = \frac{p_\text{data}(x)}{p_\text{data}(x) + p_g(x)} = \frac{p_\text{data}(x)}{2p_\text{data}(x)} = 0.5$$

The discriminator is maximally uncertain — it cannot do better than random guessing between real and fake.

---

*End of ML-Zytona Complete Exam Answer Sheet*
