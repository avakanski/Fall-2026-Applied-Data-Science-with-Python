# CS 4622/5622 – Applied Data Science with Python

[University of Idaho](https://www.uidaho.edu) - [Department of Computer Science](https://www.uidaho.edu/engr/departments/cs)

Instructor: [Alex Vakanski](https://www.idahofallshighered.org/vakanski/) (vakanski@uidaho.edu)

Office Hours: Fridays, 10:00 AM – 11:00 AM Pacific (11:00 AM – 12:00 PM Mountain), held on Zoom, link available on Canvas.

Semester: Fall 2026 (August 24 – December 18)

<a href="Lectures/CS_4622_5622-Applied_Data_Science_with_Python-Syllabus.pdf">Course Syllabus</a>

*Course website*: <https://avakanski.github.io/Fall-2026-Applied-Data-Science-with-Python/>

*GitHub repository*: <https://github.com/avakanski/Fall-2026-Applied-Data-Science-with-Python>

## Lectures

* <a href="Lectures/Lecture_1-A_Short_History_of_AI/Lecture_1-A_Short_History_of_AI.pdf">Lecture 1 - A Short History and Current State of Artificial Intelligence</a>

### Theme 1: Python Programming

* <a href="Lectures/Theme_1-Python_Programming/Lecture_2-Python_Data_Types,_Statements/Lecture_2-Python_Data_Types,_Statements.ipynb">Lecture 2 - Python Data Types, Statements</a>
* <a href="Lectures/Theme_1-Python_Programming/Lecture_3-Files,_Functions/Lecture_3-Files,_Functions.ipynb">Lecture 3 - Files, Functions</a>
* <a href="Lectures/Theme_1-Python_Programming/Lecture_4-OOP,_Modules,_Packages/Lecture_4-OOP,_Modules,_Packages.ipynb">Lecture 4 - Object-Oriented Programming, Modules, Packages</a>

### Theme 2: Data Engineering Pipelines

* <a href="Lectures/Theme_2-Data_Engineering/Lecture_5-NumPy/Lecture_5-NumPy.ipynb">Lecture 5 - NumPy for Array Operations</a>
* <a href="Lectures/Theme_2-Data_Engineering/Lecture_6-Pandas/Lecture_6-Pandas.ipynb">Lecture 6 - Data Manipulation with Pandas</a>
* <a href="Lectures/Theme_2-Data_Engineering/Lecture_7-Matplotlib,_Seaborn/Lecture_7-Matplotlib,_Seaborn.ipynb">Lecture 7 - Data Visualization with Matplotlib and Seaborn</a>
* <a href="Lectures/Theme_2-Data_Engineering/Lecture_8-SQL/Lecture_8-SQL.ipynb">Lecture 8 - Databases and SQL</a>
* <a href="Lectures/Theme_2-Data_Engineering/Lecture_9-Data_Exploration/Lecture_9-Data_Exploration.ipynb">Lecture 9 - Data Exploration and Preprocessing</a>

*(Additional lectures will be added during the semester.)*

## Tutorials

* <a href="Lectures/Tutorials/Tutorial_1-Jupyter_Notebooks/Tutorial_1-Jupyter_Notebooks.ipynb">Tutorial 1 - Jupyter Notebooks</a>
* <a href="Lectures/Tutorials/Tutorial_2-VS_Code/Tutorial_2-VS_Code.ipynb">Tutorial 2 - Python IDEs, Visual Studio Code</a>
* <a href="Lectures/Tutorials/Tutorial_3-Terminal_and_Command_Line/Tutorial_3-Terminal_and_Command_Line.ipynb">Tutorial 3 - Terminal and Command Line</a>
* <a href="Lectures/Tutorials/Tutorial_4-Virtual_Environments/Tutorial_4-Virtual_Environments.ipynb">Tutorial 4 - Virtual Environments</a>
* <a href="Lectures/Tutorials/Tutorial_5-Google_Colab/Tutorial_5-Google_Colab.ipynb">Tutorial 5 - Google Colab</a>

## Course Description

The course introduces students to Python tools and libraries commonly used by organizations for managing the phases in the life cycle of Data Science projects. The content is divided into four main themes. The first theme reviews the fundamentals of Python programming. The second theme focuses on data engineering and explores Python tools for data collection, exploration, and visualization. The next theme covers model engineering and includes topics related to model design, selection, and evaluation for image processing and natural language processing. This theme also introduces recent advances in large language models, multi-modal models, and agentic AI systems. The last theme focuses on Data Operations (DataOps) and encompasses techniques for model serving, performance monitoring, diagnosis, and reproducibility of data science projects deployed in production. Throughout the course, students will gain hands-on experience with various Python libraries for Data Science workflow management. Additional work is required for graduate credit.

## Textbooks

There are no required textbooks for this course.

## Learning Outcomes

Upon the completion of the course, the students should demonstrate the ability to:

1. Attain proficiency with commonly used Python frameworks for managing the life cycle of Data Science projects.
2. Develop pipelines for integrating data from multiple sources, designing predictive models, and deploying the models.
3. Apply Python tools for data collection, analysis, and visualization of real-world datasets, such as NumPy, Pandas, Matplotlib, and Seaborn.
4. Implement machine learning algorithms for image processing, natural language processing, and tabular data analysis using Python-based frameworks, such as Scikit-Learn, Keras, TensorFlow, and PyTorch.
5. Understand the principles of model selection and evaluation, including hyperparameter tuning, cross-validation, and regularization.
6. Design and implement advanced AI systems using large language models, vision-language models, and agentic AI integration.
7. Understand the primary characteristics of current Python libraries for deployment, continuous integration, and monitoring of Data Science projects.
8. Deploy Data Science projects as web applications using Flask, FastAPI, and Django, and to cloud servers using Microsoft's Azure platform.

## Prerequisites

The course requires basic programming skills in Python. Prior knowledge of data science methods is beneficial but not required.

## Grading

Student assessment will be based on 6 homework assignments (worth 45 marks), 4 quizzes (worth 45 marks), and class participation and engagement (worth 10 marks).

| Assessment Component | Marks |
|----------------------|:-----:|
| Assignments (×6)     | 45    |
| Quizzes (×4)         | 45    |
| Class participation  | 10    |
| **Total**            | **100** |

## Course Schedule

The week-by-week schedule of topics is on the [course website](https://avakanski.github.io/Fall-2026-Applied-Data-Science-with-Python/#course-schedule).

## Building the Website

The website is built with [Quarto](https://quarto.org). To preview locally:

```bash
quarto preview
```

To render the full site into `_site/`:

```bash
quarto render
```

The site is published automatically to GitHub Pages by the GitHub Actions workflow in `.github/workflows/publish.yml` on every push to `main`.
