# **Benchmark Integrity Policy**



REAL-AI-Benchmark is designed to evaluate reasoning, perception, numerical

discipline, code generation, and reproducibility.



## Public benchmark files must not contain


\- reference answers;

\- expected final actions;

\- expected action indices;

\- hidden numeric gold outputs;

\- private tolerances;

\- evaluator-only tie-breaking conclusions;

\- text-only duplicates of visual benchmark instances;

\- filenames or comments that reveal the intended answer.




## Public benchmark files may contain


\- full problem statements;

\- formulas;

\- public scoring categories;

\- required output schemas;

\- allowed action names;

\- allowed output labels;

\- neutral examples;

\- independent control variants.



## GO-6 rule



The GO-6 textual no-VI instance is an independent control variant and must not be

treated as numerically equivalent to the visual GO-6 instance.



## Evaluation principle



A valid solution must derive its final answer from the data provided in the

specific benchmark instance, not from repository history, previous public

solutions, external discussions, or memorized answer patterns.

