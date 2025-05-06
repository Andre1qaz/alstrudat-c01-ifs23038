# Manajemen Data Barang dan Mobil KBT

Aplikasi berbasis Java untuk mengelola data barang dan mobil KBT (Kendaraan Bertenaga Listrik) menggunakan implementasi struktur data Linked List.

## Struktur Proyek

```
Proyek Java
├── App.java                # Program utama yang menjalankan aplikasi
├── Data.java               # Kelas dasar abstrak untuk menyimpan informasi umum
├── DataBarang.java         # Kelas turunan dari Data untuk data barang
├── DataMobilKBT.java       # Kelas turunan dari Data untuk data mobil KBT
├── BarangLoader.java       # Kelas untuk memuat dan mengelola data barang
├── MobilKBT.java           # Kelas untuk memuat dan mengelola data mobil KBT
├── LinkedList.java         # Implementasi struktur data Linked List
├── LinkedListHelper.java   # Kelas pembantu untuk operasi-operasi khusus pada Linked List
└── Util.java               # Berisi fungsi-fungsi utilitas umum untuk mendukung aplikasi
```

## Deskripsi Kelas

### App.java
Kelas utama yang menjalankan aplikasi dan menampilkan menu interaktif untuk pengguna.

### Data.java
Kelas abstrak dasar yang digunakan untuk mendefinisikan atribut dan metode umum untuk semua jenis data.

### DataBarang.java
Kelas yang mewakili data barang, turunan dari kelas Data. Memiliki atribut tambahan seperti jenis barang dan harga.

### DataMobilKBT.java
Kelas yang mewakili data mobil KBT, turunan dari kelas Data. Memiliki atribut khusus seperti daya listrik, kapasitas baterai, kapasitas penumpang, dan jangkauan.

### BarangLoader.java
Kelas yang mengelola daftar barang menggunakan LinkedList. Menyediakan fungsi untuk menampilkan dan menambah data barang.

### MobilKBT.java
Kelas yang mengelola daftar mobil KBT menggunakan LinkedList. Menyediakan berbagai fungsi seperti menambah, menampilkan, memperbarui, menghapus, mencari, dan mengurutkan data mobil.

### LinkedList.java
Implementasi struktur data Linked List yang digunakan untuk menyimpan dan mengelola koleksi objek.

### LinkedListHelper.java
Kelas pembantu yang menyediakan fungsi-fungsi tambahan untuk manipulasi LinkedList, seperti pengurutan.

### Util.java
Berisi fungsi-fungsi utilitas umum seperti pengelolaan input/output untuk mendukung aplikasi.

## Diagram Hubungan Antar Kelas

Berikut adalah diagram kelas untuk proyek ini yang menunjukkan hubungan antar kelas:

