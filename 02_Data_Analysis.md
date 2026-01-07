# ============================================================== #
# BAGIAN: Analisis Data (Exploratory Data Analysis)              #
# TUJUAN: Mendapatkan insight dari data yang telah dibersihkan   #
# ============================================================== #

# --- 1. RINGKASAN STATISTIK DESKRIPTIF ---
# Menghitung statistik utama dan membulatkan ke 3 angka di belakang koma
ringkasan = df[['Quantity', 'UnitPrice', 'ReviewRating', 'TotalPrice']].describe().round(3)
print(ringkasan)

// Output (Preview)
<img width="381" height="159" alt="image" src="https://github.com/user-attachments/assets/2b6c69c0-7ee4-4594-827e-8b3dc8fc4504" />

# --- 2. ANALISIS KATEGORI TERLARIS ---
# Menghitung total pendapatan berdasarkan kategori produk (diurutkan dari yang tertinggi)
top_categories = df.groupby('ProductCategory')['TotalPrice'].sum().sort_values(ascending=False)
print(top_categories)

// Output (Preview)
<img width="240" height="86" alt="image" src="https://github.com/user-attachments/assets/bdd7795c-a8db-46a4-ba1d-7357ded94318" />

# --- 3. ANALISIS TREN PENJUALAN BULANAN ---
# Mengelompokkan total penjualan berdasarkan periode bulan
monthly_sales = df.groupby(df['PurchaseDate'].dt.to_period('M'))['TotalPrice'].sum().head(10)
print(monthly_sales)

// Output (Preview)
<img width="301" height="206" alt="image" src="https://github.com/user-attachments/assets/53e621fb-dcc0-422c-a08c-0395cde80f45" />

# --- 4. ANALISIS METODE PEMBAYARAN ---
# Menghitung frekuensi penggunaan setiap metode pembayaran
payment_method = df['PaymentMethod'].value_counts()
print(payment_method)

// Output (Preview)
<img width="187" height="121" alt="image" src="https://github.com/user-attachments/assets/3f82e128-82f1-4294-86bc-a296bc899721" />

# ============================================== #
# BAGIAN: Fungsi Pencarian & Ranking (Lookup)    #
# TUJUAN: Mempermudah pencarian data spesifik    #
# ============================================== #

# --- 5. FUNGSI LOOKUP CUSTOMER ---
# Mencari profil pelanggan berdasarkan CustomerID
def lookup(id):
    data=df[df['CustomerID'].str.contains(id, case=False, na=False)]
    if data.empty:
        return f'Data Customer {id} Tidak Tersedia'
    return data.iloc[0]
print(lookup('C7521'))

// Output (Preview)
<img width="279" height="191" alt="image" src="https://github.com/user-attachments/assets/708c37ea-092c-4428-9895-6dc2611cdcc9" />

 --- 6. FUNGSI ANALISIS SPESIFIK PRODUK ---
# Mencari distribusi data tertentu (misal: Metode Pembayaran) untuk produk tertentu
def distribusi_data(produk, kolom):
    data=df[df['Product'].str.contains(produk, case=False, na=False)]
    if data.empty:
        return f'Data Produk {produk} Tidak Tersedia'
    return data[kolom].value_counts()
print(distribusi_data('Tablet', 'PaymentMethod'))

// Output (Preview)
<img width="183" height="124" alt="image" src="https://github.com/user-attachments/assets/63050790-7717-4c66-969b-267fc3ea63c7" />

# --- 7. FUNGSI TOP RANKING (LEADERBOARD) ---
# Menampilkan 10 data teratas berdasarkan kolom tertentu dengan format tabel
from tabulate import tabulate

def top_penjualan(kolom):
    data=df.sort_values(by=kolom, ascending=False).head(10)
    if data.empty:
        return f'Kolom {kolom} Tidak Ditemukan'
    data=data.reset_index(drop=True)
    data.insert(0, 'Rank', range(1, len(data)+1))
    return data[['Product', 'ProductCategory', kolom, 'Rank']]
variabel=top_penjualan('TotalPrice')
if variabel is not None:
    print(tabulate(variabel, headers='keys', tablefmt='pretty', showindex=False))
else:
    print('Gagal Membentuk Tabel')

// Output (Preview)
<img width="355" height="242" alt="image" src="https://github.com/user-attachments/assets/620bad50-f2e1-4b0c-94ce-93baa40d8824" />

# --- 8. FUNGSI EVALUASI RATING PRODUK ---
# Menentukan predikat kepuasan pelanggan berdasarkan rata-rata rating berdasarkan produk tertentu
def kepuasan_pelanggan(produk, kolom):
    data=df[df['Product'].str.contains(produk, case=False, na=False)]
    if data.empty:
        return f'Data {produk} Tidak Ditemukan'
    variabel=data[kolom].mean()
    if variabel == 5:
        return 'Sangat Memuaskan'
    elif variabel == 4:
        return 'Memuaskan'
    elif variabel == 3:
        return 'Cukup Memuaskan'
    elif variabel == 2:
        return 'Kurang Memuaskan'
    else:
        return 'Tidak Puas'
print(kepuasan_pelanggan('Phone', 'ReviewRating'))

// Output (Preview)
<img width="163" height="53" alt="image" src="https://github.com/user-attachments/assets/98880c07-30e0-4eca-851e-370fe3ab9fe6" />

# --- 9 & 10. SEGMENTASI PRODUK (KRITERIA STRATEGIS) ---
# Menentukan status produk berdasarkan kombinasi Harga Total dan Rating
import numpy as np
kondisi=[
    (df['TotalPrice'] >= 3000) & (df['ReviewRating'] >= 4),
    (df['TotalPrice'] >= 2000) & (df['ReviewRating'] >=3),
    (df['TotalPrice'] >= 1000)
]
status=['Unggulan', 'Potensial', 'Ekonomis']
df['Kriteria']=np.select(kondisi, status, default='Tidak Termasuk')
print(df[['Product', 'ProductCategory', 'TotalPrice', 'ReviewRating', 'Kriteria']].head(10))

// Output (Preview)
<img width="503" height="190" alt="image" src="https://github.com/user-attachments/assets/7964ef8a-e8ff-4bde-9eaa-57070e9c06bb" />

# --- RINGKASAN HASIL SEGMENTASI ---
# Menghitung distribusi jumlah produk untuk setiap kriteria
kondisi=[
    (df['TotalPrice'] >= 3000) & (df['ReviewRating'] >= 4),
    (df['TotalPrice'] >= 2000) & (df['ReviewRating'] >=3),
    (df['TotalPrice'] >= 1000)
]
status=['Unggulan', 'Potensial', 'Ekonomis']
df['Kriteria']=np.select(kondisi, status, default='Tidak Termasuk')
jumlah=np.unique(df['Kriteria'], return_counts=True)
hasil=dict(zip(*jumlah))
print(hasil)

// Output (Preview)
<img width="816" height="40" alt="image" src="https://github.com/user-attachments/assets/0395ff5f-5d19-4751-9f37-f80c6fc55484" />









