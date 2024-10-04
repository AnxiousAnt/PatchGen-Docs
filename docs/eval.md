# Model Evaluation and Performance Metrics

To evaluate the performance of the **PatchGen** model, we use several key metrics, which provide insights into the time spent generating a response and the speed of token generation. Below is an example of how these metrics are captured during a single interaction with the model.

### Test Case
**Prompt**: ```Create a Pure Data patch that calculates the absolute value of a given negative number.```

**Response**:
```Sure! Here's the patch you requested:\n\n#N canvas 862 168 534 384 10;\n#X text 120 40 calculate the absolute value of -12;\n#X obj 210 70 bng 15 250 50 0 empty empty empty 17 7 0 10 #fcfcfc #000000 #000000;\n#X msg 200 110 -12;\n#X obj 207 152 abs;\n#X floatatom 207 179 0 0 0 0 - - -;\n#X text 80 202 [abs] will output the absolute value of a number.;\n#X connect 1 0 2 0;\n#X connect 2 0 3 0;\n#X connect 3 0 4 0;\n\n\nexplanation: This patch takes an input number (-12 in this case), passes it through an absolute value object ([abs]), and outputs the result (12) as a floating-point number."```

### Performance Metrics

- **Model**: `patch-gen-4b`
- **GPU**: `GTX-1650 (4GB)`
- The following performance metrics were recorded during this generation.

| Metric                | Description                                                                                       | Value                    |
| --------------------- | ------------------------------------------------------------------------------------------------- | ------------------------ |
| **Total Duration**     | Total generation time.                                                                           |51606577300 or 51.6 seconds|
| **Load Duration**      | Time in nanoseconds spent loading the model.                                                      |7730916900 or 7.73 seconds |
| **Prompt Eval Count**  | Number of tokens in the prompt.                                                                   | 21 tokens                 |
| **Prompt Eval Duration** | Time in nanoseconds spent evaluating the prompt.                                                 |1249035000 or 1.25 seconds|
| **Eval Count**         | Number of tokens in the response.                                                                 | 285 tokens                |
| **Eval Duration**      | Time in nanoseconds spent generating the response.                                                |42607315000 or 42.6 seconds|

### Token Generation Speed
To determine the speed of the token generation, we use the formula: <br/>
`Token Generation Speed (tokens/second) = eval_count / eval_duration * 10^9`<br/>
For this specific example:<br/>
`Token Generation Speed = 285 tokens / 42.6 seconds * 10^9=`**`6.69 tokens/second`**


### Summary of Model Evaluation

The **PatchGen** model, running on a **GTX 1650 (4GB VRAM)**, generated a response for the prompt `"Create a Pure Data patch that calculates the absolute value of a given negative number"` in approximately **42.6 seconds**, producing **285 tokens** at a rate of around **6.69 tokens per second**. The prompt itself consisted of **21 tokens** and took **1.25 seconds** to evaluate.

These performance metrics give us insight into the model's efficiency, helping us understand its response generation speed and where time is spent during inference.
