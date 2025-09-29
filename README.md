<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Pendaftaran Pasien - RS Rusydan Bara</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #a8edea, #BA68C8);
      margin: 0;
      padding: 0;
    }

    .container {
      width: 60%;
      margin: 50px auto;
      background-color: white;
      border-radius: 12px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
      padding: 30px 40px;
    }

    h1 {
      text-align: center;
      color: #2b6777;
    }

    label {
      font-weight: bold;
      display: block;
      margin-top: 15px;
    }

    input[type="text"],
    input[type="number"],
    textarea,
    select {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }

    .radio-group {
      margin-top: 5px;
    }

    .radio-group input {
      margin-right: 10px;
    }

    input[type="submit"] {
      margin-top: 25px;
      background-color: #2b6777;
      color: white;
      padding: 12px 20px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }

    input[type="submit"]:hover {
      background-color: #1e4d5a;
    }

    .hasil {
      background-color: #f2f2f2;
      padding: 20px;
      margin-top: 30px;
      border-radius: 10px;
      border: 1px solid #ccc;
    }

    .hasil h2 {
      margin-top: 0;
      color: #333;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>Formulir Pendaftaran Pasien</h1>
  <h1>🩺RS RUSYDAN BARA⚕️</h1>
  <h1>⭐⭐⭐⭐⭐</h1>

  <form id="formPendaftaran">
    <label for="nama">Nama Lengkap:</label>
    <input type="text" name="nama" required>

    <label for="umur">Umur:</label>
    <input type="number" name="umur" required>

    <label for="telepon">Nomor Telepon:</label>
    <input type="text" name="telepon" required placeholder="Contoh: 081234567890">

    <label for="bpjs">Nomor BPJS (jika ada):</label>
    <input type="text" name="bpjs" placeholder="Contoh: 0001234567890">

    <label for="alamat">Alamat:</label>
    <textarea name="alamat" rows="3" required></textarea>

    <label>Jenis Kelamin:</label>
    <div class="radio-group">
      <input type="radio" name="jk" value="Laki-laki" required> Laki-laki
      <input type="radio" name="jk" value="Perempuan"> Perempuan
    </div>

    <label for="goldar">Golongan Darah:</label>
    <select name="goldar" required>
      <option value="">-- Pilih Golongan Darah --</option>
      <option value="A">A</option>
      <option value="B">B</option>
      <option value="AB">AB</option>
      <option value="O">O</option>
    </select>

    <label for="poli">Poli Tujuan:</label>
    <select name="poli" required>
      <option value="">-- Pilih Poli --</option>
      <option value="Umum">Umum</option>
      <option value="Gigi">Gigi</option>
      <option value="Anak">Anak</option>
      <option value="Penyakit Dalam">Penyakit Dalam</option>
      <option value="Kandungan">Kandungan</option>
    </select>

    <label for="dokter">Pilih Dokter:</label>
    <select name="dokter" required>
      <option value="">-- Pilih Dokter --</option>
      <option value="dr. Bara,Sp.B.">dr. Bara,Sp.B.</option>
      <option value="dr. Estu,Sp.U">dr. Estu,Sp.U.</option>
    </select>

    <label for="jenis_obat">Jenis Obat:</label>
    <select name="jenis_obat" required>
      <option value="">-- Pilih Jenis Obat --</option>
      <option value="Tablet">Tablet</option>
      <option value="Kapsul">Kapsul</option>
      <option value="Cair">Cair</option>
      <option value="Salep">Salep</option>
    </select>

    <label for="keluhan">Keluhan:</label>
    <textarea name="keluhan" rows="3" placeholder="Contoh: Demam, batuk, pusing..." required></textarea>

    <label for="riwayat">Riwayat Penyakit:</label>
    <textarea name="riwayat" rows="3" placeholder="Contoh: Diabetes, Asma, Riwayat Operasi..." required></textarea>

    <input type="submit" value="Daftar">
  </form>

  <div id="hasil" class="hasil" style="display:none;"></div>
</div>

<script>
document.getElementById("formPendaftaran").addEventListener("submit", function(e) {
  e.preventDefault(); // Biar nggak reload halaman

  // Ambil data
  const nama = this.nama.value;
  const umur = this.umur.value;
  const telepon = this.telepon.value;
  const bpjs = this.bpjs.value || "-";
  const alamat = this.alamat.value;
  const jk = this.jk.value;
  const goldar = this.goldar.value;
  const poli = this.poli.value;
  const dokter = this.dokter.value;
  const jenis_obat = this.jenis_obat.value;
  const keluhan = this.keluhan.value;
  const riwayat = this.riwayat.value;

  // Tentukan jam praktik
  let jam_praktek = "Jadwal belum tersedia";
  if (dokter === "dr. Bara,Sp.B.") {
    jam_praktek = "Senin - Rabu, 08:00 - 12:00";
  } else if (dokter === "dr. Estu,Sp.U") {
    jam_praktek = "Kamis - Sabtu, 13:00 - 17:00";
  }

  // Tampilkan hasil
  const hasilDiv = document.getElementById("hasil");
  hasilDiv.style.display = "block";
  hasilDiv.innerHTML = `
    <h2>🩺 Data Pendaftaran Anda ⚕️</h2>
    <strong>🧾 Nama:</strong> ${nama}<br>
    <strong>🧾 Umur:</strong> ${umur} tahun<br>
    <strong>☎ Nomor Telepon:</strong> ${telepon}<br>
    <strong>✙ Nomor BPJS:</strong> ${bpjs}<br>
    <strong>🗺️ Alamat:</strong> ${alamat}<br>
    <strong>♂♀ Jenis Kelamin:</strong> ${jk}<br>
    <strong>🩸 Golongan Darah:</strong> ${goldar}<br>
    <strong>🧾 Poli Tujuan:</strong> ${poli}<br>
    <strong>👩🏻‍⚕️ Dokter:</strong> ${dokter}<br>
    <strong>⏱️ Jam Praktik:</strong> ${jam_praktek}<br>
    <strong>💊 Jenis Obat:</strong> ${jenis_obat}<br>
    <strong>🧾 Keluhan:</strong> ${keluhan}<br>
    <strong>🧾 Riwayat Penyakit:</strong> ${riwayat}<br>
    <br><em>✅ Terima kasih sudah mendaftar. Silakan menuju loket pendaftaran untuk langkah berikutnya.</em>
  `;
});
</script>

</body>
</html>
