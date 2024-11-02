1. Pertama-tama, buat sheet baru di Microsoft Excel, lalu input data yang diinginkan
dengan format seperti dibawah ini.
![image](https://github.com/user-attachments/assets/2e52cf75-43b2-4ac9-997d-f0d9c61f81f9)


Kolom A = ID Mata Kuliah

Kolom B = SKS

Kolom C = Nama Mata Kuliah

Kolom D = Semester Ajar

Pastikan format sesuai dengan kolom pada tabel di NetBeans untuk menghindari
terjadinya error. Setelah itu, simpan file sebagai file csv lalu letakkan Directory nya
ke Desktop.
![image](https://github.com/user-attachments/assets/3932bad4-f93a-4b91-9028-a6deffee209f)


2. Setelah itu masuk ke NetBeans, buat button baru lalu letakkan di area yang
diinginkan. Kemudain beri nama “Upload” atau “Kirim”, lalu change variable name
menjadi “btnUpload” atau “btnKirim”.
![image](https://github.com/user-attachments/assets/5de9b2b8-0096-4ec7-860e-ace2a7e31673)
![image](https://github.com/user-attachments/assets/e1338018-8865-4877-8445-4759b362dd97)



3. Langkah selanjutnya, pada ‘Events’ pilih ‘Action’ lalu ‘actionPerformed’
![image](https://github.com/user-attachments/assets/23c58c55-0549-4eb5-ae0e-b92343ea5e5a)

   
Lalu nanti akan diarahkan ke lokasi kodingannya seperti ini.
![image](https://github.com/user-attachments/assets/2bc3113b-2a3a-4f7c-b9d4-fcee91736942)


4. Setelah itu mulai untuk mengkoding buttonnya, berikut adalah code nya.
JFileChooser jfc = new
JFileChooser(FileSystemView.getFileSystemView().getHomeDirectory());
 int returnValue = jfc.showOpenDialog(null);
 if (returnValue == JFileChooser.APPROVE_OPTION) {
 File filePilihan = jfc.getSelectedFile();
 System.out.println("yang dipilih : " + filePilihan.getAbsolutePath());
 try (BufferedReader br = new BufferedReader(new
FileReader(filePilihan))) {
 Class.forName(driver);
 con = DriverManager.getConnection(koneksi, user, password);
 String baris;
 String pemisah = ";";
 while ((baris = br.readLine()) != null) {
 String[] dataMhs = baris.split(pemisah);
 String KMK = dataMhs[0];
 String SKS = dataMhs[1];
 String NMK = dataMhs[2];
 String SA = dataMhs[3];
 if (!KMK.isEmpty() && !SKS.isEmpty() && !NMK.isEmpty() &&
!SA.isEmpty()) {
 String sql = "INSERT INTO MATA_KULIAH (KodeMK, SKS,
namaMK, SemesterAjar) VALUES (?,?,?,?)";
 pst = con.prepareStatement(sql);
 pst.setString(1, KMK);
 pst.setString(2, SKS);
 pst.setString(3, NMK);
 pst.setString(4, SA);
 pst.executeUpdate();
 JOptionPane.showMessageDialog(null, "Done");
 } else {
 JOptionPane.showMessageDialog(null, "Failed to insert a row due
to missing data.");
 }
 }
 } catch (FileNotFoundException ex) {
java.util.logging.Logger.getLogger(Mata_Kuliah.class.getName()).log(java.util.l
ogging.Level.SEVERE, null, ex);
 } catch (IOException | SQLException | ClassNotFoundException ex) {
java.util.logging.Logger.getLogger(Mata_Kuliah.class.getName()).log(java.util.l
ogging.Level.SEVERE, null, ex);
 } finally {
 try {
 if (pst != null) {
 pst.close();
 }
 if (con != null) {
 con.close();
 }
 } catch (SQLException ex) {
java.util.logging.Logger.getLogger(Mata_Kuliah.class.getName()).log(java.util.l
ogging.Level.SEVERE, null, ex);
 }
 }
 }
 tampil();


5. Setelah itu, run programnya dan tampilannya akan seperti ini.
![image](https://github.com/user-attachments/assets/ec03f256-8556-4762-9114-e588fd5ef9d6)

   
6. Langkah selanjutnya, klik button ‘Upload’, setelah itu pilih file .csv yang tadi sudah
kita buat di Microsoft Excel. Kemudian klik open.
![image](https://github.com/user-attachments/assets/1fcb54f7-947d-4f09-802c-f1437aea8a02)


7. Setelah itu, akan ada pop up bertuliskan “Done” berulang berulang sesuai jumlah data
yang ada didalam file. Lalu output nya akan menjadi seperti dibawah ini
![image](https://github.com/user-attachments/assets/275c24f5-68d0-4562-aac1-27a94d2c524e)
![image](https://github.com/user-attachments/assets/abffd8df-6d40-40f7-8cdc-b195f5f9eacc)


8. Terakhir, bisa dilihat bahwa data telah terinput dengan sukses.
   
