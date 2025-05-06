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

### Gemini 2.5 Flash
Used in the refinement models. This was chosen mainly because of its Thinking capability. 

#### Linear Refinement
In the `linear-refinement` implementation, the process was broken into 4 steps using a multi-turn conversation interface. 

- Generate a brief guideline about the answer format and answer information
- Generate a primary code based on that guideline
- Go through 2 more iterations to review and refine each intermediate code
- Execute the final code

I could not evaluate the whole dataset with this implementation because of rate limits. As, it's now using around 6 API calls per question. But I have run this over some of the previously wrong answers, the model got, on average, more than 50% of those previously wrong answers correct this time.

#### MCTS Refinement
I have taken help and inspiration from these two papers: 
- https://arxiv.org/abs/2412.18319
- https://arxiv.org/abs/2406.07394

My implementation is still not ready and I will update the repository once I have a working implementation tested.

## Important

After testing and reviewing, I noticed there are incorrect answers in the `answer_list.txt` file provided. For example,
- 128th question asks for 3 values but the provided answer lists only 1.
- 129th question incorrectly gives [15, 5] while the dataset is clearly [12, 8]
- 132th question asks for 4 values but the provided answer lists only 1.

There are more like these.

So, in reality, the accuracy is higher than mentioned here but we can't just verify it as the full correct anwers key list is not available.

## Observation
In some cases, the model hallucinates badly and it cannot identify mistake in refinement iterations.
