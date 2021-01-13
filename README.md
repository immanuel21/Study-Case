Nama: Immanuel Yofi Zakarias Manafe
NIM : 19.11.2737

#Study Cashier
Aplikasi kasir sesuai yang diberikan dosen untuk tugas UAS. Aplikasi ini mempunyai fungsi seperti melihat daftar makanan, pembelian makanan serta pemakaian voucher pada pembelian makanan
## Scope and Functionalities
- User dapat melihat daftar makanan yang ditawarkan
- User dapat memasukkan atau menghapus makanan pilihan ke dalam keranjang
- User dapat melihat subtotal makanan yang terdapat pada keranjang
- User dapat melihat daftar voucher yang ditawarkan
- User dapat menggunakan salah satu voucher
- User dapat melihat harga total termasuk potongannya
## How Does It Works
1. Apa saja teknik yang diterapkan dalam Aplikasi ini?<br>
Menggunakan teknik MVC, yaitu membagi tiap kelas untuk satu tugas saja. Sehingga terdapat dua folder : Model dan Controller dengan tugas-tugas yang berbeda.<br>
2. Apa perbedaan tugas file dalam folder Model dan Controller?<br>
Folder Model berisi `Item.cs` `Voucher.cs` `Payment.cs` `KeranjangBelanja.cs` yang berfungsi mengatur logika seperti perhitungan dan inisialisasi. Model Item dan Voucher berfungsi untuk menyimpan Item dan Voucher, model Payment berfungsi untuk logic pembayaran yaitu penghitungan dari harga subtotal dikurangi potongan diskon. Model KeranjangBelanja berfungsi untuk perhitungan diskon dan perhitungan subtotal dalam keranjang belanja sebelum di kalkulasi dengan potongan diskon. Folder Controller berisi `MainWindowController.cs` `PenawaranController.cs` `VoucherController.cs` yang berfungsi mengontrol alur program seperti pengiriman data antar class. PenawaranController dan VoucherController memiliki fungsi yang sama yaitu memunculkan list item dan voucher serta menambahkannya kedalam keranjang belanja. MainWindowController berfungsi untuk memunculkan list yang ada di dalam keranjang dan function penghapusan item maupun voucher yang telah dipilih.<br>
3. Bagaimana alur program?<br>
Item diinisialisasi pada `Penawaran.xaml.cs` kemudian dimasukkan atau ditambahkan kedalam keranjang belanja.
```csharp
private void generateContentPenawaran()
        {
            Item coffeLate = new Item("Coffe Late", 30000);
            Item blackTea = new Item("BlackTea", 20000);
            Item milkShake = new Item("Milk Shake", 15000);
            Item watermelonJuice = new Item("Watermelon Juice", 25000);
            Item lemonSquash = new Item("Lemon Squash", 30000);
            Item pizza = new Item("Pizza", 75000);
            Item friedRice = new Item("Fried Rice Special", 45000);

            Penawarancontroller.addItem(coffeLate);
            Penawarancontroller.addItem(blackTea);
            Penawarancontroller.addItem(milkShake);
            Penawarancontroller.addItem(watermelonJuice);
            Penawarancontroller.addItem(lemonSquash);
            Penawarancontroller.addItem(pizza);
            Penawarancontroller.addItem(friedRice);

            listPenawaran.Items.Refresh();
        }
```
Voucher diinisialisasi pada `Voucher.xaml.cs` kemudian dimasukkan kedalam keranjang belanja.
```csharp
private void generateListVoucher()
        {
            Model.Voucher awalTahun = new Model.Voucher(title: "Promo Awal Tahun Diskon 25%", discInPercent: 25);
            Model.Voucher tebusMurah = new Model.Voucher(title: "Promo Tebus Murah Diskon 30% atau max. 30.000", discInPercent: 30);
            Model.Voucher promoNatal = new Model.Voucher(title: "Promo Natal Potongan 10000", disc: 10000);

            voucherController.addItem(awalTahun);
            voucherController.addItem(tebusMurah);
            voucherController.addItem(promoNatal);

            DaftarVoucher.Items.Refresh();
        }
```
Pada `MainWindow.xaml.cs`, diinisialisasi instance dari class-class lain seperti class payment untuk menampilkan hasil perhitungan pada label, class KeranjangBelanja untuk menampilkan item dan voucher yang telah dikirim/dimasukkan kedalam keranjang belanja, dikontrol menggunakan instance dari class MainWindowController.
```csharp
public MainWindow()
        {
            InitializeComponent();

            payment = new Payment(this);

            KeranjangBelanja keranjangBelanja = new KeranjangBelanja(payment, this);

            controller = new MainWindowController(keranjangBelanja);

            listBoxPesanan.ItemsSource = controller.getSelectedItems();
            listBoxPakaiVoucher.ItemsSource = controller.getSelectedVouchers();

            initializeView();
        }

```
