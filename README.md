# Visualisasi_data_covid
Perbandingan kasus covid 19 per hari di Indonesia dan Jepang

# Pengolahan data ini dilakukan dengan spyder
import pandas as pd # install library pandas
import matplotlib.pyplot as mtp # install library matplotlib untuk visualisasi data plot, mtp dapat diganti dengan yang lebih mudah seperti plot atau plt.

# memasukkan data frame (df) dari folder atau url
df = pd.read_csv('E:\Penelitin Data science\dataset\covid19.csv') 

# menentukan column yang akan digunakan untuk analysis 
kasus1 = df[df['Country/Region'] == 'Indonesia']
kasus2 = df[df['Country/Region'] == 'Japan'] 

# memilih data berdasarkan kasus terkonfirmasi
kasusIND = kasus1[kasus1['Confirmed']>0]
kasusJPN = kasus2[kasus2['Confirmed']>0]

# menentukan hari pertama kasus muncul
kasusIND['Date'] = pd.to_datetime(kasusIND['Date'])
kasusJPN['Date'] = pd.to_datetime(kasusJPN['Date'])
kasusIND.head()

# membuat rumus untuk menentukan (hari ke-) kasus covid terdata 
kasusIND['BaseDate'] = pd.to_datetime('2020-03-02')
kasusIND.head()
kasusJPN['BaseDate'] = pd.to_datetime('2020-01-22')
kasusJPN.head()

# menentukan hari ke dengan rumus Date - BaseDate
kasusIND['HariKe'] = kasusIND['Date'] - kasusIND['BaseDate']
kasusJPN['HariKe'] = kasusJPN['Date'] - kasusJPN['BaseDate']

# membuat time delta untuk fungsi numerik
kasusIND.HariKe = kasusIND.HariKe/pd.Timedelta(1, unit = 'd') 
kasusJPN.HariKe = kasusJPN.HariKe/pd.Timedelta(1, unit = 'd') 

# visualisasi data plot
mtp.plot(kasusIND.HariKe, kasusIND.Confirmed)
mtp.plot(kasusJPN.HariKe, kasusJPN.Confirmed)
mtp.xlabel('Hari Ke-')
mtp.ylabel('Jumlah Kasus')
mtp.legend('Indonesia', 'Jepang')
mtp.title('Perbandangin jumlah kasus per Hari di Indonesia dan Jepang')
mtp.show()
