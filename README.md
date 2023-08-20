# OpenEval
Another dataset for evaluating competition-level code generation.

## Introduction

We present the OpenEval dataset, a collection of 178 function-level programming problems sourced from open-source programming competition websites. This dataset serves as a resource for evaluating the functional correctness of LLMs in code generation tasks. 

*OpenEval can be considered as a complementary version of the HumanEval dataset.*

## Construct

Each problem in OpenEval includes a function signature, a documentation string, and a code body, with five test cases per problem.

To ensure consistency between the documentation strings and the code body, we employ open-ai's GPT3.5 interface in a few-shot method to generate the corresponding documentation strings. These generated strings are then manually reviewed to ensure their quality.

Furthermore, we take precautions to prevent test case leakage from affecting model performance by excluding test cases from the model input prompt.

## Use

Used exactly the same way as [HumanEval](https://github.com/openai/human-eval).

## Evaluation Results

| Model Name | Model Size | Pass@1 |
| ---------- | ---------- | ------ |
| CodeGen    | 350M       | 8.989  |
|            | 2B         | 14.607 |
|            | 6B         | 19.663 |
| StarCoder  | 1B         | 8.989  |
|            | 3B         | 12.360 |
|            | 7B         | 21.348 |
| CodeT5+    | 220M       | 7.303  |
|            | 770M       | 10.674 |
|            | 2B         | 16.292 |
|            | 6B         | 21.910 |

## Example

```python
{
	"task_id": "Open/0", 
	"prompt": "def validPosition ( arr , N , K ) :
    \"\"\"Write a function that takes in an array, the length of the array, and a number K.
    The function calculates the sum of all the elements in the array.
    Then, it checks each element in the array and counts how many elements, when increased by K, would be greater than the sum of all the other elements in the array.
    Finally, the function returns the count.
    \"\"\"
    ", 
    "entry_point": "validPosition", 
    "canonical_solution": "    count = 0 ; sum = 0 ;\n    for i in range ( N ) :\n        sum += arr [ i ] ;\n    for i in range ( N ) :\n        if ( ( arr [ i ] + K ) > ( sum - arr [ i ] ) ) :\n            count += 1 ;\n    return count ;\n", 
    "test": "
    METADATA = {
        'author': 'yg',
        'dataset': 'test'
    }
    
    def check(candidate):
    # test case 1
    arr = [1, 2, 3, 4, 5]
    N = 5
    K = 2
    assert candidate(arr, N, K) == 0
    
    # test case 2
    arr = [1, 2, 3, 4, 5]
    N = 5
    K = 10
    assert candidate(arr, N, K) == 3
    
    # test case 3
    arr = [1, 1, 1, 1]
    N = 4
    K = -2
    assert candidate(arr, N, K) == 0
    
    # test case 4
    arr = [1, 1, 1, 1]
    N = 4
    K = 4
    assert candidate(arr, N, K) == 4
    
    # test case 5
    arr = []
    N = 0
    K = 4
    assert candidate(arr, N, K) == 0"
}
```

## Citation

Please cite using the following bibtex entry:

```
@misc{openeval,
  author = {Guang Yang},
  title = {OpenEval: Another dataset for evaluating competition-level code generation},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/NTDXYG/open-eval}},
}
```

