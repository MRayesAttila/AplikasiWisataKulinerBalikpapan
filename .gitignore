import sys
from PyQt5.QtWidgets import QApplication, QWidget, QVBoxLayout, QPushButton, QListWidget, QLabel, QLineEdit, QMessageBox, QDialog, QComboBox, QTextEdit

class AplikasiKuliner(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Aplikasi Wisata Kuliner")
        self.setGeometry(100, 100, 400, 400)

        self.init_ui()

    def init_ui(self):
        # Meminta nama panggilan pengguna saat aplikasi dibuka
        self.nama_pengguna = self.get_nama_pengguna()

        # Membuat layout utama
        layout = QVBoxLayout()

        # Membuat label judul
        self.label_title = QLabel(f"Selamat Datang {self.nama_pengguna}, di Aplikasi Wisata Kuliner")
        layout.addWidget(self.label_title)

        # Membuat combo box untuk memilih daerah
        self.combo_daerah = QComboBox()
        self.combo_daerah.addItems(["Balikpapan Timur", "Balikpapan Barat", "Balikpapan Selatan", "Balikpapan Utara", "Balikpapan Tengah"])
        layout.addWidget(self.combo_daerah)

        # Membuat combo box untuk memilih daerah
        self.combo_jenis = QComboBox()
        self.combo_jenis.addItems(["Makanan Berat", "Makanan Ringan", "Minuman"])
        layout.addWidget(self.combo_jenis)

        # Membuat list widget untuk daftar tempat kuliner
        self.list_widget = QListWidget()
        layout.addWidget(self.list_widget)

        # Membuat tombol untuk menampilkan detail tempat kuliner terpilih
        tmbl_detail = QPushButton("Tampilkan Detail")
        tmbl_detail.clicked.connect(self.tampilkan_detail)
        layout.addWidget(tmbl_detail)

        # Menambahkan layout untuk menampilkan detail tempat kuliner
        self.layout_detail = QVBoxLayout()

        # Membuat label untuk menampilkan detail tempat kuliner terpilih
        self.label_detail = QLabel("")
        self.layout_detail.addWidget(self.label_detail)

        layout.addLayout(self.layout_detail)

        # Membuat tombol untuk menambah tempat kuliner baru
        tmbl_tambah = QPushButton("Tambah Tempat Kuliner Baru")
        tmbl_tambah.clicked.connect(self.tambah_kuliner)
        layout.addWidget(tmbl_tambah)

        # Menambahkan layout utama ke window
        self.setLayout(layout)

        # Mengatur tempat kuliner untuk setiap daerah dan jenis
        self.tempat_kuliner = {
            "Balikpapan Timur": {
                "Makanan Berat": [("Nasi Goreng", "Lokasi di dekat PJHI, depan Starbuck Mulawarman."),
                                  ("Mie Goreng Cak Shodik", "Rp 20.000 per porsi, samping gang SPBU Batakan, berjarak 200m dari jalan raya."),
                                  ("Nasi Padang", "Rp 25.000 per porsi, depan Thiess.")],
                "Makanan Ringan": [("Kue Lumpur", "Rp 3.000 per kue, lokasi di Pasar Manggar"),
                                   ("Batagor & Salome", "Samping jalan raya sekitar Stadion Batakan"),
                                   ("Aneka Gorengan", "Rp 3.000 per gorengan, lokasi dekat Indomaret Batakan.")],
                "Minuman": [("Es Doger", "Rp 4.000 per minuman, lokasi depan SDN 005."),
                            ("Es Jeruk", "Rp 6.000 per minuman, lokasi samping gang SPBU Batakan."),
                            ("Es Kelapa Muda", "Rp 5.000, lokasi jalan sekitar Pantai Manggar.")]
            },
            "Balikpapan Barat": {
                "Makanan Berat": [("Soto Ayam H.Ali", "Rp 20.000, lokasi di Kebun Sayur.")],
                "Makanan Ringan": [("Lisda Bakery", "Toko yang menyajikan beragam kue dengan beragamm rasa dan harga, daerah Marga Sari.")],
                "Minuman": [("Es Teler", "Rp 10.000, lokasi samping gereja katolik.")]
            },
            "Balikpapan Selatan": {
                "Makanan Berat": [("Seafood Dandito", "Restoran yang populer dengan sajian kepitingnya.")],
                "Makanan Ringan": [("Toko Kue", "Toko yang menyajikan beragam kue dengan beragamm rasa dan harga.")],
                "Minuman": [("Puan Kopi", "Kafe yang berlokasi di pinggir pantai, populer di kalangan remaja dewasa.")],
            },
            "Balikpapan Utara": {
                "Makanan Berat": [("Waroeng Rahmad", "Warung yang menyajikan berbagai hidangan yang bisa dipilih porsinya.")],
                "Makanan Ringan": [("Salome Pentol Granat", "Berlokasi di jalan menuju kamput ITK, depan Toko Giska.")],
                "Minuman": [("Teh IKN Nusantara", "Menyajikan minuman dengan berbagai rasa dan harga, populer di kalangan mahasiswa ITK.")]
            },
            "Balikpapan Tengah": {
                "Makanan Berat": [("Teluk Bayur Seafood", "Berlokasi di Jl. Ahmad Yani.")],
                "Makanan Ringan": [("Holland Bakery Gunun Sari", "Berlokasi di Jl. Ahmad Yani samping Bank CIMB Niaga.")],
                "Minuman": [("Kedai Kopi Hitam Manis", "Rp 25.000-50.000 per orang, sangat populer di kalangan anak muda pada malam hari.")]
            }
        }

        # Mengatur event untuk mengubah daftar tempat kuliner saat daerah dipilih
        self.combo_daerah.currentIndexChanged.connect(self.daerah_terpilih)
        self.combo_jenis.currentIndexChanged.connect(self.jenis_terpilih)

    def get_nama_pengguna(self):
        # Membuat dialog untuk meminta nama panggilan pengguna
        dialog = QDialog(self)
        dialog.setWindowTitle("Masukkan Nama Panggilan")
        dialog.setGeometry(200, 200, 300, 100)

        layout = QVBoxLayout()

        # Membuat label dan line edit untuk memasukkan nama panggilan
        label_nama = QLabel("Nama Panggilan:")
        layout.addWidget(label_nama)
        edit_nama = QLineEdit()
        layout.addWidget(edit_nama)

        # Membuat tombol OK
        tmbl_ok = QPushButton("OK")
        tmbl_ok.clicked.connect(dialog.accept)
        layout.addWidget(tmbl_ok)

        dialog.setLayout(layout)

        # Menampilkan dialog dan mengembalikan nama panggilan
        if dialog.exec_() == QDialog.Accepted:
            return edit_nama.text() or "Pengguna"
        else:
            return "Pengguna"

    def tampilkan_detail(self):
        # Mendapatkan item terpilih dari list
        item_terpilih = self.list_widget.currentItem()
        if item_terpilih:
            detail = item_terpilih.data(1000)  # 1000 adalah Role kustom untuk menyimpan detail
            if detail:
                self.label_detail.setText(detail)
            else:
                self.label_detail.setText("Detail belum ditambahkan.")
        else:
            QMessageBox.warning(self, "Peringatan", "Pilih salah satu tempat kuliner terlebih dahulu.")

    def tambah_kuliner(self):
        # Membuat dialog untuk menambah tempat kuliner baru
        dialog = QDialog()
        dialog.setWindowTitle("Tambah Tempat Kuliner Baru")
        dialog.setGeometry(200, 200, 300, 200)

        layout = QVBoxLayout()

        # Membuat label dan line edit untuk nama tempat kuliner baru
        label_nama = QLabel("Nama Tempat Kuliner:")
        layout.addWidget(label_nama)
        edit_nama = QLineEdit()
        layout.addWidget(edit_nama)

        # Membuat label dan text edit untuk detail tempat kuliner baru
        label_detail = QLabel("Detail Tempat Kuliner:")
        layout.addWidget(label_detail)
        edit_detail = QTextEdit()
        layout.addWidget(edit_detail)

        # Membuat tombol untuk menambah tempat kuliner
        tmbl_ok = QPushButton("Tambah")
        tmbl_ok.clicked.connect(lambda: self.tambah_kuliner_aksi(dialog, edit_nama.text(), edit_detail.toPlainText()))
        layout.addWidget(tmbl_ok)

        dialog.setLayout(layout)
        dialog.exec_()

    def tambah_kuliner_aksi(self, dialog, nama, detail):
        # Menambah tempat kuliner baru ke list
        if nama:
            if detail:
                daerah_terpilih = self.combo_daerah.currentText()
                jenis_terpilih = self.combo_jenis.currentText()
                self.list_widget.addItem(nama)
                self.tempat_kuliner[daerah_terpilih][jenis_terpilih].append((nama, detail))
                self.list_widget.item(self.list_widget.count() - 1).setData(1000, detail)  # Menyimpan detail dengan Role kustom
                dialog.close()
            else:
                QMessageBox.warning(dialog, "Peringatan", "Detail tempat kuliner tidak boleh kosong.")
        else:
            QMessageBox.warning(dialog, "Peringatan", "Nama tempat kuliner tidak boleh kosong.")

    def daerah_terpilih(self, index):
        # Membersihkan daftar tempat kuliner sebelumnya
        self.list_widget.clear()
        # Memperbarui daftar tempat kuliner berdasarkan daerah yang dipilih
        daerah_terpilih = self.combo_daerah.currentText()
        tempat_kuliner_daerah = self.tempat_kuliner[daerah_terpilih][self.combo_jenis.currentText()]
        for nama, detail in tempat_kuliner_daerah:
            self.list_widget.addItem(nama)  # Menambahkan nama tempat kuliner
            self.list_widget.item(self.list_widget.count() - 1).setData(1000, detail)  # Menyimpan detail dengan Role kustom
        self.label_detail.clear()

    def jenis_terpilih(self, index):
        # Membersihkan daftar tempat kuliner sebelumnya
        self.list_widget.clear()

        # Memperbarui daftar tempat kuliner berdasarkan jenis makanan yang dipilih
        jenis_terpilih = self.combo_jenis.currentText()
        tempat_kuliner_jenis = self.tempat_kuliner[self.combo_daerah.currentText()][jenis_terpilih]

        # Menambahkan tempat kuliner ke list widget
        for nama, detail in tempat_kuliner_jenis:
            self.list_widget.addItem(nama)  # Menambahkan nama tempat kuliner
            self.list_widget.item(self.list_widget.count() - 1).setData(1000, detail)  # Menyimpan detail dengan Role kustom
        self.label_detail.clear()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = AplikasiKuliner()
    window.show()
    sys.exit(app.exec_())

