#PyCitySchools

District Summary

Perform the necessary calculations and then create a high-level snapshot of the district's key metrics in a DataFrame.
    Include the following:
    - Total number of unique schools
    - Total students
    - Total budget
    - Average math score
    -mAverage reading score
    - % passing math (the percentage of students who passed math)
    - % passing reading (the percentage of students who passed reading)
    - % overall passing (the percentage of students who passed math AND reading)


School Summary

Perform the necessary calculations and then create a DataFrame that summarizes key metrics about each school.
    Include the following:
    - School name
    - School type
    - Total students
    - Total school budget
    - Per student budget
    - Average math score
    - Average reading score
    - % passing math (the percentage of students who passed math)
    - % passing reading (the percentage of students who passed reading)
    - % overall passing (the percentage of students who passed math AND reading)


list of sources used:

    - 01: https://pandas.pydata.org/docs/reference/api/pandas.Series.value_counts.html
    - 02: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html
    - 03: https://www.datacamp.com/tutorial/pandas-sort-values?utm_source=google&utm_medium=paid_search&utm_campaignid=19589720830&utm_adgroupid=157156377311&utm_device=c&utm_keyword=&utm_matchtype=&utm_network=g&utm_adpostion=&utm_creative=684753665233&utm_targetid=dsa-2218886984100&utm_loc_interest_ms=&utm_loc_physical_ms=9032205&utm_content=&utm_campaign=230119_1-sea~dsa~tofu_2-b2c_3-us_4-prc_5-na_6-na_7-le_8-pdsh-go_9-na_10-na_11-na-jan24&gad_source=1&gclid=EAIaIQobChMIr5fOs5bjgwMV-tAWBR2dsQC4EAAYASAAEgKvqfD_BwE
    - 04: https://pandas.pydata.org/docs/reference/api/pandas.cut.html

    source 01 was used for value_counts() to gather counts per variable

        per_school_counts = school_data_complete["school_name"].value_counts()
        school_students_passing_math = school_data_complete[(school_data_complete["math_score"] >= 70)]["school_name"].value_counts()
    
    source 02 was used to select a certain set of data using groupby()

        per_school_budget = school_data_complete.groupby(["school_name"])["budget"].mean()
        per_school_math = school_data_complete.groupby(["school_name"])["math_score"].mean()
    
    source 03 was used to sort data by descending/ascending using sort_values()

        top_schools = per_school_summary.sort_values(['% Overall Passing'], ascending=False)
        bottom_schools = per_school_summary.sort_values(['% Overall Passing'], ascending=True)
    
    source 04 was used for pd.cut

        school_spending_df["Spending Ranges (Per Student)"] = pd.cut(per_school_capita, spending_bins, labels=labels)
    

important note: there was a warning for codes similar to the one below, so i asked peers for help to get rid of the warning

    spending_math_scores = school_spending_df.groupby(["Spending Ranges (Per Student)"],observed=False)["Average Math Score"].mean()
    size_math_scores = per_school_summary.groupby(["School Size"],observed=False)["Average Math Score"].mean()