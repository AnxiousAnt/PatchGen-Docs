# Some Insights on the collected / curated data for model training
## Sunburst Chart Visualization

<iframe width="800" height="800" seamless="seamless" scrolling="yes" src="output-101.html"></iframe>

This sunburst chart visualizes the distribution of instruction verbs and their associated objects in the training dataset for generating Pd patches.

### Structure of the Plot:
- **Inner Circle**: Represents the root verbs extracted from the instructions (e.g., *create*, *generate*).
- **Outer Circle**: Displays the direct objects related to these verbs (e.g., *patch*, *metro*, *counter*).
- **Hierarchical View**: Each segment represents a unique combination of a root verb and its direct object, offering a hierarchical view of the structure of instructions in the dataset.
  
### How to Interpret the Plot:
1. **Root Verbs**:
   - The size of each segment in the inner circle represents the relative frequency of each root verb in the dataset.
   - For example, if *create* occupies a large portion of the circle, it indicates that a majority of instructions start with this verb.
   
2. **Direct Objects**:
   - The outer circle segments show the distribution of objects for each root verb.
   - A larger segment indicates a common verb-object combination in the dataset.

### Insights:
This visualization helps analyze the structure and diversity of the natural language instructions in the dataset. 

## Word Cloud Visualizations

### 1. Word Cloud for 'Prompts'
![Word Cloud for 'Prompts'](_images\word-cloud-prompt.png)

This word cloud highlights the most frequent terms used in the **'prompt'** column of the dataset. The dataset consists of natural language instructions aimed at generating Pd patches. Here are some key insights:

- **Dominant Terms**: 
  - **"Pure Data"** and **"patch"** are the most frequently mentioned words, which makes sense given the context of the dataset, where each instruction revolves around creating patches.
  - Other common words include **"create"**, **"generate"**, and **"output"**, emphasizing that the prompts frequently involve creating audio, math or signal-related patches.
  
- **Key Themes**: 
  - The dataset instructions seem to frequently include tasks around **signal processing** (e.g., **"frequency"**, **"audio"**, **"control"**), and handling **input/output** operations (e.g., **"input"**, **"output"**, **"print"**).
  
This word cloud serves as a visual summary, reflecting the emphasis on signal manipulation, patch generation, and data handling in the instructions.

### 2. Word Cloud for 'Explanations'
![Word Cloud for 'Explanation'](_images\word-cloud-explanation.png)

This word cloud is based on the **'explanation'** column, which provides detailed descriptions of the functionalities or operations the Pd patches are expected to perform.

- **Dominant Terms**: 
  - **"object"** and **"patch"** are the most prominent, reflecting the use of objects within Pure Data patches as key elements of the instructions.
  - Other frequent words include **"output"**, **"signal"**, **"input"**, and **"value"**, all of which are essential elements in describing the behavior and design of audio or signal-based patches.
  
- **Key Themes**: 
  - There is a strong focus on **signal processing** (e.g., **"audio signal"**, **"frequency"**, **"control"**) and object-oriented manipulation within Pd (e.g., **"object"**, **"inlet"**, **"outlet"**).
  - The explanations also emphasize various operations and result-based actions (e.g., **"trigger"**, **"generate"**, **"send"**, **"display"**).

This visualization helps understand the technical language used to describe the actions and operations within the patches, offering insight into the kinds of instructions provided.

### Insights:

Both word clouds reveal the core focus of the dataset on math, signal and audio manipulation within patches, emphasizing key operations like **create**, **generate**, **output**, and **control**. The visualizations offer a quick and intuitive way to grasp the recurring terms and themes in the dataset, assisting in understanding its overall structure and focus.
