# LINGO Copilot

LINGO Copilot is an extension of GitHub Copilot that can assist you with developing LINGO models from free form text descriptions of what you would like to do. This documentation describes how to get started, and gives examples. Use cases include generating a model from a detailed description in LaTeX, generating new model data, building on an existing model, asking about functions in LINGO, and changing the data source of a model.

LINGO Copilot requires three software: LINGO, GitHub Copilot, and Microsoft Visual Studio.

## Getting LINGO 
The Copilot extension does not require that LINGO is installed. However, having the [latest version of LINGO 21](https://lindo.com/index.php/ls-downloads/try-lingo) installed on your computer is highly recommended. 

## Getting access to GitHub Copilot

Sign up for  [GitHub Copilot Free](https://github.com/settings/copilot?utm_source=vscode-completions-readme&utm_medium=second&utm_campaign=2024dec-em-MSFT-signup "https://github.com/settings/copilot?utm_source=vscode-completions-readme&utm_medium=second&utm_campaign=2024dec-em-MSFT-signup"), or request access from your enterprise admin.

To access GitHub Copilot, an active GitHub Copilot subscription is required. See: [github.com/features/copilot](https://github.com/features/copilot?utm_source=vscode-completions-readme&utm_medium=readme&utm_campaign=2024q3-em-MSFT-signup "https://github.com/features/copilot?utm_source=vscode-completions-readme&utm_medium=readme&utm_campaign=2024q3-em-MSFT-signup").

## Getting LINGO Copilot 

LINGO Copilot is available on the VS Code marketplace for download. To install open VS Code and bring up the Extensions view by clicking on the Extensions icon, which is located on the Activity Bar on the left-hand side of the VS Code editor. Search the marketplace for LINGO Copilot and click Install. Next it is recommended that you also download the LINGO-lsp for syntax highlighting, auto complete and the ability to run LINGO scripts from VS Code.
![Extensions icon](https://github.com/lindosystems/LINGO-Copilot/blob/main/res/Extensions_btn.png?raw=true#gh-light-mode-only)
![](https://github.com/lindosystems/LINGO-Copilot/blob/main/res/lingo_copilot_market.png?raw=true#gh-light-mode-only)

## Using LINGO Copilot

Start Visual Studio, and then in Copilot [chat view](https://code.visualstudio.com/docs/copilot/overview#_chat-view), open a LINGO .LNG file.  
Having the .LNG file open in Visual Studio Code will give Copilot context to your questions.  

![](res/LINGO_Copilot_1_DARK.png#gh-dark-mode-only)
![](res/LINGO_Copilot_1_LIGHT.png#gh-light-mode-only)

To interact with LINGO Copilot in the chat view enter  `@LINGO` followed by your request. 

![](res/blank_prompt_DARK.png#gh-dark-mode-only)
![](res/blank_prompt_LIGHT.png#gh-light-mode-only)

### Generating Models
If you do not yet have a LINGO model to work on, LINGO Copilot can assist you with generating one. For the best quality model generation, have a detailed model statement, sets, attributes, objective, and constraints included in the initial prompt.
#### Example

Statement: 
The objective of this model is to minimize the production cost, such that the amount of each product produced is within the upper and lower limits of the factory producing it. Also, the demand for each product is met each month.

Sets:

* Month: January through December. 
	* Each month has a demand.
* Factory: 
	* Each factory has an upper $u_f$ and lower $l_f$ limit on production levels.
	* Each factory has a fixed cost $a_f$ if it produces anything. 
	* Each factory has a cost $c_f$, per unit of produced.
* MxF: Cartesian product of Month and Factory.  
	* Each MxF has decision variable $x_{m,f}$ for the number of items produced in month $m$ at factory $f$.
	* Each MxF has a binary decision variable $z_{m,f} = 1$ if the factory runs in month m $0$ otherwise.


Model:

$$
\min  \sum\limits_{f \in F, m \in M} a_f z_{m,f} + c_f x_{m,f}
$$

$$
x_{m,f} \le u_f z_{m,f}  \quad  \forall f \in F, m \in M 
$$

$$
x_{m,f} \ge l_f z_{m,f}  \quad  \forall  f \in F, m \in M 
$$

$$
\sum\limits_{f\in F} x_{m,f} = d_m  \quad  \forall f \in F, m \in M 
$$

$$
z_{m,f} \in \{0, 1\}  \quad  \forall f \in F, m \in M.
$$

![](res/factory_ex_gen_DARK.png#gh-dark-mode-only)
![](res/factory_ex_gen_LIGHT.png#gh-light-mode-only)

Copy the generated model over to the blank .LNG file opened in Visual Studio code. Use the Run LINGO button to test your generated LINGO model.

![](res/runLINGO_DARK.png#gh-dark-mode-only)
![](res/runLINGO_LIGHT.png#gh-light-mode-only)
### Generating Model data

LINGO Copilot can assist you with generating data to help test your models. In the generated factory model, we may want to add more factories which requires new upper and lower limits, unit costs, and fixed costs.


![](res/new_data_prompt_DARK.png#gh-dark-mode-only)
![](res/new_data_prompt_LIGHT.png#gh-light-mode-only)

![](res/new_data_gen_DARK.png#gh-dark-mode-only)
![](res/new_data_gen_LIGHT.png#gh-light-mode-only)
 
### Adding Constraints 
LINGO Copilot can assist you with adding constraints to an existing model. In the example factory model, we may want to make the variable $x_{m,f}$  an integer.

![](res/con_prompt_DARK.png#gh-dark-mode-only)
![](res/con_prompt_LIGHT.png#gh-light-mode-only)

![](res/con_gen_DARK.png#gh-dark-mode-only)
![](res/con_gen_LIGHT.png#gh-light-mode-only)

### Displaying Solution Data
Ask LINGO copilot to assist with building a solution report. After solving the factory model, we may want a breakdown of production for each month at each factory. 

![](res/display_prompt_DARK.png#gh-dark-mode-only)
![](res/display_prompt_LIGHT.png#gh-light-mode-only)

![](res/display_gen_DARK.png#gh-dark-mode-only)
![](res/display_gen_LIGHT.png#gh-light-mode-only)

### Documentation Questions
LINGO Copilot can assist with learning about developing LINGO models. For example, you may not be sure what `@BIN(M, F)` is doing in the factory model.

![](res/bin_prompt_DARK.png#gh-dark-mode-only)
![](res/bin_prompt_LIGHT.png#gh-light-mode-only)

![](res/bin_gen_DARK.png#gh-dark-mode-only)
![](res/bin_gen_LIGHT.png#gh-light-mode-only)

### Documenting Models
Ask LINGO copilot to add comments to your model. This may help you understand the LINGO modeling language better, and help others understand your model. 

![](res/comment_prompt_DARK.png#gh-dark-mode-only)
![](res/comment_prompt_LIGHT.png#gh-light-mode-only)

![](res/comment_gen_DARK.png#gh-dark-mode-only)
![](res/comment_gen_LIGHT.png#gh-light-mode-only)

### Importing data
Data for your LINGO model may come from external sources such as Excel, a text file, or a different programming language. You can ask copilot to assist you with converting your model to read and write data to these external sources.

LINGO uses `@OLE` to read and write data with Excel. LINGO Copilot can edit your model to use `@OLE`:

![](res/excel_prompt_DARK.png#gh-dark-mode-only)
![](res/excel_prompt_LIGHT.png#gh-light-mode-only)

![](res/excel_gen_DARK.png#gh-dark-mode-only)
![](res/excel_gen_LIGHT.png#gh-light-mode-only)


LINGO uses `@FILE` to read from an external file. LINGO Copilot can edit your data to be read from an external file:

![](res/file_prompt_DARK.png#gh-dark-mode-only)
![](res/file_prompt_LIGHT.png#gh-light-mode-only)

LINGO Copilot can even generate a file for you to test out:

![](res/data_file_prompt_gen_DARK.png#gh-dark-mode-only)
![](res/data_file_prompt_gen_LIGHT.png#gh-light-mode-only)


LINGO uses `@POINTER( N)` to read and write data from a different programing language. LINGO Copilot can edit your data to be read in with `@POINTER`:

![](res/API_prompt_gen_DARK.png#gh-dark-mode-only)
![](res/API_prompt_gen_LIGHT.png#gh-light-mode-only)
