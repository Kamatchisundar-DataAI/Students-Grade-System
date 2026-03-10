# Students-Grade-System
A simple level Student Marks Management System using Pandas
import pandas as pd
import os

filename = "Stud_data.csv"

# 1. LOAD DATA: Check if file exists, otherwise create the starting data
if os.path.exists(filename):
    df1 = pd.read_csv(filename)
    df1 = df1.loc[:, ~df1.columns.str.contains('^Unnamed')]
    print("--- Existing Data Loaded ---")
else:

    print("file Not found")
       '''
    a = {
        'Student':['David', 'Samuel', 'Terry', 'Evan'],
        'Age':[27, 24, 22, 32],
        'Country':['UK', 'Canada', 'China', 'USA'],
        'Course':['Python','Data Structures','Machine Learning','Web Development'],
        'Marks':[85,72,89,76]
    }
    df1 = pd.DataFrame(a)
    print("--- Creating New Database ---")
    '''

def Hi_marks(grade):
    if grade >= 80: return 'A+'
    elif 80 > grade >= 68: return 'A'
    else: return 'B'

# Ensure 'Grade' column exists even for newly loaded files
if 'Grade' not in df1.columns:
    df1['Grade'] = df1['Marks'].apply(Hi_marks)

print(df1)

# 2. ADD DATA
user_choice = input("\nDo you want to add new data (yes/no): ").lower()

if user_choice == 'yes':
    new_name = input("Enter Student Name: ").strip()
    new_age = int(input("Enter Age: "))
    new_country = input("Enter Country: ")
    new_course = input("Enter Course: ")
    new_marks = int(input("Enter Marks: "))
    new_row = pd.DataFrame([{
  'Student': new_name, 
'Age': new_age, 
'Country': new_country, 
'Course': new_course, 
'Marks': new_marks,
'Grade': Hi_marks(new_marks)
}])

# 3. Save Data
    df1 = pd.concat([df1, new_row], ignore_index=True)
    
  
    df1.to_csv(filename, index=False)
    print("\n Saved to file successfully!")
    print(df1)

# 4. SEARCH SECTION
Search_name = input("\nEnter name to search: ").strip()
result = df1[df1['Student'].str.lower() == Search_name.lower()]

if not result.empty:
    row = result.iloc[0]
    print(f"Result: {row['Student']} | {row['Grade']} in {row['Course']}")
else:
    print("Data not found.")

Outputs:
<img width="320" height="238" alt="image" src="https://github.com/user-attachments/assets/7398617b-038a-44c1-80d9-482ca16a4ed3" />
<img width="315" height="279" alt="image" src="https://github.com/user-attachments/assets/ecad4d73-746e-44e0-8994-e17c28e2f05e" />



