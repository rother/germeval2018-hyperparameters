# Collection of hyperparameters for the models from the GermEval-2018 paper
## Link to the proceedings: [GermEval-2018 Proceedings](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=2ahUKEwj1j7OpxbHhAhUi2aYKHfSDBfEQFjAAegQIAhAC&url=https%3A%2F%2Fwww.oeaw.ac.at%2Ffileadmin%2Fsubsites%2Facademiaecorpora%2FPDF%2FGermEval2018_Proceedings.pdf&usg=AOvVaw121MWJiBhUX37Guho0moxm "GermEval-2018 Proceedings")

Due to the big changes of the fast.ai library from version 0.7.x (when the paper was submitted) to 1.0.x I'm currently rewriting the previously messy code for the new library. In the meantime this repo collects the hyperparameters of the best models from the paper for reference/implementation purposes. The other parameters can be found in the paper. 

## Language Model (LM)

These are the hyperparameters for LM-E. While LM-A achieved a slightly lower/better perplexity, model E seems more promising in post-conference experiments. The lowest perplexity (50k tokens) was 27.39 for LM-A and 29.37 for LM-E.

The language model was trained on 100k articles from the German Wikipedia. This is a reduced dataset, the entire Wikipedia contains more that 700k articles. The vocabulary was limited to 50k tokens.

Note: One epoch trains in roughly 2 hours 50 minutes on a GTX 1080.

### Hyperparameters LM-E
| Name        | Value           | 
| ------------- |:-------------:| 
| Optimizer      | SGD |
| Epochs      | 25 |
| BS      | 32 |
| BPTT      | 70      | 
| LR | 5.12 (fixed)   |
| WD | 1e-7      |
| CLR | [10, 10, 0.95, 0.85]  |
| Dropout | [0.6, 0.4, 0.5, 0.1, 0.2] * 0.5  |
| Gradient Clipping | not used  |


## Language-Medium Model (LMM)

The model was trained on 303.256 unlabeled tweets that were collected from the streaming API with a custom script.

The model was gradually unfrozen by unfreezing the last layer and then unfreezing all layers.

### Hyperparameters LMM-1
| Name        | Value           | 
| ------------- |:-------------:| 
| Optimizer      | SGD |
| Epochs      | 30 |
| BS      | 32 |
| BPTT      | 70      | 
| LR (last unfrozen) | 3e-3 (fixed)   |
| LR (all unfrozen) | 3e-3 (fixed)   |
| WD | 1e-7      |
| STL-Ratio (last unfrozen) | 32  |
| STL-Cut_Fract (last unfrozen) | 0.5  |
| STL-Ratio (all unfrozen) | 20  |
| STL-Cut_Fract (all unfrozen) | 0.1  |
| Dropout | [0.25, 0.1, 0.2, 0.02, 0.15] * 1.8  |
| Gradient Clipping | not used  |

## Task-Specific Head (TSH)

The TSH was trained on the provided data from the organizers of GermEval-2018.

The model was gradually unfrozen layer by layer with the same hyperparameters.

### Hyperparameters TSH
| Name        | Value           | 
| ------------- |:-------------:| 
| Optimizer      | SGD |
| BS      | 52 |
| BPTT      | 70      | 
| LR | 3e-1 (fixed)   |
| WD | 1e-7      |
| CLR | [10, 10, 0.98, 0.85]  |
| Dropout | [0.25, 0.1, 0.2, 0.02, 0.15] * 1.8  |
| Gradient Clipping | not used  |
