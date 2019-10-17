# Dataframe_Encryption
Encrypt and decrypt sensitive pandas dataframe. 

# Pandas dataframe encryption and decryption
**Purpose:** Work on a sensitive data file? You can use AES-256 encryption to store the data. 

**Author:** Pranab Das (Twitter : @pranab_das) 

**Version:** 20191017

**Requirement:** Pycrypt, simplecrypt


```python
import pandas as pd
from io import StringIO
from simplecrypt import encrypt, decrypt
from getpass import getpass
```

Create a dataframe.


```python
data = {'Date': ['2019-10-10', '2019-10-12', '2019-10-15'], \
        'Credit Amount (SGD)': [40.00, 500.00, 60.00],\
        'Transaction type': ['CC *1234', 'Bank transfer', 'CC *1234']}
df = pd.DataFrame(data)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Credit Amount (SGD)</th>
      <th>Transaction type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>2019-10-10</td>
      <td>40.0</td>
      <td>CC *1234</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2019-10-12</td>
      <td>500.0</td>
      <td>Bank transfer</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2019-10-15</td>
      <td>60.0</td>
      <td>CC *1234</td>
    </tr>
  </tbody>
</table>
</div>



Store data in csv format. 


```python
data_csv = df.to_csv(index=False)
```

Encrypt the data using password : bfsS#@308sW (Example)


```python
print('Enter a password for encryption.')
encdata = encrypt(getpass("password: "), data_csv)
```

    Enter a password for encryption.
    password: ········


Write/store the encrypted data in a file. 


```python
file_w = open('file.enc', 'wb')
file_w.write(encdata)
file_w.close()
```

Open/Decrypt the data from encrypted file. 


```python
file_r = open('file.enc','rb').read()
```


```python
print('Enter password for decryption.')
CSVplaintext = decrypt(getpass("password: "), file_r).decode('utf8')
```

    Enter password for decryption.
    password: ········



```python
CSVplaintext
```




    'Date,Credit Amount (SGD),Transaction type\n2019-10-10,40.0,CC *1234\n2019-10-12,500.0,Bank transfer\n2019-10-15,60.0,CC *1234\n'




```python
DATA=StringIO(CSVplaintext)
```


```python
df = pd.read_csv(DATA)
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Credit Amount (SGD)</th>
      <th>Transaction type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>2019-10-10</td>
      <td>40.0</td>
      <td>CC *1234</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2019-10-12</td>
      <td>500.0</td>
      <td>Bank transfer</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2019-10-15</td>
      <td>60.0</td>
      <td>CC *1234</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