```mermaid
classDiagram
    %% Class definitions with inheritance
    class App {
        -MobilKBT mobilManager
        -BarangLoader barangLoader
        +main(String[] args) void
        -tampilkanMenu() void
        -bacaInputAngka(String prompt) int
    }
    
    class Util {
        +getScanner() Scanner
        +closeScanner() void
    }
    
    class Data {
        <<abstract>>
        #String id
        #String nama
        +Data(String id, String nama)
        +getId() String
        +setId(String id) void
        +getNama() String
        +setNama(String nama) void
        +tampilData() void*
    }
    
    class DataBarang {
        -String jenis
        -double harga
        +DataBarang(String id, String nama, String jenis, double harga)
        +getJenis() String
        +setJenis(String jenis) void
        +getHarga() double
        +setHarga(double harga) void
        +tampilData() void
    }
    
    class DataMobilKBT {
        -String jenis
        -double dayaListrik
        -int kapasitasBaterai
        -int kapasitasPenumpang
        -double jangkauan
        +DataMobilKBT(String id, String nama, String jenis, double dayaListrik, int kapasitasBaterai, int kapasitasPenumpang, double jangkauan)
        +getJenis() String
        +setJenis(String jenis) void
        +getDayaListrik() double
        +setDayaListrik(double dayaListrik) void
        +getKapasitasBaterai() int
        +setKapasitasBaterai(int kapasitasBaterai) void
        +getKapasitasPenumpang() int
        +setKapasitasPenumpang(int kapasitasPenumpang) void
        +getJangkauan() double
        +setJangkauan(double jangkauan) void
        +tampilData() void
    }
    
    class LinkedList~T~ {
        -Node~T~ head
        -int size
        +LinkedList()
        +add(T data) void
        +get(int index) T
        +remove(int index) void
        +size() int
        +isEmpty() boolean
        +getFirst() T
        +getLast() T
        +clear() void
    }
    
    class LinkedListHelper {
        +sortList~T~(LinkedList~T~ list, Comparator~T~ comparator) void
    }
    
    class BarangLoader {
        -LinkedList~DataBarang~ daftarBarang
        +BarangLoader()
        -initData() void
        +tampilkanBarang() void
        +tambahBarang() void
        +close() void
    }
    
    class MobilKBT {
        -LinkedList~DataMobilKBT~ daftarMobil
        +MobilKBT()
        +initializeData() void
        +tambahMobil() void
        +tampilkanSemuaMobil() void
        +tampilkanDetailMobil() void
        +updateMobil() void
        +hapusMobil() void
        +cariMobilByNama() void
        +cariMobilByKapasitasPenumpang() void
        +sortMobilByDaya() void
        +sortMobilByKapasitasBaterai() void
        -cariMobilById(String id) DataMobilKBT
    }
    
    %% Inheritance relationships
    Data <|-- DataBarang
    Data <|-- DataMobilKBT
    
    %% Usage relationships
    App --> MobilKBT : uses
    App --> BarangLoader : uses
    App --> Util : uses
    MobilKBT --> LinkedList : contains
    MobilKBT --> LinkedListHelper : uses
    MobilKBT --> Util : uses
    BarangLoader --> LinkedList : contains
    BarangLoader --> Util : uses
    LinkedListHelper --> LinkedList : manipulates
```

Keterangan hubungan antar kelas:
- **Inheritance (Pewarisan)**: `DataBarang` dan `DataMobilKBT` mewarisi `Data` sebagai kelas abstrak induk
- **Dependency (Ketergantungan)**: 
  - `App` menggunakan `MobilKBT`, `BarangLoader`, dan `Util`
  - `MobilKBT` dan `BarangLoader` menggunakan `LinkedList` dan `Util`
  - `LinkedListHelper` memanipulasi `LinkedList`
- **Composition (Komposisi)**:
  - `MobilKBT` memiliki koleksi objek `DataMobilKBT` dalam `LinkedList`
  - `BarangLoader` memiliki koleksi objek `DataBarang` dalam `LinkedList`

## Alur Program

1. Program dimulai dari metode `main()` di kelas `App`
2. Inisialisasi objek `MobilKBT` dan `BarangLoader`
3. Menampilkan menu utama kepada pengguna
4. Berdasarkan pilihan pengguna, program akan memanggil fungsi-fungsi yang sesuai:
   - Menampilkan, menambah, memperbarui, atau menghapus data mobil KBT
   - Mencari mobil berdasarkan nama atau kapasitas penumpang
   - Mengurutkan data mobil berdasarkan daya listrik atau kapasitas baterai
   - Menampilkan atau menambah data barang
5. Program terus berjalan hingga pengguna memilih untuk keluar

## Fitur

- Manajemen data mobil KBT (tambah, tampil, perbarui, hapus)
- Pencarian data mobil berdasarkan nama dan kapasitas penumpang
- Pengurutan data mobil berdasarkan daya listrik dan kapasitas baterai
- Manajemen data barang (tambah, tampil)
- Implementasi struktur data Linked List kustom

## Cara Menjalankan

1. Pastikan Java Development Kit (JDK) telah terinstal di sistem Anda
2. Kompilasi semua file Java:
   ```
   javac *.java
   ```
3. Jalankan aplikasi:
   ```
   java App
   ```

## Dikembangkan Oleh

Andre Christian Saragih

---

*Program ini dibuat sebagai proyek untuk mempelajari implementasi struktur data Linked List dalam aplikasi Java.*
