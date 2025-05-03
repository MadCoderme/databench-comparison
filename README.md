# databench-comparison
This repository contains attempt notebooks and results for this competition: https://www.codabench.org/competitions/3360/

The python package `databench-eval` has an `Evaluator` which seems to have some problems. So, the accuracy mentioned was tested externally and should not be considered without proper verification. 
Models below were run without fine-tuning and over the lite datasets.

## Outputs

### Llama-3.1 8B - Instruct
Primary attempt. Its performance somehow got worse after around 40 questions. The accuracy was not that good. Needs further testing and tweaks.

### Qwen-2.5 7B - Instruct
In different benchmarks, this model has better coding capability than llama 3.1 8b. Interestingly, its performance also got worse after around 40 questions. Based on this observation, this **might be** because the questions coming up later has tasks that doesn't fit well with the prompt and small models.

It yielded around ~63.7% accuracy.

### Gemini 2.0 Flash
Used through the API. This model had quite consistent performance. But ultimately yielded ~74.3% accuracy in primary attempt.

After improving the prompt, the code errors were mostly gone and the accuracy increased to ~84.67%.

## Observation
Observing the predictions, majority of the wrong results was just errors while running the generated code. Prompt engineering helped to fix most of them. For further improvement, while fine tuning may help the smaller models, Gemini 2.0 Flash should be able to provide more accurate predictions itself.

Since, the official evaluator could not be used, there can be incorrect answers in the `answers_lite.txt` file which was used to calculate accuracy externally.
