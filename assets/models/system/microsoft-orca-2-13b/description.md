## **Microsoft Orca-2 13b**

Orca 2 is a finetuned version of LLAMA-2. Orca 2’s training data is a synthetic dataset that was created to enhance the small model’s reasoning abilities. All synthetic training data was moderated using the Microsoft Azure content filters. More details about the model can be found in the [Orca 2 paper](https://arxiv.org/pdf/2311.11045.pdf).

### Intended Uses

Orca 2 is built for research purposes only and provides a single turn response in tasks such as reasoning over user given data, reading comprehension, math problem solving and text summarization. The model is designed to excel particularly in reasoning.

**Out of scope**

* This is a research model, intended to show that we can use capable models and complex workflows (advanced prompts, multiple calls) to create synthetic data that can teach Small Language Models (SLMs) new capabilities. We chose reasoning because it is a widely useful capability that SLMs lack.

* The model is not optimized for chat and has not been trained with RLHF or DPO. It is best used after being finetuned for chat or for a specific task.

* Beyond reasoning, the model inherits capabilities and limitations of its base (LLAMA-2 base). We have already seen that the benefits of the Orca training can be applied to other base model too.

### Limitations

Orca 2, built upon the LLaMA 2 model family, retains many of its limitations, as well as the common limitations of other large language models or limitation caused by its training process, including:

* **Data Biases:** Large language models, trained on extensive data, can inadvertently carry biases present in the source data. Consequently, the models may generate outputs that could be potentially biased or unfair.
* **Lack of Contextual Understanding:** Despite their impressive capabilities in language understanding and generation, these models exhibit limited real-world understanding, resulting in potential inaccuracies or nonsensical responses.
* **Lack of Transparency:** Due to the complexity and size, large language models can act as “black boxes”, making it difficult to comprehend the rationale behind specific outputs or decisions. We recommend reviewing transparency notes from Azure for more information.
* **Content Harms:** There are various types of content harms that large language models can cause. It is important to be aware of them when using these models, and to take actions to prevent them. It is recommended to leverage various content moderation services provided by different companies and institutions. On an important note, we hope for better regulations and standards from government and technology leaders around content harms for AI technologies in future. We value and acknowledge the important role that research and open source community can play in this direction.
* **Hallucination:** It is important to be aware and cautious not to entirely rely on a given language model for critical decisions or information that might have deep impact as it is not obvious how to prevent these models from fabricating content. Moreover, it is not clear whether small models may be more susceptible to hallucination in ungrounded generation use cases due to their smaller sizes and hence reduced memorization capacities. This is an active research topic and we hope there will be more rigorous measurement, understanding and mitigations around this topic.
* **Potential for Misuse:** Without suitable safeguards, there is a risk that these models could be maliciously used for generating disinformation or harmful content.
* **Data Distribution:** Orca 2’s performance is likely to correlate strongly with the distribution of the tuning data. This correlation might limit its accuracy in areas underrepresented in the training dataset such as math, coding, and reasoning.
* **System messages:** Orca 2 demonstrates variance in performance depending on the system instructions. Additionally, the stochasticity introduced by the model size may lead to generation of non-deterministic responses to different system instructions.
* **Zero-Shot Settings:** Orca 2 was trained on data that mostly simulate zero-shot settings. While the model demonstrate very strong performance in zero-shot settings, it does not show the same gains of using few-shot learning compared to other, specially larger, models.
* **Synthetic data:** As Orca 2 is trained on synthetic data, it could inherit both the advantages and shortcomings of the models and methods used for data generation. We posit that Orca 2 benefits from the safety measures incorporated during training and safety guardrails (e.g., content filter) within the Azure OpenAI API. However, detailed studies are required for better quantification of such risks.

This model is solely designed for research settings, and its testing has only been carried out in such environments. It should not be used in downstream applications, as additional analysis is needed to assess potential harm or bias in the proposed application.

**Training:**

**Model**

* Architecture: a finetuned version of LLAMA-2
* Dataset size: ~817K training instances
* Training: trained with progressive learning, with
subsets of data obtained from combining the original FLAN annotations, Orca 1 dataset
and the Orca 2 dataset
* GPUs: 32 NVIDIA A100 GPUs with 80GB memory with bfloat16
* Training time: ~17 hours to train Orca 2 on FLAN dataset for one epoch,
~40 hours to train on 5 million ChatGPT data for 3 epochs and ~23 hours to continue
training on ~1.8 million GPT-4 data for 4 epochs

**License:**

Orca 2 is licensed under the [Microsoft Research License](https://huggingface.co/microsoft/Orca-2-13b/blob/main/LICENSE).

Llama 2 is licensed under the [LLAMA 2 Community License](https://ai.meta.com/llama/license/), Copyright © Meta Platforms, Inc. All Rights Reserved.

### Sample inputs and outputs (for real-time inference)

#### Sample input
```json
{
	  "input_data": {
	    "input_string": [
	      "<|im_start|>system\nYou are Orca, an AI language model created by Microsoft. You are a cautious assistant. You carefully follow instructions. You are helpful and harmless and you follow ethical guidelines and promote positive behavior.<|im_end|>\n<|im_start|>user\nHow can you determine if a restaurant is popular among locals or mainly attracts tourists, and why might this information be useful?<|im_end|>\n<|im_start|>assistant"
	    ]
	  }
}
```

#### Sample output
```json
{
  "output": [
    "<|im_start|>system You are Orca, an AI language model created by Microsoft. You are a cautious assistant. You carefully follow instructions. You are helpful and harmless and you follow ethical guidelines and promote positive behavior.<|im_end|> <|im_start|>user How can you determine if a restaurant is popular among locals or mainly attracts tourists, and why might this information be useful?<|im_end|> <|im_start|>assistant There are different ways to find out if a restaurant is popular among locals or mainly attracts tourists, and some of them are: - Checking online reviews and ratings from platforms like Yelp, TripAdvisor, or Google Maps. These sources can give you an idea of how satisfied customers are with the food, service, and atmosphere of the restaurant, as well as how busy it is and how long the wait times are. - Looking for local recommendations from friends, colleagues, or neighbors who live in the area. They can share their personal experiences and opinions about the restaurant, and also suggest other places to try that might appeal to you. - Visiting the restaurant during off-peak hours or days, when it is less likely to be crowded or noisy. You can observe how the staff and customers interact, and how attentive and friendly they are. You can also try the dishes yourself and see if they match your taste and expectations. - Asking the staff or the host about the origin and popularity of the restaurant. They can tell you if they are a local or a chain establishment, and how long they have been in business. They can also give you some insights into the target audience and the specialties of the restaurant. Knowing if a restaurant is popular among locals or mainly attracts tourists can be useful for several reasons, such as: - Saving time and money. If you are looking for a place to eat that is convenient, affordable, and satisfying, you might prefer a restaurant that is frequented by locals, as they tend to offer better quality, variety, and value for their dishes. You might also avoid the hassle and disappointment of waiting in long lines, being rushed, or paying a high price for mediocre food. - Enhancing your cultural and social experience. If you are interested in learning more about the local culture, cuisine, and lifestyle, you might want to try a restaurant that is popular among locals, as they can offer you a more authentic and diverse range of dishes, flavors, and ingredients. You might also have a chance to interact with the locals, hear their stories, and share your own. - Avoiding tourist traps and scams. If you are wary of being overcharged, over-serviced, or over-sold by unscrupulous operators, you might want to avoid restaurants that are mainly targeting tourists, as they can have lower standards, lower quality, and higher prices. You might also be exposed to unpleasant or unsafe situations, such as crowded, noisy, or dirty environments, or dishes that are poorly prepared, expired, or contaminated."
  ]
}
```

#### Sample input with parameters
```json
{
  "input_data": {
    "input_string": [
      "<|im_start|>system\nYou are Orca, an AI language model created by Microsoft. You are a cautious assistant. You carefully follow instructions. You are helpful and harmless and you follow ethical guidelines and promote positive behavior.<|im_end|>\n<|im_start|>user\nHow can you determine if a restaurant is popular among locals or mainly attracts tourists, and why might this information be useful?<|im_end|>\n<|im_start|>assistant"
    ],
    "parameters": {
      "top_p": 0.9,
      "temperature": 0.6,
      "max_new_tokens": 120,
      "do_sample": true,
      "return_full_text": false
    }
  }
}
```

#### Sample output
```json
{
  "output": [
    " There are different ways to determine if a restaurant is popular among locals or mainly attracts tourists, such as: - Looking at online reviews and ratings from different sources, such as Yelp, TripAdvisor, Google, etc. If a restaurant has mostly positive reviews from locals who live nearby or frequent the area, it might indicate that it is popular among locals. If a restaurant has mostly positive reviews from tourists who visited once or rarely come back, it might indicate that it is mainly attracts tourists. - Asking locals for their"
  ]
}
```