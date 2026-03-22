# Gradient Descent Visualization — animint2

An interactive visualization of the Gradient Descent algorithm built with [animint2](https://github.com/tdhock/animint2) for the GSoC 2026 application.

**Live demo:** https://Nishita-shah1.github.io/animint-viz/

---

## What this shows

The visualization has three linked interactive plots:

**Plot 1 — |Gradient| vs Iteration**
Shows how the magnitude of the gradient shrinks toward zero as the algorithm converges. Click any bar to jump to that iteration.

**Plot 2 — Loss Landscape**
Shows the function curve `f(x) = x² + 2sin(2x)` with the current position marked as a teal dot and the step arrow in orange. Faint dots show all previously visited positions so you can see the full path.

**Plot 3 — Loss vs Iteration (log scale)**
Shows how the loss value decreases across iterations on a log scale so small changes in later iterations are clearly visible.

All three plots are linked — clicking a bar in Plot 1 or Plot 3 updates the position shown in Plot 2. The animation plays automatically at 800ms per iteration.

---

## Function details

```
f(x)  = x² + 2sin(2x)       # loss function
f'(x) = 2x + 4cos(2x)       # gradient

Starting point: x = 2.5
Learning rate:  0.02
Iterations:     30
```

---

## How it was built

The visualization translates the iterative gradient descent loop into data.frames which are then passed to animint2 ggplots:

- `curve_df` — 300-point grid of the function curve
- `point_df` — one row per iteration storing x, loss, and gradient values
- `arrow_df` — one row per step storing start and end coordinates for the step arrow
- `label_df` — one row per iteration storing formatted label text

animint2-specific features used:
- `clickSelects = "iteration"` — makes the tall rectangles clickable
- `showSelected = "iteration"` — shows only the selected iteration's point/arrow/label
- `time = list(variable = "iteration", ms = 800)` — drives auto-playback

---

## Source

- Source code: [figure-combined.R](https://github.com/Nishita-shah1/animint/blob/main/figure-combined.R)
- Part of GSoC 2026 application for the [animint2](https://github.com/tdhock/animint2) project
- Original animation package function: [animation::grad.desc()](https://yihui.org/animation/example/grad-desc/)

---

## How to run locally

```r
install.packages("remotes")
remotes::install_github("tdhock/animint2")

library(animint2)
# source the script
source("figure-combined.R")
```
