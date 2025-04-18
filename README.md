[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/JyfpAES5)
# Final Exam: Coding 

Welcome to the coding portion of the Final Exam!  
This exam assesses your ability to use tools and skills covered throughout the course, including git/GitHub, data wrangling, data cleaning, basic web scraping, summary statistics, visualizations, and exploratory data analysis. Depending on your skill, preparation, and understanding of the class material, I expect that the exam should take between 3 and 5 hours but there is no formal time limit.

### Rules:
* This part of the exam is open LearningSuite and open internet
* You should not search for exact (or nearly exact) versions of the exam questions online.
* You may use AI tools (ChatGPT, CoPilot, etc.), but keep in mind that the goal is to assess **your** ability to work through real data problems using the tools you’ve practiced. It’s okay to use AI to help with debugging or syntax, *but not to bypass the thinking process.*
   - Refer to the [official class GenAI Policy](https://learningsuite.byu.edu/.wUmB/cid-BbcKkLhfX-d7/pages/id-476E) but the basics are: 
      - Help with snippets of code is ok
      - Having AI write large portions of code is **not ok**.
      - You should **not** copy and paste any portion of the exam into any AI tool

* You do NOT need to complete this portion of the exam in one sitting
* The exam should be finished by Wednesday April 23 at **12:00pm** *(Noon)*
* You should not discuss the exam with other students, even after you have completed it

  
### Set up a local version of the repository: 
* When you accept the assignment in GitHub Classroom, a repository named `final` will be automatically generated for you under the "stat386-winter2025" organization.
* Your personal repository for this homework can be found at `https://github.com/stat386-winter2025/final-your_user_name`.
* *Clone the Repository*: 
    - Open your terminal and navigate to the directory where you want to download the repository.
    - Run `git clone your_repository_URL` to clone the repository onto your local machine.
* The cloning process will create a new directory. Ensure that you perform all your work inside this directory.  Push your work from your local repo to the remote GitHub repo in order to submit your work. 

---
## Git Requirements (Task 0)
1. You need to create a gitignore file
   * The following files and folders should not be in any commit of your repository:  
      * `.DS_Store`
      * `.ipynb_checkpoints/`
      * `__pycache__/`
      * any file with the extension `.pyo`, `.pyc`, or `.pyd`
      * any other file not requested in the "Submission" section below.
   * To clarify, the ONLY files that I should find in your repo are:
      * A file called `code.py` OR `code.ipynb` 
      * A `.gitignore` file
      * The `final-answers.txt` file
      * The file `earthquakes.csv`
      * The file `fatalities-by-magnitude.png`
      * The file `earthquake-map.html`
2. As you are working, you should make **at least** 5 commits.  The commits should be made *locally* (not directly through GitHub) and should have **sensible and informative** commit messages.
3. When you are finished with the exam, make sure that your work gets pushed to GitHub.


## Python Requirements 
* You should complete the final in Python
* I should be able to run your code without errors
* Your code should not take longer than 1 minute to run and should be shorter than ~150 lines
* Your code should be neat, organized, and well-commented 

## Submission
* Be sure to put the answers to the questions in "Task 4" in the `final-answers.txt` file.  
* At the time of submission, your repository should include the following files:
   * A file called `code.ipynb` or `code.py` that contains the code used the answer the questions.  This code should be neat, organized, and well commented
   * A `.gitignore` file
   * The `final-answers.txt` file
   * The file `earthquakes.csv`
   * The file `fatalities-by-magnitude.png`
   * The file `earthquake-map.html`
* You do **NOT** need to submit to Gradescope.  Having the files in the GitHub repository is sufficient. 
* Be sure that all files are finished and in the repo before the deadline (Wednesday, April 23 at 12:00pm) 


## Python Version
Tell me what version of pandas that you are using.  You can find this out by running:
```
import pandas as pd
pd.__version__
```
*(There are two underscores before and after the word "`version`")*

---
### Task 1:  Data Collection

1. Create a pandas DataFrame of significant earthquakes occurring from 2001 through the present by using the `pandas.read_html` function to scrape data from the following three Wikipedia pages. 
* [List of Earthquakes 2001-2010](https://en.wikipedia.org/wiki/List_of_earthquakes_2001%E2%80%932010)
* [List of Earthquakes 2011-2020](https://en.wikipedia.org/wiki/List_of_earthquakes_2011%E2%80%932020)
* [List of Earthquakes 2021-2030](https://en.wikipedia.org/wiki/List_of_earthquakes_2021%E2%80%932030)
   * *Hint: All relevant data on the Wikipedia pages will be in tables with at least 8 columns*
---

### Task 2: Data Cleaning
After getting the data, clean the dataset as follows:

1. Combine the `Date` and `Time` columns into a single `datetime` column named `date_time` 
   * Convert the dtype to `datetime`
2. Clean the "Fatalities" column 
   * Your goal is to convert the values to clean, numeric integers, following these guidelines: 
      * Ignore "missing" people unless they are the only value listed (e.g., "100 dead 5 missing -> 100; "3 missing" -> 3).
      * If a range is provided, use the **lower bound** (e.g. "50~100" -> 50)
      * Remove commas in numbers (e.g. "1,000" -> 1000)
      * Convert to integer values
   * *Note: These cleaning guidelines are not meant to be tricky; they are actually meant to make things easier for you.*
   * *Note: Use common sense when deciding the order in which to apply these steps. For example, removing commas should happen before converting to integers*
3. Clean the "Magnitude" column
   * Your goal is to convert the values to clean, numeric floats, following these guidelines: 
      * If the magnitude is a range, use the **upper bound** (e.g., "7.0~7.5" -> 7.5)
      * Remove any formatting issues (e.g., stray symbols or whitespace)
      * Convert to numeric (float) values
   * 	*Note: As with the Fatalities column, use common sense when deciding the order in which to apply these steps. For example, you should resolve ranges and remove any non-numeric characters before converting to floats.*
4. Create a new column called `magnitude_cat` that categorizes earthquakes into the following bins based on Magnitude:
      * Low: Magnitude < 5
      * Moderate: Magnitude 5-6.99
      * High: Magnitude >= 7
5. To ensure consistency across students, **remove any earthquakes that occur *after* April 17, 2025.** 
6. Retain only the following columns: `date_time`, `latitude`, `longitude`, `fatalities`, `magnitude` and `magnitude_cat`
   * *Note: Ensure your column names match those listed above exactly. If your dataset uses different names, rename the columns to align with this requirement.*
7. **Print** the first 5 rows of the dataset
8. **Print** the results from the `.info()` method

---
### Task 3: Save the Cleaned Data

1. Save your cleaned dataset as a CSV file named `earthquakes.csv` in your repository.

   * The final dataset should have the columns:  `date_time`, `latitude`, `longitude`, `fatalities`, `magnitude` and `magnitude_cat`. All the variables should be numeric except `date_time` (which should be a datetime) and `magnitude_cat` (which should be of dtype object or category)

   * **Important:** Ensure the index is not saved as a column in your CSV. 

---
### Task 4: Questions
Using your cleaned dataset, answer the following questions.  Provide **short numeric answer** unless otherwise specified.     
   * Make sure your code for each question is included in your `code.ipynb` (or `code.py`) file
   * Round numeric non-integer answers to **three decimal places**
   * All dates should be reported as YYYY-MM-DD
   * Make sure the answers to the questions are added to the "final-answers.txt" file

1. How many rows are in your cleaned dataset?
2. What is the mean and median of the earthquake magnitudes?
3. 
   * (a) What date has the highest total number of fatalities  
   * (b) How many fatalities occurred on that date 
   * (c) The number of fatalities on that date is what percent of the total fatalities in the data?
   * (d) In your code, make a copy of the dataset **with this row removed**.  Use this copy for all subsequent calculations, but do not overwrite or resave your original `earthquakes.csv` file. 
4. What is the date, latitude, and longitude of the earthquake with the **lowest magnitude**?
5. What is the date, latitude and longitude of the earthquake with **highest number of fatalities**?
6. What is the **average latitude and longitude** for earthquakes with a magnitude of 8 or higher?
7. What is the **average time between earthquakes** in the dataset.  Report the result in the format "XX days HH:MM:S.sss" (for example "2 days 13:24:30.235" which would represent 2 days, 13 hours, 24 minutes and 30.235 seconds).
   * *Hint: Sort by DateTime and use the `.diff()` method*
8. Compute the **average number of fatalities**  for Low, Moderate, and High magnitude earthquakes.
9. Using Seaborn or Matplotlib, make a scatter plot that shows `magnitude` on the x-axis, `fatalities` on the y-axis, and each marker colored by `magnitude_cat`.  **Briefly describe what the figure helps you understand about the data.** 
Save this figure as a .png file called *fatalities-by-magnitude.png*. Include the file in your repo.  You can save a figure from seaborn or matplotlib using the `savefig` method:
   ```
   plt.savefig('my_figure.png')
   ```
10. Using Plotly express, make a plot of all the latitudes and longitudes on a world map.  Color the marker by magnitude_cat.  When you hover over a marker on the graph, the following details should be displayed: `latitude`, `longitude`, `magnitude`, `fatalities`, and `date_time`.  **Briefly describe what the figure helps you understand about the data.** 
Save this file as a .html file called *earthquake-map.html*.  Include the file in your repo.  You can save a figure from plotly using the `write_html` method:
      ```
      fig = # code to create plotly figure
      fig.write_html('my_figure.html')
      ```

### Task 5: You're Own EDA
Explore your cleaned earthquake dataset and identify one notable or unusual pattern that was *not directly asked* about in earlier tasks. This could be:
* A data point that stands out as extreme 
* A time period with an unusual number of events
* A pattern over time 
* A surprising relationship between two variables
* Anything else that seems noteworthy

**In your code.ipynb** (or code.py) file, include the code you used to explore or visualize this pattern.

**In your final-answers.txt file, write 1–2 sentences summarizing the pattern and why you found it interesting.**

*You will be graded on clarity and effort—not on whether the pattern is “correct” or especially complex.*

### Task 6: Reflection

In the **final-answers.txt** file, answer the following questions with 1-2 sentences each:

1. What part of the exam was most challenging for you and why?
2.	Did you use an AI tool (such as ChatGPT, CoPilot, etc.) during the exam?
- IF YES:
   * (a) What kinds of tasks did you use it for? (e.g., debugging, checking syntax, brainstorming)
   * (b) Briefly describe one specific way you used it—what you asked and how you used the response.
   * (c) What was helpful or unhelpful about it?
- IF NO:
   * (a) Why did you decide not to use GenAI this time? 
   * (b) *(leave blank)*
   * (c) *(leave blank)*
3. Approximately how much time did it take you to complete this portion of the final exam? 
