**ECE2112: ADVANCED COMPUTER PROGRAMMING AND ALGORITHMS**

**EXPERIMENT 4**

**DATA WRANLING AND DATA VISUALIZATION**

Pascual, Jasmine Nicole S.

2ECE-B
##
**I. Intended Learning Outcomes:**

1. To identify the codes and functions needed in cleaning and visualizing data
2. To be able to apply and use the different codes and functions in creating a Python program
   that will be used in data wrangling and data visualization
##
**II. Instructions:**

Download the ECE Board Exam 2 dataset found on this link: https://bit.ly/ECEBoardExamDataset and write a Python script/code
in the Jupyter Notebook to do the given problems. You may submit your Jupyter notebook in the dedicated submission bin.
##
**ECE BOARD EXAM PROBLEM:** 
Using data wrangling and data visualization technique with a storytelling, analyze the data and 
present different (i) data frames; and (ii) visuals using the dataset given.
##
1. Create the following data frames based on the format provided:

   Example: Vis=["Name", "Gender", "Track", "Math<70"]; hometown is constant as **Visayas**

   Ouput:
   
      **Name Gender    Track            Math**
   
      S4   Male      Instrumentation  65
   
      S11  Female    Communication    48
   
      S22  Female    Communication     6

**Code:**

    import pandas as pd #Access the Pandas library
    
    df = pd.read_excel('board2.xlsx') #Load the .xlsx file into a DataFrame
    
    Vis = df[(df['Math']<70)& 
          (df['Hometown']== 'Visayas' )].reset_index(drop=True) #Select the rows containing Math < 70 and Visayas under Hometown
          
    Vis = Vis[['Name', 'Gender', 'Track', 'Math']] #Select the columns to be displayed in the DataFrame
    
    Vis #Display the DataFrame

##
   a. Filename: Instru=["Name", "GEAS", "Electronics>70"]; were track is constant as Instrumentation
   and hometown Luzon
   **Code:**
   
       import pandas as pd #Access the Pandas library
    
       df = pd.read_excel('board2.xlsx') #Load the .xlsx file into a DataFrame
    
       Instru = df[(df['Track']== 'Instrumentation') & 
             (df['Hometown']== 'Luzon' ) &
             (df['Electronics'] >70)] #Select rows containing Instrumentation under Track, Luzon under Hometown, and Electronics > 70
             
       Instru = Instru[['Name', 'GEAS', 'Electronics']].reset_index(drop=True) #Select the columns to be displayed in the DataFrame
    
       Instru #Display the DataFrame
   ##
   b. Filename: Mindy=["Name", "Track", "Electronics", "Average >=55"]; where hometown is constant as
   Mindanao and gender Female.
   **Code:**
   
         import pandas as pd #Access the Pandas library
      
         f = pd.read_excel('board2.xlsx') #Load the .xlsx file into a DataFrame
      
         score = ['Math', 'Electronics', 'GEAS', 'Communication'] #Select the columns to calculate for the average
         
         df['Average']= df[score].mean(axis=1) #Calculate the average of the selected columns
      
         Mindy = df[(df['Hometown']=='Mindanao') & 
                 (df['Gender'] == 'Female')&
                 (df['Average']>=55)] #Select rows containing Mindanao under Hometown, Female under Gender, and Average >=55
        
        Mindy = Mindy[['Name', 'Track', 'Electronics', 'Average']].reset_index(drop=True) #Select the columns to be displayed in the DataFrame
        Mindy #Display the DataFrame

   ##
3. Create a visualization that shows how the different features contributes to average grade.
   Does chosen track in college, gender, or hometown contributes to a higher average score?
   **Code:**
   
        import seaborn as sns 
        import matplotlib.pyplot as plt #Access the library for plot
        
        df = pd.read_excel('board2.xlsx') #Load the .xlsx file into a DataFrame
        
        def plot_scores(df, x, y, hue=None, title=''):
            plt.figure(figsize=(10, 5))
            sns.barplot(x=x, y=y, hue=hue, data=df, palette=['pink','purple','gray'])
            plt.title(title)
            plt.xlabel(x)
            plt.ylabel(y)
            plt.xticks(rotation=45)
            plt.show()
        
        #Plot for the Math scores by Track and Gender
        plot_scores(df, 'Track', 'Math', hue='Gender', title='Math Scores by Track and Gender')
        
        #Plot for the Math scores by Hometown and Gender
        plot_scores(df, 'Hometown', 'Math', hue='Gender', title='Math Scores by Hometown and Gender')
        
        #Plot for the Electronics scores by Track and Gender
        plot_scores(df, 'Track', 'Electronics', hue='Gender', title='Electronics Scores by Track and Gender')
        
        #Plot for the Electronics scores by Hometown and Gender
        plot_scores(df, 'Hometown', 'Electronics', hue='Gender', title='Electronics Scores by Hometown and Gender')
        
        #Plot for the GEAS scores by Track and Gender
        plot_scores(df, 'Track', 'GEAS', hue='Gender', title='GEAS Scores by Track and Gender')
        
        #Plot for the GEAS scores by Hometown and Gender
        plot_scores(df, 'Hometown', 'GEAS', hue='Gender', title='GEAS Scores by Hometown and Gender')
        
        #Plot for the Communication scores by Track and Gender
        plot_scores(df, 'Track', 'Communication', hue='Gender', title='Communication Scores by Track and Gender')
        
        #Plot for the Communication scores by Hometown and Gender
        plot_scores(df, 'Hometown', 'Communication', hue='Gender', title='Communication Scores by Hometown and Gender')
