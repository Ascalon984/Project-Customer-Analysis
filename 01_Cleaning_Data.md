# ================================================ #
# BAGIAN 1: Pembersihan Data (Data Cleaning)       #
# TUJUAN  : Menyiapkan data agar siap dianalisis   #
# ================================================ #

import pandas as pd

# --- LOAD DATA ---
# Membaca file Excel dari direktori lokal pada sheet tertentu
df=pd.read_excel(r'C:\Users\User\Downloads\Customer-Purchase-History.xlsx', sheet_name='Sheet1')

# --- EXPLORE COLUMNS ---
# Mengekstrak daftar nama kolom ke dalam format list
print(df.columns.tolist())

# --- DATA INSPECTION ---
# Menampilkan 10 baris pertama untuk validasi struktur dan isi data
print(df.head(10))

// Output (Preview)
<img width="1051" height="206" alt="image" src="https://github.com/user-attachments/assets/eb489269-c201-4485-b0a6-1e0d97428d6a" />

# Mengecek jumlah nilai null di setiap kolom untuk menandai sebagai array kosong
print(df.isnull().sum())

// Output (Preview)
<img width="172" height="188" alt="image" src="https://github.com/user-attachments/assets/a592ca54-5972-48fc-b165-b737a13201ae" />

# --- DATA CLEANING: STRIP WHITESPACE ---
# Menghapus spasi di awal/akhir pada nama kolom
df.columns=df.columns.str.strip()

# Menghapus spasi di awal/akhir pada semua data bertipe objek (string)
df=df.apply(lambda x:x.str.strip() if x.dtypes == 'object' else x)

# --- DATA CLEANING: HANDLING MISSING VALUES ---
# Mengisi nilai kosong pada kolom 'Product' dan 'ProductCategory' dengan 'Unknown'
df['Product']=df['Product'].fillna('Unknown')
df['ProductCategory']=df['ProductCategory'].fillna('Unknown')

# --- COLUMN DATA FIX ---
# Memperbaiki typo pada nama kolom secara permanen (inplace)
df.rename(columns={'Quatity': 'Quantity'}, inplace=True)

# --- FINAL VALIDATION ---
# Menampilkan 10 baris pertama hasil pembersihan
print(df.head(10))

# Mengecek jumlah nilai null di setiap kolom untuk menandai sebagai array kosong
print(df.isnull().sum())

// Output (Preview)
<img width="900" height="381" alt="image" src="https://github.com/user-attachments/assets/c22c0099-7a86-481d-8375-20b6201a32ab" />

# --- DATA TYPE OPTIMIZATION ---
# Mengonversi tipe data secara otomatis ke tipe yang paling sesuai (Int64, string, dll.)
df=df.convert_dtypes()

# Memastikan kolom tanggal memiliki format datetime yang benar
# 'errors=coerce' akan mengubah data yang tidak valid menjadi NaT (Not a Time)
df['PurchaseDate']=pd.to_datetime(df['PurchaseDate'], errors='coerce')

# Memastikan kolom numerik memiliki format angka (float/int)
# 'errors=coerce' akan mengubah data non-numerik menjadi NaN (Not a Number)
df['Quantity']=pd.to_numeric(df['Quantity'], errors='coerce')
df['UnitPrice']=pd.to_numeric(df['UnitPrice'], errors='coerce')
df['ReviewRating']=pd.to_numeric(df['ReviewRating'], errors='coerce')
df['TotalPrice']=pd.to_numeric(df['TotalPrice'], errors='coerce')

# --- VERIFICATION ---
# Mengecek tipe data akhir setelah optimasi
print(df.dtypes)

// Output (Preview)
<img width="244" height="209" alt="image" src="https://github.com/user-attachments/assets/50ffbc9c-10d3-4d17-a21b-7702a43efcd5" />




