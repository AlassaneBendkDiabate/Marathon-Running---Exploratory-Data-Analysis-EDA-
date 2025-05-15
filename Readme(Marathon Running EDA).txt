Marathon Running - Exploratory Data Analysis (EDA)
________________


Overview
This project performs an exploratory data analysis (EDA) on marathon running data, focusing specifically on events that took place in the USA in 2018 and over a distance of 50km. The analysis aims to uncover trends and insights related to athlete performance, demographics, and club participation.


________________


Dataset
The dataset includes the following fields:
* Year of event

* Event dates

* Event name

* Event distance/length

* Event number of finishers

* Athlete performance

* Athlete club

* Athlete country

* Athlete year of birth

* Athlete gender

* Athlete age category

* Athlete average speed

* Athlete ID

We focused our study  on only events that occurred in 2018 in the USA and that are 50 km long.
Code : df_USA = df[(df['Event distance/length'] == '50km') & (df['Event country'] == 'USA') & (df['Year of event'] == 2018)]


________________


Technologies Used
   * Python (Pandas, NumPy, Matplotlib, Seaborn)

________________


Data Preprocessing
      * Converted Athlete performance from string to timedelta.

      * Removed outliers (e.g., athletes aged <10 or >80).

      * Parsed Event country from Event name when necessary.

      * Converted numeric columns to appropriate types.

________________


Questions & Visualizations
1. Gender Distribution of Athletes
Code/Graph: 
gender_counts = df_USA.groupby('Athlete gender').size()  
gender_counts.plot(kind='pie', y='Athlete gender', autopct='%1.0f%%', figsize=(6, 6))
Insight: Males are significantly more represented than females.


2. Are There Clubs with Only Male or Female Athletes?
Code:  df_USA.groupby('Athlete club')['Athlete gender'].unique()
Insight: Yes, some clubs have only one gender represented while some have ⅔ genders.


3. Distribution of Speeds
Code/Graph:
sns.displot(data=df_USA,x='Athlete average speed',hue='Athlete gender', kind='kde',
fill=True, palette='Set1', height=5,aspect=1.2)
Insight: Distribution is right-skewed, showing most athletes cluster below the top speed.


4. Top Performing Clubs
Code:  
df_USA.groupby('Athlete club')[('Athlete performance')].mean().sort_values(ascending=True) 
Insight: Smaller clubs like Nairobi or Chappaqua occasionally rank higher in performance 


5. Relationship Between Club Size and Athlete Performance
Code:  club_stats = df_USA.groupby('Athlete club')['Athlete performance'].agg(['mean','count']).sort_index(ascending=False).sort_values(by='mean',ascending=True)
Scatter plot with regression line
Graph: sns.regplot(x='count', y='mean', data=club_stats, scatter_kws={"color":"red"}, line_kws={"color":"blue"})
Insight: Weak negative correlation. We can’t say much . Larger clubs don't necessarily perform better.






6. Best performing group Age 
Code:  
df_USA.groupby('Athlete age')['Athlete performance'].agg(['mean']).sort_values(by='mean', ascending=True)
Insight: We can see the Best performing athletes are between 20-25 years old.


7. Relationship Between Athletes Age and their Average Speed
Code:
df_USA_cleaned = df_USA[(df_USA['Athlete age'] >= 10) & (df_USA['Athlete age'] <= 80)]
Graph : sns.regplot(x='Athlete age', y='Athlete average speed', data=df_USA_cleaned, scatter_kws={"color":"red"}, line_kws={"color":"blue"})
Insight: We can Clearly see Performance tends to decrease with age.
________________


Key Insights
         * Athlete performance slightly decreases with age.

         * Gender distribution is male-dominated.

         * Larger clubs do not necessarily perform better.

         * Outliers can strongly affect mean performance metrics.

________________


Future Work
            * Expand analysis to other distances (e.g., 100km).

            * Analyze athlete performance over multiple years.

            * Explore regional comparisons (e.g., USA vs Europe).

            * Build predictive models for athlete performance.
________________


Author
Alassane Ben Deka Diabate
Feel free to reach out for collaboration or feedback!