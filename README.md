# Phonepe-Pulse-Data-Visualization-and-Exploration-A-User-Friendly-Tool-Using-Streamlit-and-Plotly

LIBRARIES/ MODULES 
1. Ploty
2. pandas
3. mysql.connector
4. streamlit
5. json
6. git.repo.base

# WORKFLOW

# IMPORTING LIBRARIES
1. !pip install ["Name of the library"]
2. import pandas as pd
3. import mysql.connector as sql
4. import streamlit as st
5. import plotly.express as px
6. import os
7. import json
8. from streamlit_option_menu import option_menu
9. from PIL import Image
10. from git.repo.base import Repo

# DATA EXTRACTION
Cloning github using scripting pulse data:

    from git.repo.base import Repo
    Repo.clone_from("GitHub Clone URL","Path to get the cloded files")

# DATA TRANSFORMATION
Json file converted to DATAFRAMES:

     path1 = "Path of the JSON files"
    agg_trans_list = os.listdir(path1)

    #Give any column names that you want
    columns1 = {'State': [], 'Year': [], 'Quarter': [], 
    'Transaction_type': 
    [], 'Transaction_count': [],'Transaction_amount': []}

          for state in agg_trans_list:
             cur_state = path1 + state + "/"
             agg_year_list = os.listdir(cur_state)

          for year in agg_year_list:
              cur_year = cur_state + year + "/"
              agg_file_list = os.listdir(cur_year)

           for file in agg_file_list:
               cur_file = cur_year + file
               data = open(cur_file, 'r')
               A = json.load(data)

            for i in A['data']['transactionData']:
                name = i['name']
                count = i['paymentInstruments'][0]['count']
                amount = i['paymentInstruments'][0]['amount']
                columns1['Transaction_type'].append(name)
                columns1['Transaction_count'].append(count)
                columns1['Transaction_amount'].append(amount)
                columns1['State'].append(state)
                columns1['Year'].append(year)
                columns1['Quarter'].append(int(file.strip('.json')))
                df = pd.DataFrame(columns1)

                 #converting the dataframe into csv
             
                df.to_csv('filename.csv',index=False)

# DATABASE INSERTION
creating connection between python and sql:

               mydb = sql.connect(host="localhost",
                     user="username",
                     password="password",
                     database= "phonepe_pulse"
                      )
                    mycursor = mydb.cursor(buffered=True)

creating tables:

        mycursor.execute("create table 'Table name' (col1 varchar(100), col2 int, col3 int, col4 varchar(100), col5 int, col6 double)")

        for i,row in df.iterrows():
    
           #here %S means string values 
           sql = "INSERT INTO agg_trans VALUES (%s,%s,%s,%s,%s,%s)"
           mycursor.execute(sql, tuple(row))
        
           # the connection is not auto committed by default, so we must commit to save our changes
           mydb.commit()

# DASHBOARD CREATION

 Creating a insightful dashboard with ploty libraries

# DATA RETRIEVAL

Instead of using the "mysql_connector-python" library to connect MySql database to fetch the data.









