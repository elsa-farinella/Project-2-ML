\[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/fEFF99tU)
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12899338&assignment_repo_type=AssignmentRepo)

# ML PROJECT 2

# Team
- **Team name**: BetterThanPoli
- **Team member**:
    - Elsa Farinella, SCIPER: 377583
    - Robin Faro, SCIPER: 370950
    - Marco Scialanga, SCIPER: 369469

# Codebase
The project's codebase is structured across the following files and folder:

**web_scraping.py**: This file contains the code to scrape all the comments from the Washington Post's article. 

**topic_extraction.py**: This script performs topic modeling on text data related to heat pumps using the BERTopic library. The code is organized in the following way: 

  - *Data Preprocessing*: The code begins by loading and preprocessing data from a CSV file ("comments_long.csv"). It employs spaCy for lemmatization and stopwords removal to prepare the text data for analysis.
  
  - *Topic Modeling*: An instance of the BERTopic model is created and fitted to the preprocessed text data. The "all-MiniLM-L6-v2" embedding model is utilized to extract topics from the data.


**DatasetChatbot.py**: This file defines a custom dataset class to be used for the training of the chatbot model. It reads data from a CSV file with question and answer columns, tokenizes the text using the specified tokenizer (that will be specified in the "train.py" file), and prepares the data for model input. It also ensures that the input sequences are appropriately formatted for the chatbot model.

**train.py**: The train.py script contains the code for training the GPT-2 model for chatbot purposes. Here's an explanation of the key components:

  - *Data Preparation*: The script loads and preprocesses the chatbot dataset, splitting it into training, validation, and test sets.
  
  - *Model Configuration*: It loads the GPT-2 Large model and tokenizer, adding special tokens as needed.

  - *Training Loop*: The code includes a training loop that fine-tunes the model. It tracks training and validation losses over epochs.
  
  - *Model Saving*: The trained model is saved to the specified path if it produces the lowest validation loss.

**test.py**: This file performs a comparison between the performances of the non fine-tuned model and the fine-tuned version. It just prints the average loss on the test set in both cases. Before executing, please ensure that the weights are correctly loaded and stored, as we will explain in the "Model State Download" section.

**data**: The data folder contains the two dataset we used for our exmperiments. Specifically it contains the following files:
  - *comments_long.csv*: This .csv file contains all the comments longer than 20 characters extracted from the Washington Post's article regarding heat pumps. 

  - *qa_heatpumps_2.csv*: This .csv file contains the synthetic dataset we use for fine-tuning our model. Each row represents a pair of question and answer, following the format: "questions" ; "answer". 

**flask_chatbot**: The flask_chatbot folder contains all the necessary code to launch a local instance of the chatbot. The internal folders are organized according to Flask rules.  This structure includes key internal folders:

 - *Statistic Folder*: this is where all the .js and .css files are stored. These files are essential for the aesthetic and functional aspects of the website's user interface.

 - *Templates Folder*: this folder contains the HTML files. These files define the layout and elements of the web pages.
 - *App.py*: this script has a dual function. Firstly, its defines the routes for the front-end version of the bot. Secondly, it handles the internal computation of the chatbot. These computations are based on the 'infer' function.


# How to reproduce our experiments
In order to reproduce our experiments it is necessary to excute the python script we provided in the following way:
- **web_scraping.py**: This program does not require any parameter. It will produce a 'comments_long.csv' file containing the preprocessed comments.
- **topic_extraction.py**: Similar to the previous program, this one does not require the user to input any parameters. However, it depends on the 'comments_long.csv' file we created earlier, so it is crucial to ensure that this file is located in the 'data' folder, as in the repository.
- **train.py**: This script will reproduce the fine-tuning of our model. Since it generates the model's weights, users are required to run it by specifying the path to the folder where they wish to save these weights. Please be aware that the size of the '.pt' file will be approximately 2.88GB; ensure you have sufficient available space. Here is an usage example, given that you are in the command line, having already accessed the main folder:
" python train.py 'path/to/save/weights' "

# How to start an interactive session with the bot

To successfully use this GPT-2 Chatbot Web Application, please follow these steps:

- **Model State Download**:

  To obtain the required fine-tuned GPT-2 model state you can download the weights from the following link:
  https://drive.google.com/file/d/1RiazXe8BqMCSaNywLvyHIcvybAk315Sk/view?usp=share_link. Alternatively, it is possible to reproduce them by executing the 'train.py' script previously discussed. Once you have the 'model_state_2_large_v2.pt' file, please ensure it is placed inside the main folder. 
  

- **Application Execution**:

  Launch the Flask application by running the file *app.py* in your terminal or command prompt inside the main folder. Since, as we said, you have to be in main folder when executing the command, the usage example is the following:
  " python flask_chatbot/app.py "

- **Chatbot Interaction**:

  The application will execute on localhost on the port 5002, hence you can access it just browsing the '127.0.0.1:5002' in your web browser. Enter your question, and the chatbot will respond with generated answer based on your input.
  
  
## Requirements
- torch = 2.0.1
- transformers = 4.35.2
- flask = 2.2.2
- bertopic = 0.15.0
- pandas = 1.5.3
- spacy = 3.7.2
- selenium = 4.16.0
