# Mandarin-Digit-Asr
Digital Speech Processing hw 2-1

**TOC**

* [Baseline](#Baseline)
* [Result](#Result)
* [Analysis](#Analysis)
  * [States](#States)
  * [Iteration](#Iteration)
  * [Numgauss & Totgauss](#Numgauss & Totgauss)
  * [Opt_acwt](#Opt_acwt)
  * [Test_beam](#Test_beam)


## Baseline

- State :

  - NONSILENCEPHONES - 4 states
  - SILENCEPHONES - 4 states

- Train parameters :

  - numiters=5                                    # Number of iterations of training
    maxiterinc=4                                  # Last iter to increase #Gauss on.
    numgauss=1                                    # Initial num-Gauss (must be more than #states=3*phones).
    totgauss=5                                    # Target #Gaussians.
    incgauss=$[($totgauss-$numgauss)/$maxiterinc] # per-iter increment for #Gauss
    realign_iters="1 2 3 4 5";
    scale_opts="--transition-scale=1.0 --acoustic-scale=0.1 --self-loop-scale=0.1"

- Test parameters :

  - opt_acwt=0.87
    test_beam=15.0

## Result

**Accuracy = 95.45 %**

- State :

  - NONSILENCEPHONES - 12 states
  - SILENCEPHONES - 2 states

- Train parameters :

  - numiters=5                                    # Number of iterations of training
    maxiterinc=4                                  # Last iter to increase #Gauss on.
    numgauss=1                                    # Initial num-Gauss (must be more than #states=3*phones).
    totgauss=5                                    # Target #Gaussians.
    incgauss=$[($totgauss-$numgauss)/$maxiterinc] # per-iter increment for #Gauss
    realign_iters="1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20";
    scale_opts="--transition-scale=1.0 --acoustic-scale=0.1 --self-loop-scale=0.1"

- Test parameters :

  - opt_acwt=0.87
    test_beam=50.0



## Analysis

### States

**Using baseline model as basic model below**

基本上state的複雜度可以對應到我們訓練model的複雜度，也就是當我們訓練資料較為困難時，我們的model便會越複雜，因此實驗也很合理的調整state會使accuracy上升，但會有個極限值，再上去accuracy就會下降了。

| number of State<br />(NONSILENCEPHONES/SILENCEPHONES) | 4/4   | 8/4   | 12/4  | 16/4  |
| ----------------------------------------------------- | ----- | ----- | ----- | ----- |
| Accuracy                                              | 73.5% | 83.4% | 82.4% | 80.7% |
| number of State<br />(NONSILENCEPHONES/SILENCEPHONES) | 12/2  | 12/4  | 12/6  | 12/8  |
| Accuracy                                              | 85.2% | 82.4% | 80.3% | 43.6% |

### Iteration

**Using baseline model as basic model below (with state=12)**

| Iteration | 5     | 10   | 15   | 20   |
| ----------------------------------------------------- | ----- | ---- | ---- | ---- |
| Accuracy                                              | 85.2% | 83.19% | 82.14% | 82.4% |

### Numgauss & Totgauss

**Using baseline model as basic model below (with state=12)**

| Numgauss   | 1     | 5     | 20    | 50    | 100   |
| ---------- | ----- | ----- | ----- | ----- | ----- |
| Maxiterinc | 4     | 5     | 10    | 15    | 15    |
| Totgauss   | 5     | 5     | 20    | 50    | 100   |
| Accuracy   | 85.2% | 85.2% | 85.2% | 85.2% | 85.2% |

### Opt_acwt

**Using baseline model as basic model below (with state=12)**

| Opt_acwt | 0.1    | 0.2    | 0.4   | 0.65   | 0.87  | 0.9    | 0.95   |
| -------- | ------ | ------ | ----- | ------ | ----- | ------ | ------ |
| Accuracy | 93.44% | 94.93% | 92.80 | 88.37% | 85.2% | 84.69% | 83.88% |

### Test_beam

**Using baseline model as basic model below (with state=12)**

| Test_beam | 15    | 40     | 60     | 100    | 150    |
| --------- | ----- | ------ | ------ | ------ | ------ |
| Accuracy  | 85.2% | 94.59% | 95.34% | 95.22% | 95.34% |

