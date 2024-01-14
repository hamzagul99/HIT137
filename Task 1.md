import pandas as pd
import os

csv_folder = os.getcwd()
output_txt_file = os.getcwd() + '\\output.txt'

# Read all CSV files and extract columns with strings (not numbers)
all_texts = []

for file in os.listdir(csv_folder):
    if file.endswith('.csv'):
        df = pd.read_csv(os.path.join(csv_folder, file))
        
        # Iterate through columns and select only those with string data
        string_columns = [col for col in df.columns if df[col].dtype == 'O']  
        
        # Extract and append only the string values from selected columns
        for col in string_columns:
            all_texts.extend(df[col].astype(str).tolist())

with open(output_txt_file, 'w', encoding='utf-8') as txt_file:
    txt_file.write('\n'.join(all_texts))
