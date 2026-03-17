# Dokumentasi-Kustome-SIMRS
kostume SIMRS KHANZA

# 1. Surat Sakit ODC 
Penambahan DPJP IGD ke Poli ( di dalam Folder Surat )
di File SuratSakit.java
## Codingan Yang Di Kostume `rptSuratSakit4 tambahkan codingan di bawah ini

```
param.put("namadokterdpjp",Sequel.cariIsi("select dokter.nm_dokter, dpjp_ranap.kd_dokter, reg_periksa.no_rawat from reg_periksa inner join dpjp_ranap on reg_periksa.no_rawat=dpjp_ranap.no_rawat inner join dokter on dpjp_ranap.kd_dokter=dokter.kd_dokter where reg_periksa.no_rawat=?", TNoRw.getText()));
```


# 2. Penambahan Informasi Nama Akun
Difolder simrskhanza lalu frmUtama.java
ubah di lblUser
Tambhkan variable lblStts1 atau copy dari lblStts
Ketika ganti password di aplikasi bisa dilakukan
```
lblStts1.setText("Nama User : ");
lblUser1.setText(Sequel.cariIsi("select pegawai.nama from pegawai where pegawai.nik=?",akses.getkode()));
```
