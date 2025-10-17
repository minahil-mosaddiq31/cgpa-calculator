import streamlit as st
import pandas as pd

st.set_page_config(page_title="GPA & CGPA Calculator", page_icon="🎓", layout="centered")

st.title("🎓 Student GPA & CGPA Calculator (with Credit Hours)")

# Step 1: Ask number of subjects
num_subjects = st.number_input("Enter number of subjects:", min_value=1, max_value=15, step=1)

subjects = []
marks = []
credits = []

st.subheader("Enter Subject Details")

# Step 2: Get subject info
for i in range(num_subjects):
    col1, col2, col3 = st.columns(3)
    with col1:
        subject = st.text_input(f"Subject {i+1} Name", key=f"sub_{i}")
    with col2:
        mark = st.number_input(f"Marks for {subject or f'Subject {i+1}'}", 0, 100, key=f"mark_{i}")
    with col3:
        credit = st.number_input(f"Credit Hours", 1.0, 5.0, 3.0, step=0.5, key=f"credit_{i}")

    subjects.append(subject)
    marks.append(mark)
    credits.append(credit)

# Step 3: Define grading logic
def get_grade_point(mark):
    if mark >= 90: return ("A+", 4.0)
    elif mark >= 85: return ("A", 3.7)
    elif mark >= 80: return ("A-", 3.5)
    elif mark >= 75: return ("B+", 3.3)
    elif mark >= 70: return ("B", 3.0)
    elif mark >= 65: return ("C+", 2.5)
    elif mark >= 60: return ("C", 2.0)
    elif mark >= 50: return ("D", 1.0)
    else: return ("F", 0.0)

# Step 4: Calculate and display results
if st.button("Calculate CGPA"):
    grades, grade_points, total_points = [], [], []

    for m, c in zip(marks, credits):
        grade, point = get_grade_point(m)
        grades.append(grade)
        grade_points.append(point)
        total_points.append(point * c)

    df = pd.DataFrame({
        "Subject": subjects,
        "Marks": marks,
        "Credit Hours": credits,
        "Grade": grades,
        "Grade Point": grade_points,
        "Total Points (GP × Credit)": total_points
    })

    total_credits = sum(credits)
    total_grade_points = sum(total_points)
    cgpa = round(total_grade_points / total_credits, 2)
    percentage = round(sum(marks) / len(marks), 2)

    st.success(f" Your CGPA is: **{cgpa}**")
    st.info(f" Overall Percentage: **{percentage}%**")
    st.dataframe(df, use_container_width=True)
