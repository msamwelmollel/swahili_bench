# Swahili ARC Evaluation

This guide provides step-by-step instructions for running the Swahili ARC evaluation using the lm-evaluation-harness.

## Steps to Run the Evaluation

1. **Clone the lm-evaluation-harness repository:**

    ```bash
    !git clone https://github.com/EleutherAI/lm-evaluation-harness
    %cd lm-evaluation-harness
    !pip install -e .
    ```

2. **Create a directory for swahili_bench inside tasks:**

    ```bash
    !mkdir ../lm-evaluation-harness/lm_eval/tasks/swahili_bench
    ```

3. **Clone the swahili_bench repository:**

    ```bash
    %cd ..
    !git clone https://github.com/msamwelmollel/swahili_bench
    ```

4. **Move to the swahili_bench directory:**

    ```bash
    %cd swahili_bench/swahili_bench
    ```

5. **Move all contents from swahili_bench to the newly created swahili_bench directory inside lm-evaluation-harness/tasks:**

    ```bash
    !mv * ../../lm-evaluation-harness/lm_eval/tasks/swahili_bench
    ```

6. **Change back to the lm-evaluation-harness directory:**

    ```bash
    %cd ../../lm-evaluation-harness
    ```

7. **Run the evaluation:**

    ```bash
    !lm_eval --model hf \
        --model_args pretrained='sartifyllc/sartify_gemma2-2B-16bit' \
        --tasks arc_challenge_swh  \
        --device cuda:0 \
        --batch_size auto:4
    ```

Follow these steps to set up and run the Swahili ARC evaluation.

#run vllm
```python 
import os
import subprocess

os.environ["CUDA_VISIBLE_DEVICES"] = "1"

model_name = "model_output/gemma2b"

command = (
    "lm_eval --model vllm --model_args "
    f'pretrained={model_name},tensor_parallel_size=1,dtype=bfloat16,'
    "gpu_memory_utilization=0.5 --tasks arc_challenge_swh --batch_size 1"
)

subprocess.run(command, shell=True)
```
