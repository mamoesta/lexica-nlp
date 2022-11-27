# lexica-nlp
The goal of this project is develop a named-entity-recognition model that can identify artist names from prompts.
Some novel applications of this model:
* Prompt optimization: Artist names are analyzed against prompt outputs to determine optimal artist names and locations in a prompt
* A model like this begins to attribute "credit" to the various artist's work who were included in the prompt. The concern of attribution for artists in prompts is an unresolved issue. A model like enables the conversation to continue.

See `./main.ipynb` for a walkthrough. This is an e2e project:

* Generate random search strings to poll [lexica.art](https://lexica.art/) API to bootstrap a dataset of prompts. I developed this project before the larger HF dataset became available.
* Query Lexica serach API and deal with rate limiting. Store prompts and image URL.
* Use [Label Studio](https://labelstud.io/) to annotate ~ 230 prompts to identify artist's name.
* Experiment: Use BART outputs to generate weak labels for the remaining 19k collected datapoints. Note: Fine-tuning a transformer model with 230 ground truth generated strong enough performance such that weak labels did not prove necessary for this proof-of-concept.
* Concat label studio GT with prompts dataframe. Convert dataframe --> spacy Docs to prepare for training.
* Train model
* Import an evaluation set of prompts from a [huggingface](https://huggingface.co/) dataset. Generate predictions for HF prompts.
* Eval set predictions @ `./eval/entities.html`
* You can review model predictions on holdout data [here](https://htmlpreview.github.io/?https://github.com/mamoesta/lexica-nlp/blob/main/eval/entities.html)
