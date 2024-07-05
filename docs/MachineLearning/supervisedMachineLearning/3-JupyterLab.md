---
layout: default
title: Jupyter Notebook
parent: Supervised Machine Learning
grand_parent: Machine Learning
nav_order: 3
---
## Jupyter Notebook
A Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations, and narrative text. It's a popular tool among data scientists, researchers, and educators for conducting data analysis, running code interactively, and documenting their work.

Here are some key features and characteristics of Jupyter Notebooks:

* Interactive Computing: Jupyter Notebooks support various programming languages, with Python being the most commonly used. You can write and execute code in cells interactively, which means you can see the results of your code right in the notebook.
* Rich Text and Markdown Support: In addition to code cells, Jupyter Notebooks allow you to include explanatory text, equations, and formatted content using Markdown, LaTeX, and HTML. This makes it easy to create documentation, tutorials, or reports alongside your code.
* Data Visualization: Jupyter Notebooks can display a wide range of data visualizations, including plots, charts, and interactive widgets. Popular Python libraries like Matplotlib, Seaborn, and Plotly are often used for this purpose.
* Code Execution: You can run code cells in any order, which allows for an interactive and exploratory workflow. You can also rerun cells as needed and see the updated results.
* Kernel Support: Jupyter Notebooks work with different kernels, which are computational engines that execute code written in various programming languages. This flexibility allows you to use languages such as Python, R, Julia, and more within the same notebook.
* Sharing and Collaboration: Jupyter Notebooks can be easily shared with others, making it a valuable tool for collaborative work. You can export notebooks to various formats, including HTML, PDF, and Jupyter's own .ipynb format.
* Extensions: Jupyter Notebooks can be extended with various plugins and extensions to add functionality, such as code snippets, spell-checking, and improved visualizations.
* Notebook Environment: You can run Jupyter Notebooks locally on your computer or on cloud-based platforms like Google Colab, Azure Notebooks, or AWS SageMaker, which provide access to additional computing resources.

Jupyter Notebooks are widely used in fields like data science, machine learning, scientific research, and education due to their flexibility, interactivity, and ability to combine code, data, and explanatory text in a single document. They help make data analysis and experimentation more accessible and reproducible.

## Install JupyterLab
To install JupyterLab on a Mac and use it for Jupyter Notebook-style interactive computing, you can follow these steps:

Note: Before you proceed, make sure you have Python and pip (Python package manager) installed on your Mac. You can install Python from the official website (https://www.python.org/downloads/) or by using a package manager like Homebrew.
* Install JupyterLab:
Open a terminal on your Mac and use pip to install JupyterLab. You can do this by running the following command:
```markdown
pip install jupyterlab
```
* Launch JupyterLab:

After installation, you can start JupyterLab by running the following command in your terminal:
```markdown
jupyter lab
```

## Use JupyterLab:

JupyterLab provides a web-based interface where you can create and manage Jupyter notebooks and other interactive documents. Here's how you can use it:
* In the JupyterLab interface, you can create a new Jupyter notebook by clicking on the "File" menu and selecting "New" -> "Notebook."
* You can write and run code in code cells. To add a new cell, you can click the "+" button in the toolbar or use keyboard shortcuts (e.g., "A" for adding a cell above, "B" for adding a cell below).
* You can switch between code cells and Markdown cells for documentation and explanations.
* To run a code cell, select it and click the "Run" button in the toolbar, or use the keyboard shortcut (usually Shift+Enter).
* JupyterLab also supports various extensions and widgets for data visualization, interactive widgets, and more. You can explore and install these extensions as needed.
* To save your work, you can use the "File" menu or the save icon in the toolbar. Notebooks are saved with the ".ipynb" extension.

When you're finished, you can shut down JupyterLab by closing the browser tab or by stopping the JupyterLab server in the terminal (press Ctrl+C twice in the terminal).