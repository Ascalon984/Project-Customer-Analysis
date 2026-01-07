# ========================================================== #
# BAGIAN: Visualisasi Data (Data Visualization)              #
# TUJUAN: Menyajikan tren dan komposisi data secara visual   #
# ========================================================== #
import matplotlib.pyplot as plt

# --- 11. FUNGSI TREN PENJUALAN TOP 5 KATEGORI ---
# Menampilkan grafik garis untuk melihat fluktuasi penjualan 5 kategori terbesar
def tren(kolom):
    top_kategori = (df.groupby('ProductCategory')[kolom].sum().nlargest(5).index)
    data = df[df['ProductCategory'].isin(top_kategori)]
    tren_data = (data.groupby(['PurchaseDate', 'ProductCategory'])[kolom].sum().unstack())
    plt.figure(figsize=(12, 6.5))
    tren_data.plot(marker='o', ax=plt.gca())
    plt.title('Tren Distribusi Penjualan Top 5 Kategori Produk')
    plt.ylabel('Jumlah Unit')
    plt.xlabel('Periode')
    plt.xticks(rotation=25)
    plt.grid(True, linestyle='--', alpha=0.3)
    plt.legend(title='Kategori Produk')
    plt.tight_layout()
    plt.show()
tren('Quantity')

// Output (Preview)
<img width="1190" height="724" alt="image" src="https://github.com/user-attachments/assets/93770c5c-c6a3-4450-83b7-c8aadabc2930" />

# --- 12. FUNGSI TREN KATEGORI SPESIFIK ---
# Memantau tren satu kategori tertentu secara mendalam
def tren_spesifik(kolom, kategori_spesifik=None):
    if kategori_spesifik:
        data = df[df['ProductCategory'].str.contains(kategori_spesifik, case=False, na=False)]
        judul = f'Tren Penjualan Kategori: {kategori_spesifik}'
    tren_data = data.groupby(['PurchaseDate', 'ProductCategory'])[kolom].sum().unstack()
    plt.figure(figsize=(12, 6.5))
    tren_data.plot(marker='o', ax=plt.gca())
    plt.title(judul, fontsize=14, pad=15)
    plt.ylabel(f'Jumlah {kolom}')
    plt.xlabel('Periode')
    plt.xticks(rotation=25)
    plt.grid(True, linestyle='--', alpha=0.3)
    plt.legend(title='Kategori Produk', bbox_to_anchor=(1, 1), loc='upper left')
    plt.tight_layout()
    plt.show()
tren_spesifik('Quantity', kategori_spesifik='Office Supplies')

// Output (Preview)
<img width="1195" height="719" alt="image" src="https://github.com/user-attachments/assets/1aaf0077-a7bb-4f19-aa10-f2e0db6af9db" />

# --- 13. FUNGSI KOMPOSISI PENDAPATAN (PIE CHART) ---
# Melihat persentase kontribusi setiap kategori terhadap total pendapatan
def visualisasi_pie_pendapatan():
    data_pie = df.groupby('ProductCategory')['TotalPrice'].sum()
    plt.figure(figsize=(10, 8))
    explode = [0.05] * len(data_pie) 
    data_pie.plot(kind='pie', autopct='%1.1f%%', startangle=140, explode=explode, colors=plt.cm.Paired.colors, shadow=True)
    plt.title('Kontribusi Pendapatan per Kategori Produk', fontsize=14, pad=20)
    plt.ylabel('')
    plt.legend(title="Kategori", loc="center left", bbox_to_anchor=(1, 0, 0.5, 1))
    plt.tight_layout()
    plt.show()
visualisasi_pie_pendapatan()

// Output (Preview)
<img width="984" height="858" alt="image" src="https://github.com/user-attachments/assets/66a0645c-5b56-45d8-b91c-dcb0869b8fd6" />


