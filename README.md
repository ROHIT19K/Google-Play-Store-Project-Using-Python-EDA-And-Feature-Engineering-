# 📊 Google Play Store App Analytics 

> End-to-End Data Analytics Project using Python, Pandas, NumPy, Matplotlib, Seaborn, and Jupyter Notebook to analyze Google Play Store applications, user engagement, app popularity, and market trends.

---

# 📌 Project Overview


The Google Play Store App Analytics project focuses on analyzing application data from the Google Play Store to uncover insights related to app categories, ratings, reviews, installations, pricing, and market trends.

The project follows a complete Data Analytics workflow involving:

* Data Cleaning
* Data Transformation
* Feature Engineering
* Exploratory Data Analysis (EDA)
* Data Visualization
* Business Insights Generation

Using Python and Jupyter Notebook, raw Google Play Store data was transformed into a clean analytical dataset and used to identify the most popular app categories, installation trends, rating patterns, and user preferences.

---

## 🎯 Business Problem

With thousands of applications available on the Google Play Store, it becomes difficult for developers and businesses to understand:

* Which app categories are most popular
* Which categories receive the highest installations
* User rating patterns
* Market competition across categories
* App growth opportunities

---

# 🛠 Tools & Technologies

## 📌 Programming Language

* Python

## 📌 Development Environment

* Jupyter Notebook

## 📌 Libraries Used

* Pandas
* NumPy
* Matplotlib
* Seaborn

## 📌 Techniques Used

* Data Cleaning
* Feature Engineering
* Exploratory Data Analysis (EDA)
* Data Visualization
* Statistical Analysis

---

# 📂 Dataset Information

## 📌 Dataset Source

Google Play Store Dataset

---

## 📌 Dataset Size

* 10,000+ Applications
* Multiple Categories
* User Ratings
* Reviews
* Installation Data

---

## 📌 Important Features

* App Name
* Category
* Rating
* Reviews
* Size
* Installs
* Type (Free/Paid)
* Price
* Content Rating
* Genres
* Last Updated
* Android Version

---

# 🧹 Data Cleaning Performed

The raw dataset contained multiple data quality issues.

### Tasks Performed

### 1️⃣ Invalid Record Removal

* Identified non-numeric values in the Reviews column.
* Removed corrupted records causing datatype conversion issues.

### 2️⃣ Data Type Conversion

Converted:

* Reviews → Integer
* Installs → Integer
* Price → Float
* Last Updated → Datetime

### 3️⃣ Size Column Cleaning

Performed transformations such as:

* Converted MB values into numeric format.
* Removed special characters.
* Replaced "Varies with device" values with null values.

### 4️⃣ Install & Price Cleaning

Removed:

* "+"
* ","
* "$"

characters before conversion.

### 5️⃣ Duplicate Removal

Detected duplicate applications and retained only the first occurrence of each app.

### 6️⃣ Missing Value Handling

* Analyzed missing values.
* Calculated percentage of null records.
* Prepared clean dataset for analysis.

---

# ⚙️ Feature Engineering

Created additional features from the Last Updated column:

### Generated Columns

* Day
* Month
* Year

These features enabled time-based analysis and trend identification.

---

# 📈 Exploratory Data Analysis (EDA)

## 1️⃣ Dataset Exploration

Performed:

* Shape Analysis
* Data Type Analysis
* Missing Value Analysis
* Statistical Summary

---

## 2️⃣ Numerical Feature Analysis

Analyzed distributions of:

* Rating
* Reviews
* Size
* Installs
* Price

### Observations

* Rating and Year showed left-skewed distributions.
* Reviews, Installs, Price, and Size showed right-skewed distributions.

---

## 3️⃣ Categorical Feature Analysis

Analyzed:

* Category
* Type
* Content Rating
* Genres
* Android Version

Performed:

* Frequency Analysis
* Percentage Distribution Analysis

---

## 4️⃣ Univariate Analysis

Created visualizations to understand:

* App category distribution
* Rating distributions
* Install distributions
* Price distributions

---

# 📊 Business Questions Solved

## 📌 1. Which Category Has the Most Apps?

Analyzed app count by category.

    df_copy['Category'].value_counts().plot.pie(y=df['Category'], figsize=(20,16),autopct='%1.1f')

    cat = df_copy['Category'].value_counts().reset_index()
    cat.columns = ['Category', 'Count']

    cat1 = df_copy['Category'].value_counts().head(10).reset_index()
    cat1.columns = ['Category', 'Count']



