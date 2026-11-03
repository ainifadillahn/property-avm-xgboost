# Data

The raw data are **not included** in this repository.

## Source

USA Real Estate Dataset (Realtor.com listings, 2.2M+ records) on Kaggle:
https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset

- Accessed: `[insert date]`
- License / terms: `[insert from the Kaggle dataset page]`

## How to obtain the data

A free Kaggle account is required for either option.

### Option 1: Manual download

1. Log in to Kaggle and open the dataset page above.
2. Click the **Download** button on the dataset page (it appears after you log in).
3. Extract the downloaded archive.
4. Place the CSV file in this `data/` folder.

### Option 2: Download with code (Kaggle CLI)

1. In Kaggle, open **Settings → API → Create New Token**. This downloads `kaggle.json`.
2. Place `kaggle.json` in `~/.kaggle/` (Windows: `C:\Users\<username>\.kaggle\`).
3. Run from the repository root:

```
pip install kaggle
kaggle datasets download -d ahmedshahriarsakib/usa-real-estate-dataset -p data --unzip
```

### Option 3: Download with code (kagglehub)

```python
# pip install kagglehub
import kagglehub
path = kagglehub.dataset_download("ahmedshahriarsakib/usa-real-estate-dataset")
print(path)  # folder that contains the CSV file
```

After downloading, set the data path at the top of the notebook to the CSV file.

## Expected columns

`brokered_by`, `status`, `price`, `bed`, `bath`, `acre_lot`, `street`, `city`, `state`, `zip_code`, `house_size`, `prev_sold_date`

The data are subject to the original owner's terms. Please do not redistribute them.
