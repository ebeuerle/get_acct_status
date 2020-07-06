# RedLock Account status output to CSV 

Version: *1.0*
Author: *Eddie Beuerlein*

### Summary
This script will create a csv file that contains the account statuses from the RedLock UI.  This will help customer audit their cloud accounts.

### Requirements and Dependencies

1. Python 3.x or newer

2. OpenSSL 1.0.2 or newer

(if using on Mac OS, additional items may be nessessary.)

3. Pip

```sudo easy_install pip```

4. Requests (Python library)

```sudo pip install requests```

5. YAML (Python library)

```sudo pip install pyyaml```

### Configuration

1. Navigate to *get_acct_status/config/configs.yml*

2. Fill out your RedLock username, password, and customer name - if you are the only customer in your account then leave this blank.

3. CSV file will be named output.csv and located in the script directory

### Run

```
python runner.py

```
