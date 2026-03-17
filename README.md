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

# 3. Penambahan Menu MCU Di navbar
Copy Dari DlgIGD.java lalu refactor project menjadi DlgMCU.java di Folder simrskhanza
Edit di bagian tampil() agar poli MCU saja yang tampil di Menu ini 
```
ps=koneksi.prepareStatement("select reg_periksa.no_reg,reg_periksa.no_rawat,reg_periksa.tgl_registrasi,reg_periksa.jam_reg,"+
                               "reg_periksa.kd_dokter,dokter.nm_dokter,reg_periksa.no_rkm_medis,pasien.nm_pasien,pasien.jk,concat(reg_periksa.umurdaftar,' ',reg_periksa.sttsumur)as                                 umur,poliklinik.nm_poli,"+  "reg_periksa.p_jawab,reg_periksa.almt_pj,reg_periksa.hubunganpj,reg_periksa.biaya_reg,reg_periksa.stts_daftar,penjab.png_jawab,reg_periksa.stts,reg_periksa.kd_pj,reg_periksa.status_bayar "+
                               "from reg_periksa inner join dokter inner join pasien inner join poliklinik inner join penjab "+
                               "on reg_periksa.kd_dokter=dokter.kd_dokter and reg_periksa.no_rkm_medis=pasien.no_rkm_medis "+
                               "and reg_periksa.kd_pj=penjab.kd_pj and reg_periksa.kd_poli=poliklinik.kd_poli  where  "+
                               "poliklinik.kd_poli='U0074' and reg_periksa.tgl_registrasi between ? and ? "+
                               (TCari.getText().trim().equals("")?"":"and (reg_periksa.no_reg like ? or reg_periksa.no_rawat like ? or reg_periksa.tgl_registrasi like ? or "+
                               "reg_periksa.kd_dokter like ? or dokter.nm_dokter like ? or reg_periksa.no_rkm_medis like ? or "+
                               "reg_periksa.stts_daftar like ? or pasien.nm_pasien like ? or poliklinik.nm_poli like ? or "+
                               "reg_periksa.p_jawab like ? or reg_periksa.almt_pj like ? or reg_periksa.hubunganpj like ? or "+
                               "penjab.png_jawab like ?) ")+terbitsep+" order by reg_periksa.no_rawat "); 
```
Ketika sudah diganti di bagian tsb, Tambahkan di tabel Tampil Untuk menampilkan Menu Paket Pemeriksaan MCU  
Tambahkan didlm while(rs.next()) 
```
Sequel.cariIsi("SELECT jns_perawatan_lab.nm_perawatan " +  // ← nm_perawatan di kolom 1
                                    "FROM reg_periksa " +
                                    "INNER JOIN periksa_lab ON periksa_lab.no_rawat = reg_periksa.no_rawat " +
                                    "INNER JOIN jns_perawatan_lab ON jns_perawatan_lab.kd_jenis_prw = periksa_lab.kd_jenis_prw " +
                                    "WHERE reg_periksa.no_rawat = ? ORDER BY jns_perawatan_lab.kd_jenis_prw",
                                    rs.getString(2))  // ← no_rawat di index 
```
Jangan Lupa tambahkan jumlah kolom dan beri nama Paket Pemeriksaan MCU


# 4. Tambah Instansi di Tabel RawatIap
Buka di Folder simrskhanza lalu di file dlgKamarInap.java 
Tambahkan Jumlah kolom terlebih dahulu, kemudian tambahkan nama Instansi/Perusahaan.
Ketika sudah, tambahkan di bagian tampil ()
Tambahkan didlm while(rs.next()) 
```
Sequel.cariIsi("select perusahaan_pasien.nama_perusahaan, pasien.perusahaan_pasien, reg_periksa.no_rkm_medis from reg_periksa inner join pasien on reg_periksa.no_rkm_medis=pasien.no_rkm_medis inner join perusahaan_pasien on pasien.perusahaan_pasien=perusahaan_pasien.kode_perusahaan where reg_periksa.no_rkm_medis=?",rs.getString(2)),
```

# 5. Tambah Instansi di Tabel Rawa Jalan
Buka di Folder simrskhanza lalu di file dlgKasirRalan.java 
Tambahkan Jumlah kolom terlebih dahulu, kemudian tambahkan nama Instansi/Perusahaan.
Ketika sudah, tambahkan di bagian tampil ()
Tambahkan didlm while(rs.next()) 
```
Sequel.cariIsi("select perusahaan_pasien.nama_perusahaan, pasien.perusahaan_pasien, reg_periksa.no_rkm_medis from reg_periksa inner join pasien on reg_periksa.no_rkm_medis=pasien.no_rkm_medis inner join perusahaan_pasien on pasien.perusahaan_pasien=perusahaan_pasien.kode_perusahaan where reg_periksa.no_rkm_medis=?",rskasir.getString(7)),
```



