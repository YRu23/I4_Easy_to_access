# I4_Easy_to_access

# CSV File

Set up the library
```python
import pandas as pd
from google.colab import files
```

Upload file
```python
uploaded = files.upload()
csv_file_name = list(uploaded.keys())[0]
```

Read the file and print the first few rows
```python
data = pd.read_csv(csv_file_name)
print(data.head())
```

Access tech: manual file download and load/read

Pros:
- easy to access. The CSV file is straightfoward and easy to understand.
- CSV file could be access, read and edit directly.
- widely supported in most platforms and systems.

Cons:
- require data cleaning before using data in csv file as they do not have a standard format in handling special characters
- the loading process takes longer with large datasets

# ZIP file
link to download zip file: https://zenodo.org/records/7665868

set up the libraries and upload the file
```python
import zipfile
from google.colab import files
import os

uploaded = files.upload()
zip_file_name = list(uploaded.keys())[0]  # This gets the name of the file
```
Extract the file and list it our
```python
with zipfile.ZipFile(zip_file_name, 'r') as zip_ref:
    
    extract_path = "/content/extracted_files"
    os.makedirs(extract_path, exist_ok=True)
    zip_ref.extractall(extract_path)
    print(f"Extracted files to {extract_path}")

extracted_files = os.listdir(extract_path)
print("Files in the extracted directory:")
print(extracted_files)
```

define the file path and read the zip file
```python
import pandas as pd

def print_csv_sample(file_name):
    file_path = os.path.join(extract_path, file_name)
    if os.path.exists(file_path):
        try:
            # error handling
            data = pd.read_csv(file_path, on_bad_lines='skip')
            print(f"Sample data from {file_name}:")
            print(data.head())
        except Exception as e:
            print(f"Failed to read {file_name}: {str(e)}")
    else:
        print(f"{file_name} not found in the extracted files.")

# show the result
print_csv_sample('movies.csv')
print_csv_sample('ratings.csv')
```

Access tech: manual file download and load/read.

Pros:
- simplify the file management and transfer as multiple files are bundle into one.
- efficient in downloading multiple files.

Cons:
- longer processing time required to upload the and read the file.
- limitation to upload large file size to some platform due to file size


# JSON 

set up the library and use API to access

```python
import requests

def fetch_json_sample(url):
    # GET request to the URL
    response = requests.get(url)

```
check if the request works and convert to Python dictionary
```python
    if response.status_code == 200:

        data = response.json()
```

Print a sample of the data, print keys of the dictionary and parts of data

  ```python
        print("Keys in the JSON data:", data.keys())
        
        if 'data' in data:
            print("Sample entries from 'data':")
            for entry in data['data'][:5]:  # Adjust the slice as needed to print more or less
                print(entry)
        else:
            print("No 'data' key found. Here's the full JSON data for reference:")
            print(data)
    else:
        print("Failed to retrieve data:", response.status_code)
```

URL link
```python
url = 'https://data.cityofnewyork.us/api/views/c3uy-2p5r/rows.json?accessType=DOWNLOAD'
fetch_json_sample(url)
```

Access tech: API connection over HTTPS to access structure data

Pros:
- easy to access and process the data
- JSOn file could easily read, understand the structure.
- supported by APIs easy to access with various types of applications.

Cons:
- might be challenging to process lage dataset
- JSON would require converting the string format into native data structures used by specific types of programming language.




