# Pandas Data Cleaning Project

This project demonstrates how to clean and preprocess a customer data list using Python's Pandas library. It includes common data cleaning operations such as removing duplicates, handling missing values, standardizing formats, and filtering data based on specific conditions.

## Features

- **File Import**: Reads customer data from an Excel file for cleaning and transformation.
- **Data Deduplication**: Removes duplicate entries for accurate data representation.
- **Unnecessary Columns**: Drops columns that are not useful for analysis.
- **String Cleaning**:
  - Cleans and standardizes names by stripping unwanted characters.
  - Formats phone numbers consistently (e.g., `123-456-7890`).
- **Address Parsing**: Splits full addresses into `Street_Address`, `State`, and `Zip_Code` columns for better usability.
- **Standardization**: Converts `Yes/No` values to `Y/N` for uniformity.
- **Missing Data Handling**:
  - Replaces specific placeholder values like `N/a` with empty strings.
  - Fills empty fields with blank values for consistency.
- **Row Filtering**:
  - Removes rows where customers opted out of contact.
  - Excludes entries with missing or invalid phone numbers.
- **Index Reset**: Resets the DataFrame index after modifications.

## Prerequisites

- Python 3.x installed on your system.
- Libraries:
  - `pandas`
  - `openpyxl` (required for reading Excel files)

To install the dependencies, run:
```bash
pip install pandas openpyxl
```

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/pandas-data-cleaning.git
   ```
2. Navigate to the project directory:
   ```bash
   cd pandas-data-cleaning
   ```

## Usage

1. Place your input Excel file (e.g., `Customer Call List.xlsx`) in the working directory.
2. Update the script to include the correct file path for your dataset:
   ```python
   df = pd.read_excel(r"path_to_your_file.xlsx")
   ```
3. Run the script:
   ```bash
   python data_cleaning_script.py
   ```
4. After execution, the cleaned DataFrame will be displayed or saved as needed.

## Code Overview

The script includes the following key steps:

1. **Load Dataset**:
   ```python
   df = pd.read_excel(r"path_to_your_file.xlsx")
   ```

2. **Remove Duplicates**:
   ```python
   df = df.drop_duplicates()
   ```

3. **Drop Unnecessary Columns**:
   ```python
   df = df.drop(columns='Not_Useful_Column')
   ```

4. **Clean and Format Strings**:
   - Strip unwanted characters from names:
     ```python
     df["Last_Name"] = df["Last_Name"].str.strip("123._/")
     ```
   - Format phone numbers consistently:
     ```python
     df['Phone_Number'] = df['Phone_Number'].str.replace(r'[-/|]', '', regex=True)
     ```

5. **Parse Addresses**:
   ```python
   df[["Street_Address", "State", "Zip_Code"]] = df["Address"].str.split(',', n=2, expand=True)
   ```

6. **Standardize Yes/No Columns**:
   ```python
   df["Paying Customer"] = df["Paying Customer"].str.replace('Yes', 'Y').str.replace('No', 'N')
   ```

7. **Filter Rows**:
   ```python
   df = df[df["Do_Not_Contact"] != 'Y']
   ```

8. **Handle Missing Values**:
   ```python
   df = df.replace('N/a', '').fillna('')
   ```

9. **Reset Index**:
   ```python
   df = df.reset_index(drop=True)
   ```

## Output

The final cleaned dataset will:
- Exclude invalid or incomplete records.
- Contain well-structured, standardized columns ready for analysis.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

## Contributions

Contributions, bug reports, and feature requests are welcome! Feel free to fork this repository and submit a pull request.

---
