# Students-Grade-System
A simple level Student Marks Management System using Pandas

#  Students Grade System
A Python-based data management tool that automates student grading, data persistence, and searching using Pandas.

### Features
-  Data Persistence : Uses os.path to load existing data from CSV or create a new database.
-  Automated Grading: Custom function to assign 'A+', 'A', or 'B' based on marks.
-  Dynamic Entry: Interactive CLI to add new students with real-time validation.
-  Smart Search: Case-insensitive search to find student records instantly.

### Technology Stack
-  Python 3.x
-  Pandas Library (Data Manipulation)
-  OS Library (File Management)

### File Structure
- Students_Grade_System.py: The main logic.
- Stud_data.csv: The persistent database (created automatically).





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

    
# 5. PLOTTING SECTION

sns.set_theme(style="whitegrid")

plt.figure(figsize=(8, 5))

ax = sns.barplot(data=df1, x='Student', y='Marks', hue='Grade')

sns.move_legend(ax, "upper left", bbox_to_anchor=(1, 1))

plt.title('Student Marks Comparison', fontsize=15)
plt.xlabel('Student Name', fontsize=12)
plt.ylabel('Marks Obtained', fontsize=12)

plt.tight_layout()

plt.show()