![Image](https://github.com/ROHIT19K/Google-Play-Store-Project-Using-Python-EDA-And-Feature-Engineering-/blob/main/1.png)

### Result

* Family category contains the highest number of applications.
* Games and Tools categories also contain a large number of applications.
* Beauty category has the lowest number of applications.

---

## 📌 2. Which Category Has the Highest Installations?

Calculated total installs for each category.

        df_copy.groupby(['Category'])['Installs'].sum()

        dfa_cat_installs = df_copy.groupby(['Category'])['Installs'].sum().sort_values(ascending=False).reset_index()

        dfa_cat_installs.Installs = dfa_cat_installs.Installs/1000000000

        plt.figure(figsize=(15,10))
        sns.set_context("talk")
        sns.set_style("darkgrid")
        ax = sns.barplot(x='Installs', y='Category', data=df2, palette='hls')
        ax.set_xlabel('No of Installations in Billions')
        ax.set_ylabel('')
        ax.set_title("Most Popular Categories in Play Store", size=20)

![Image2](https://github.com/ROHIT19K/Google-Play-Store-Project-Using-Python-EDA-And-Feature-Engineering-/blob/main/2.png)

### Result

* GAME category recorded the highest number of installations.
* Total installations exceeded approximately 35 billion installs.
* Communication and Productivity categories also performed strongly.

---

## 📌 3. What Are the Most Installed Apps?

Identified the top installed applications across major categories.

        dfa = df_copy.groupby(['Category', 'App'])['Installs'].sum().reset_index()
        dfa = dfa.sort_values('Installs', ascending=False)
        apps = ['GAME', 'COMMUNICATION', 'PRODUCTIVITY', 'SOCIAL']
        sns.set_context('poster')
        sns.set_style('darkgrid')

        plt.figure(figsize=(40,30))

        for i, app in enumerate(apps):
            df2 = dfa[dfa.Category == app]
            df3 = df2.head(5)
            plt.subplot(4,2,i+1)
            sns.barplot(data = df3, x='Installs', y='App', palette='hls')
            plt.xlabel("Installation in Millions")
            plt.ylabel('')
            plt.title(app, size=20)

        plt.tight_layout()
        plt.subplots_adjust(hspace=.3)
        plt.show()

![Image3](https://github.com/ROHIT19K/Google-Play-Store-Project-Using-Python-EDA-And-Feature-Engineering-/blob/main/3.png)

### Results

Most popular apps identified include:

* Subway Surfers (Game Category)
* Hangouts (Communication Category)

These applications dominated their respective categories based on installation count.

---

## 📌 4. How Many Apps Have a Perfect Rating?

Analyzed applications with a rating of 5.0.

        rating = df_copy.groupby(['Category', 'Installs', 'App'])['Rating'].sum().sort_values(ascending=False).reset_index()

        toprating = rating[rating.Rating == 5.0]
        toprating.head()

![Image4](https://github.com/ROHIT19K/Google-Play-Store-Project-Using-Python-EDA-And-Feature-Engineering-/blob/main/4.png)

### Result

* 271 applications received a perfect 5-star rating.
* One of the highest-rated applications identified was:

  * CT Brain Interpretation

---

---

# 🚀 Future Enhancements

* Build interactive Power BI dashboard
* Create Tableau visualizations
* Perform sentiment analysis on app reviews
* Develop app success prediction models
* Implement machine learning classification models
* Create recommendation system for app categories

---

# ▶️ Project Workflow

1. Data Collection
2. Data Cleaning
3. Data Transformation
4. Feature Engineering
5. Exploratory Data Analysis
6. Data Visualization
7. Business Insights Generation
8. Reporting

---

# 🧠 Business Value

This project helps:

* App Developers understand market trends
* Businesses identify profitable categories
* Product Teams analyze user preferences
* Marketing Teams optimize app strategies
* Decision Makers understand competitive landscapes

---

# ✅ Results & Outcomes

* Cleaned and transformed Google Play Store dataset.
* Built reusable analytical dataset.
* Performed comprehensive EDA.
* Identified top-performing categories and applications.
* Generated actionable business insights.
* Demonstrated end-to-end Data Analytics workflow using Python.

---

# 📬 Contact

## 👤 Author

Your Name

* LinkedIn: Your LinkedIn 

* GitHub: Your GitHub Profile

* Email: [yourmail@gmail.com](mailto:yourmail@gmail.com)

