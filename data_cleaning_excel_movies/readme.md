# Movie Data Cleaning Project

A data cleaning project for data scrapped from imdb and netflix and put on kaggle. 

📂 **Data Source:**

[From this Repo](unclean_movie.csv)

[From Kaggle](https://www.kaggle.com/datasets/bharatnatrayn/movies-dataset-for-feature-extracion-prediction)

---

### OPENING FILE 

1. Open a new excel file. Csv file cannot be opened directly as it will result in corrupted characters
2. Go to Data > From Text/CSV > (Select movies.csv) > Set File Origin = 65001 : Unicode (UTF-8) > Load 
3. Go to Data > Remove Duplicates . 431 duplicates values found and removed

---

### LINE BREAK IN "Genre","One-Line" and "Stars" 

1. Column 'Genre','One-Line',and 'Stars' have some awful line break. Browse the data, you find some text exist, but is not exist in formula bar, meaning it has line break.
2. We solve all of them by creating new column each to them and with `=TRIM(CLEAN(A2))`
3. Browse data again, i see some 'add plot' will be replace as blank in 'one-line' column

---

### YEAR COLUMN

1. Looking at year column, it is irregular , some have (2012-2018), (2017-) and (2017 TV special)
2. We want to split this year column into year_start and year_end.
3. Replace () with blank, with  Find and Replace 
4. Use Text to Column > Delimited > Other (the Em Dash) to the next 2 columns

---

### PARSING "STARS" COLUMN INTO "DIRECTORS" , "STARS" COLUMN

1. For Stars column , Use Data > Text to Columns. Choose Delimited > [/] Other: | > General to next 2 columns
2. Column 2 will have many empty column that is supposed to be filled by "Stars:.."
3. For Column 2 use Go To: , Press Control G > Special > Blank > OK. Blank cell will be highlighted.
4. For first empty cell, type = , and type in left to cell location. e.g "=H2"
5. Press Ctrl + Enter. Do not use Enter only.
6. Next, for Column 1, use Find and Replace. replace Stars:* with blank
7. Replace all "Directors:" with blank for column 1 and replace all "Stars:" with blank for column 2.

---

### "GROSS" COLUMN

1. Replace "$" and "M" with blank
2. Code this `=IFERROR(@[Gross]*1000000,"")` for data to be like 74700000 instead of $74.7M.

---

### FINISHED

[Finished product](data_cleaning_movies.xlsx)
