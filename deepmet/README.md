# Data for the DeepMETProducer in the CMSSW [RecoMET/METPUSubtraction](https://github.com/cms-sw/cmssw/tree/master/RecoMET/METPUSubtraction) package

### Model v1

The current and first training version is `_v1_`.
Models are trained for different conditions (2016, 2018, and phase 2) and either with a response term in the loss (`_resp_`) or without. For 2016 conditions, only a training with response term in the loss is provided.
All momentum inputs and outputs are scaled by `1/norm` with `norm = 50`. The model files are accessible in CMSSW via `RecoMET/METPUSubtraction/data/deepmet`.

Links to CMS-internal information giving more details on the model and the trainings are provided in the following presentation: https://indico.cern.ch/event/918058/#264-deep-met-producer

The models take the following inputs:

- `"input"`: Input tensor with dimension `batch x n_max_pf x 8 (features)`. `n_max_pf = 4500` for run 2 (`_2016`, `_2018`) and `n_max_pf = 12500` for phase 2 (`_phase2`). The features for each PF candidate are `dxy`, `dz`, `eta`, `mass`, `pt`, `puppiWeight`, `px`, `py`.
- `"input_cat{i}"` (with i from {0, 1, 2}): Input tensor with dimension `batch x n_max_pf x 1 (single embedded feature)`. These are for categorical embeddings of the integer inputs `charge`, `pdgId`, and `fromPV`.

The relevant output is:
- `"output/BiasAdd"`: Output tensor with dimension `batch x 2`, giving the missing px and py values (to be scaled by `norm`)
