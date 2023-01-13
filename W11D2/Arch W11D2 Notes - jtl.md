# Arch W11D2 Notes

## Branch Prediction

#### 2-bit dynamic prediction

change prediction only if misprediction twice

#### Correlation Branches

different branch instruction may hash to same 2-bit predictor

solution: four predictors for each hash value, use the behavior of previous 2 branches to determine which to choose. 

#### Tournament Predictor

a 2-bit counter to choose among

- global predictor
  - 4k entries, indexed by history of  last 12 branches
- local predictor
  - 1024 10-bit entries: last 10 outcomes of the entry

#### BHT & BTB

branch history table : help to make prediction

branch target buffer : jump to predicted position quickly

#### Special Case

JALR hard to predict address