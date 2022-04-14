<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 Mengapa panduan ini dapat membawa keterampilan pengujian Anda ke tingkat berikutnya

<br/>

## 📗 50+ praktik terbaik: Sangat komprehensif dan lengkap

Ini adalah panduan untuk keandalan JavaScript & Node.js dari A-Z. Ini merangkum dan mengkurasi untuk Anda lusinan posting blog, buku, dan alat terbaik yang ditawarkan pasar

## 🚢 Lanjutan: Melampaui 10.000 mil di luar dasar-dasar

Ikuti perjalanan yang melampaui dasar-dasar ke topik lanjutan seperti pengujian dalam produksi, pengujian mutasi, pengujian berbasis properti, dan banyak alat strategis & profesional lainnya. Jika Anda membaca setiap kata dalam panduan ini, keterampilan pengujian Anda kemungkinan akan jauh di atas rata-rata

## 🌐 Full-stack: front, backend, CI, apa pun

Mulailah dengan memahami praktik pengujian di mana-mana yang merupakan dasar untuk setiap tingkat aplikasi. Kemudian, selidiki area pilihan Anda: frontend/UI, backend, CI atau mungkin semuanya?

<br/>

### Ditulis Oleh Yoni Goldberg

- Konsultan JavaScript & Node.js
- 📗 [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com) - Kursus online komprehensif saya dengan lebih dari 7 jam video [7 hours of video](https://www.testjavascript.com), 14 jenis pengujian, dan lebih dari 40 praktik terbaik
- [Ikuti saya di Twitter](https://twitter.com/goldbergyoni/)

<br/>

### Terjemahan - baca dalam bahasa Anda sendiri

- 🇨🇳[Chinese](readme-zh-CN.md) - Courtesy of [Yves yao](https://github.com/yvesyao)
- 🇰🇷[Korean](readme.kr.md) - Courtesy of [Rain Byun](https://github.com/ragubyun)
- 🇵🇱[Polish](readme-pl.md) - Courtesy of [Michal Biesiada](https://github.com/mbiesiad)
- 🇪🇸[Spanish](readme-es.md) - Courtesy of [Miguel G. Sanguino](https://github.com/sanguino)
- 🇧🇷[Portuguese-BR](readme-pt-br.md) - Courtesy of [Iago Angelim Costa Cavalcante](https://github.com/iagocavalcante) , [Douglas Mariano Valero](https://github.com/DouglasMV) and [koooge](https://github.com/koooge)
- 🇫🇷[French](readme-fr.md) - Courtesy of [Mathilde El Mouktafi](https://github.com/mel-mouk)
- 🇯🇵[Japanese (draft)](https://github.com/yuichkun/javascript-testing-best-practices/blob/master/readme-jp.md) - Courtesy of [Yuichi Yogo](https://github.com/yuichkun) and [ryo](https://github.com/kawamataryo)
- 🇹🇼[Traditional Chinese](readme-zh-TW.md) - Courtesy of [Yubin Hsu](https://github.com/yubinTW)
- 🇹🇼[Traditional Chinese](readme-zh-TW.md) - Courtesy of [Yubin Hsu](https://github.com/yubinTW)
- 🇮🇩[Indonesia](readme-id.md) - Courtesy of [R.M Reza](https://github.com/renomureza)
- Ingin menerjemahkan ke bahasa Anda sendiri? tolong buka issue 💜

<br/><br/>

## `Daftar Isi`

#### [`Bagian 0: Aturan Emas`](#bagian-0️⃣-aturan-emas)

Satu saran yang menginspirasi semua yang lain (1 butir khusus)

#### [`Bagian 1: Tes Anatomi`](#bagian-1-tes-anatomi-1)

Pondasi - menyusun tes bersih (12 butir)

#### [`Bagian 2: Backend`](#bagian-2️⃣-pengujian-backend)

Menulis pengujian backend dan Microservices secara efisien (13 butir)

#### [`Bagian 3: Frontend`](#bagian-3️⃣-pengujian-frontend)

Tes penulisan untuk UI web termasuk pengujian komponen dan E2E (11 butir)

#### [`Bagian 4: Mengukur Efektivitas Tes`](#bagian-4️⃣-mengukur-efektivitas-tes)

Menonton penjaga - mengukur kualitas tes (4 butir)

#### [`Bagian 5: Continuous Integration`](#bagian-5️⃣-ci-dan-ukuran-kualitas-lainnya)

Pedoman untuk CI di dunia JS (9 butir)

<br/><br/>

# Bagian 0️⃣: Aturan Emas

<br/>

## ⚪️ 0 Aturan Emas: Desain untuk pengujian ramping

:white_check_mark: **Lakukan:**
Menguji kode bukan kode produksi - Rancang agar pendek, sederhana, datar, dan menyenangkan untuk digunakan. Seseorang harus melihat tes dan mendapatkan niat secara instan.

Lihat, pikiran kita sudah sibuk dengan pekerjaan utama kita - kode produksi. Tidak ada 'headspace' untuk kompleksitas tambahan. Jika kita mencoba memasukkan sistem sus lain ke otak kita yang buruk, itu akan memperlambat tim yang bekerja melawan alasan kita melakukan pengujian. Praktis di sinilah banyak tim mengabaikan pengujian.

Tes adalah kesempatan untuk sesuatu yang lain - asisten ramah, co-pilot, yang memberikan nilai yang besar untuk investasi kecil. Sains memberi tahu kita bahwa kita memiliki dua sistem otak: sistem 1 digunakan untuk aktivitas yang mudah seperti mengemudikan mobil di jalan yang kosong dan sistem 2 yang dimaksudkan untuk operasi yang kompleks dan sadar seperti memecahkan persamaan matematika. Rancang pengujian Anda untuk sistem 1, ketika melihat kode pengujian seharusnya terasa semudah memodifikasi dokumen HTML dan tidak seperti memecahkan 2X(17 × 24).

Ini dapat dicapai dengan teknik, alat, dan target pengujian selektif yang hemat biaya dan memberikan ROI yang bagus. Uji hanya sebanyak yang diperlukan, berusahalah untuk membuatnya tetap gesit, kadang-kadang bahkan layak untuk menjatuhkan beberapa tes dan memperdagangkan keandalan untuk kelincahan dan kesederhanaan.

![alt text](/assets/headspace.png "We have no head room for additional complexity")

Sebagian besar saran di bawah ini adalah turunan dari prinsip ini.

### Siap untuk mulai?

<br/><br/>

# Bagian 1: Tes Anatomi

<br/>

## ⚪ ️ 1.1 Sertakan 3 bagian di setiap nama tes

:white_check_mark: **Lakukan:** Laporan pengujian harus memberi tahu apakah revisi aplikasi saat ini memenuhi persyaratan untuk orang-orang yang belum tentu akrab dengan kode: penguji, insinyur DevOps yang menerapkan dan masa depan Anda dua tahun dari sekarang. Ini dapat dicapai paling baik jika tes berbicara pada tingkat persyaratan dan mencakup 3 bagian:

(1) Apa yang sedang diuji? Misalnya, metode ProductsService.addNewProduct

(2) Dalam situasi dan skenario apa? Misalnya, tidak ada harga yang diteruskan ke metode

(3) Apa hasil yang diharapkan? Misalnya, produk baru tidak disetujui

<br/>

❌ **Jika tidak:** Penerapan baru saja gagal, pengujian bernama "Tambahkan produk" gagal. Apakah ini memberi tahu Anda apa sebenarnya yang tidak berfungsi?

<br/>

**👇 Catatan:** Setiap butir memiliki contoh kode dan terkadang juga ilustrasi gambar. Klik untuk memperluas

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>
  
<br/>
  
### :clap: Melakukannya dengan Benar Contoh: Nama tes yang terdiri dari 3 bagian

![](https://img.shields.io/badge/🔨%20Example%20using%20Mocha-blue.svg "Using Mocha to illustrate the idea")

```javascript
//1. unit under test
describe('Products Service', function() {
  describe('Add new product', function() {
    //2. scenario and 3. expectation
    it('When no price is specified, then the product status is pending approval', ()=> {
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});

```

<br/>

### :clap: Melakukannya dengan Benar Contoh: Nama tes yang terdiri dari 3 bagian

![alt text](/assets/bp-1-3-parts.jpeg "A test name that constitutes 3 parts")

</details>

<br/>
<details><summary>© <b>Kredit & baca lebih lanjut</b></summary>
  1. <a href='https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html'>Roy Osherove - Naming standards for unit tests</a>
</details>

<br/><br/>

## ⚪ ️ 1.2 Tes struktur dengan pola AAA

:white_check_mark: **Lakukan:** Susun pengujian Anda dengan 3 bagian yang terpisah dengan baik Atur (Arrange), Bertindak (Act) & Tegaskan(Assert) (AAA). Mengikuti struktur ini menjamin bahwa pembaca tidak menghabiskan CPU-otak untuk memahami rencana pengujian:

1 A - Arrange: Semua kode pengaturan untuk membawa sistem ke skenario yang ingin disimulasikan oleh pengujian. Ini mungkin termasuk membuat instance unit yang sedang diuji konstruktor, menambahkan catatan DB, mocking/stubbing objek dan kode persiapan lainnya

2 A - Act: Jalankan unit yang sedang diuji. Biasanya 1 baris kode

3 A - Assert: Pastikan bahwa nilai yang diterima memenuhi harapan. Biasanya 1 baris kode

<br/>

❌ **Jika tidak:** Anda tidak hanya menghabiskan berjam-jam untuk memahami kode utama, tetapi apa yang seharusnya menjadi bagian paling sederhana dari hari (pengujian) meregangkan otak Anda

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Tes terstruktur dengan pola AAA

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest") ![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
describe("Customer classifier", () => {
  test("When customer spent more than 500$, should be classified as premium", () => {
    //Arrange
    const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
    const DBStub = sinon
      .stub(dataAccess, "getCustomer")
      .reply({ id: 1, classification: "regular" });

    //Act
    const receivedClassification =
      customerClassifier.classifyCustomer(customerToClassify);

    //Assert
    expect(receivedClassification).toMatch("premium");
  });
});
```

<br/>

### :thumbsdown: Contoh Anti-Pola: Tidak ada pemisahan, satu massal, lebih sulit untuk ditafsirkan

```javascript
test("Should be classified as premium", () => {
  const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
  const DBStub = sinon
    .stub(dataAccess, "getCustomer")
    .reply({ id: 1, classification: "regular" });
  const receivedClassification =
    customerClassifier.classifyCustomer(customerToClassify);
  expect(receivedClassification).toMatch("premium");
});
```

</details>

<br/><br/>

## ⚪ ️1.3 Jelaskan harapan dalam bahasa produk: gunakan pernyataan gaya BDD

:white_check_mark: **Lakukan:** Mengodekan tes Anda dalam gaya deklaratif memungkinkan pembaca untuk langsung memahaminya tanpa menghabiskan satu siklus CPU-otak. Saat Anda menulis kode imperatif yang dikemas dengan logika kondisional, pembaca dipaksa untuk menggunakan lebih banyak siklus CPU-otak. Dalam hal ini, kodekan ekspektasi dalam bahasa seperti manusia, gaya BDD deklaratif menggunakan `expect` atau `should` dan tidak menggunakan kode khusus. Jika Chai & Jest tidak menyertakan pernyataan yang diinginkan dan sangat berulang, pertimbangkan untuk [memperluas Jest matcher (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) atau [menulis plugin Chai khusus](https://www.chaijs.com/guide/plugins/)

<br/>

❌ **Jika tidak:** Tim akan menulis lebih sedikit tes dan menghias yang mengganggu dengan .skip()

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha & Chai") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

### :thumbsdown: Contoh Anti-Pola: Pembaca harus membaca kode yang tidak terlalu pendek, dan imperatif hanya untuk mendapatkan cerita pengujian

```javascript
test("When asking for an admin, ensure only ordered admins in results", () => {
  //assuming we've added here two admins "admin1", "admin2" and "user1"
  const allAdmins = getUsers({ adminOnly: true });

  let admin1Found,
    adming2Found = false;

  allAdmins.forEach((aSingleUser) => {
    if (aSingleUser === "user1") {
      assert.notEqual(aSingleUser, "user1", "A user was found and not admin");
    }
    if (aSingleUser === "admin1") {
      admin1Found = true;
    }
    if (aSingleUser === "admin2") {
      admin2Found = true;
    }
  });

  if (!admin1Found || !admin2Found) {
    throw new Error("Not all admins were returned");
  }
});
```

<br/>

### :clap: Melakukannya dengan Benar Contoh: Membaca sekilas tes deklaratif berikut sangat mudah

```javascript
it("When asking for an admin, ensure only ordered admins in results", () => {
  //assuming we've added here two admins
  const allAdmins = getUsers({ adminOnly: true });

  expect(allAdmins)
    .to.include.ordered.members(["admin1", "admin2"])
    .but.not.include.ordered.members(["user1"]);
});
```

</details>

<br/><br/>

## ⚪ ️ 1.4 Tetap berpegang pada pengujian kotak hitam: Hanya uji metode publik

:white_check_mark: **Lakukan:** Menguji internal membawa overhead besar hampir tanpa biaya. Jika kode/API Anda memberikan hasil yang tepat, haruskah Anda benar-benar menginvestasikan 3 jam berikutnya untuk menguji BAGAIMANA cara kerjanya secara internal dan kemudian mempertahankan pengujian rapuh ini? Setiap kali perilaku publik diperiksa, implementasi privat juga diuji secara implisit dan pengujian Anda akan rusak hanya jika ada masalah tertentu (mis. output yang salah). Pendekatan ini juga disebut sebagai `behavioral testing`. Di sisi lain, jika Anda menguji internal (pendekatan kotak putih) — fokus Anda beralih dari perencanaan hasil komponen ke detail seluk beluk dan pengujian Anda mungkin rusak karena refactor kode kecil meskipun hasilnya baik-baik saja - ini secara dramatis meningkatkan pemeliharaan beban
<br/>

❌ **Jika tidak:** Tes Anda berperilaku seperti [anak laki-laki yang menangis serigala](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf): meneriakkan tangisan positif palsu (misalnya, Tes gagal karena nama variabel pribadi diubah). Tidak mengherankan, orang akan segera mulai mengabaikan pemberitahuan CI sampai suatu hari nanti, bug yang sebenarnya akan diabaikan…

<br/>
<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Kasus uji sedang menguji internal tanpa alasan yang bagus

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha & Chai")

```javascript
class ProductService {
  //this method is only used internally
  //Change this name will make the tests fail
  calculateVATAdd(priceWithoutVAT) {
    return { finalPrice: priceWithoutVAT * 1.2 };
    //Change the result format or key name above will make the tests fail
  }
  //public method
  getPrice(productId) {
    const desiredProduct = DB.getProduct(productId);
    finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
    return finalPrice;
  }
}

it("White-box test: When the internal methods get 0 vat, it return 0 response", async () => {
  //There's no requirement to allow users to calculate the VAT, only show the final price. Nevertheless we falsely insist here to test the class internals
  expect(new ProductService().calculateVATAdd(0).finalPrice).to.equal(0);
});
```

</details>

<br/><br/>

## ⚪ ️ ️1.5 Pilih tes ganda yang tepat: Hindari mock demi rintisan dan mata-mata

:white_check_mark: **Lakukan:** Uji ganda adalah kejahatan yang diperlukan karena mereka digabungkan ke internal aplikasi, namun beberapa memberikan nilai yang sangat besar (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Baca di sini pengingat tentang tes ganda: mengejek vs bertopik vs mata-mata](https://martinfowler.com/articles/mocksArentStubs.html)</a>).

Sebelum menggunakan uji ganda, ajukan pertanyaan yang sangat sederhana: Apakah saya menggunakannya untuk menguji fungsionalitas yang muncul, atau mungkin muncul, dalam dokumen persyaratan? Jika tidak, itu adalah bau pengujian kotak putih.

Misalnya, jika Anda ingin menguji apakah aplikasi Anda berperilaku wajar saat layanan pembayaran tidak aktif, Anda mungkin mematikan layanan pembayaran dan memicu beberapa pengembalian 'Tidak Ada Respons' untuk memastikan bahwa unit yang sedang diuji mengembalikan nilai yang benar. Ini memeriksa perilaku/respons/hasil aplikasi kami di bawah skenario tertentu. Anda mungkin juga menggunakan mata-mata untuk menegaskan bahwa email telah dikirim saat layanan itu tidak aktif — ini lagi-lagi merupakan pemeriksaan perilaku yang kemungkinan akan muncul di dokumen persyaratan (“Kirim email jika pembayaran tidak dapat disimpan”). Di sisi lain, jika Anda mock layanan Pembayaran dan memastikan bahwa itu dipanggil dengan jenis JavaScript yang tepat — maka pengujian Anda difokuskan pada hal-hal internal yang tidak ada hubungannya dengan fungsionalitas aplikasi dan cenderung sering berubah
<br/>

❌ **Jika tidak:** Setiap refactoring kode mengamanatkan untuk mencari semua tiruan dalam kode dan memperbarui yang sesuai. Testing menjadi beban bukan teman yang membantu

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh anti-pola: Mengolok-olok fokus pada internal

![](https://img.shields.io/badge/🔧%20Example%20using%20Sinon-blue.svg "Examples with Sinon")

```javascript
it("When a valid product is about to be deleted, ensure data access DAL was called once, with the right product and right config", async () => {
  //Assume we already added a product
  const dataAccessMock = sinon.mock(DAL);
  //hmmm BAD: testing the internals is actually our main goal here, not just a side-effect
  dataAccessMock
    .expects("deleteProduct")
    .once()
    .withArgs(DBConfig, theProductWeJustAdded, true, false);
  new ProductService().deletePrice(theProductWeJustAdded);
  dataAccessMock.verify();
});
```

<br/>

### :clap: Melakukannya dengan Benar Contoh: mata-mata terfokus pada pengujian persyaratan tetapi sebagai efek samping yang tak terhindarkan menyentuh internal

```javascript
it("When a valid product is about to be deleted, ensure an email is sent", async () => {
  //Assume we already added here a product
  const spy = sinon.spy(Emailer.prototype, "sendEmail");
  new ProductService().deletePrice(theProductWeJustAdded);
  //hmmm OK: we deal with internals? Yes, but as a side effect of testing the requirements (sending an email)
  expect(spy.calledOnce).to.be.true;
});
```

</details>

<br/><br/>

## ⚪ ️️1.6 Jangan "foo", gunakan input data yang realistis

:white_check_mark: **Lakukan:** Seringkali bug produksi terungkap di bawah beberapa input yang sangat spesifik dan mengejutkan — semakin realistis input pengujian, semakin besar peluang untuk menangkap bug lebih awal. Gunakan perpustakaan khusus seperti [Chance](https://github.com/chancejs/chancejs) atau [Faker](https://www.npmjs.com/package/faker) untuk menghasilkan data pseudo-nyata yang menyerupai variasi dan bentuk data produksi. Misalnya, perpustakaan tersebut dapat menghasilkan nomor telepon realistis, nama pengguna, kartu kredit, nama perusahaan, dan bahkan teks 'lorem ipsum'. Anda juga dapat membuat beberapa pengujian (di atas pengujian unit, bukan sebagai pengganti) yang mengacak data pemalsu untuk meregangkan unit Anda yang sedang diuji atau bahkan mengimpor data nyata dari lingkungan produksi Anda. Ingin membawanya ke level selanjutnya? Lihat butir berikutnya (pengujian berbasis properti).
<br/>

❌ **Jika tidak:** Semua pengujian pengembangan Anda akan salah menunjukkan hijau saat Anda menggunakan input sintetis seperti "Foo", tetapi kemudian produksi mungkin berubah menjadi merah saat peretas memasukkan string jahat seperti "@3e2ddsf . ##' 1 fdsfds . fds432 AAA”

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Rangkaian pengujian yang lolos karena data yang tidak realistis

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
const addProduct = (name, price) => {
  const productNameRegexNoSpace = /^\S*$/; //no white-space allowed

  if (!productNameRegexNoSpace.test(name)) return false; //this path never reached due to dull input

  //some logic here
  return true;
};

test("Wrong: When adding new product with valid properties, get successful confirmation", async () => {
  //The string "Foo" which is used in all tests never triggers a false result
  const addProductResult = addProduct("Foo", 5);
  expect(addProductResult).toBe(true);
  //Positive-false: the operation succeeded because we never tried with long
  //product name including spaces
});
```

<br/>

### :clap: Melakukannya dengan Benar Contoh: Mengacak input realistis

```javascript
it("Better: When adding new valid product, get successful confirmation", async () => {
  const addProductResult = addProduct(
    faker.commerce.productName(),
    faker.random.number()
  );
  //Generated random input: {'Sleek Cotton Computer',  85481}
  expect(addProductResult).to.be.true;
  //Test failed, the random input triggered some path we never planned for.
  //We discovered a bug early!
});
```

</details>

<br/><br/>

## ⚪ ️ 1.7 Uji banyak kombinasi input menggunakan pengujian berbasis Properti

:white_check_mark: **Lakukan:** Biasanya kami memilih beberapa sampel input untuk setiap pengujian. Bahkan ketika format input menyerupai data dunia nyata (lihat butir [‘Jangan foo’](#-%EF%B8%8F16-jangan-foo-gunakan-input-yang-realistis)), kami hanya mencakup beberapa kombinasi input (method('', true, 1), method(“string” , false , 0)) , Namun, dalam produksi, API yang dipanggil dengan 5 parameter dapat dipanggil dengan ribuan permutasi yang berbeda, salah satunya mungkin membuat proses kita terhenti ([lihat Fuzz Testing](https://en.wikipedia.org/wiki/Fuzzing)). Bagaimana jika Anda dapat menulis satu tes yang mengirimkan 1000 permutasi dari input yang berbeda secara otomatis dan menangkap input yang mana kode kami gagal mengembalikan respons yang benar? Pengujian berbasis properti adalah teknik yang melakukan hal itu: dengan mengirimkan semua kombinasi input yang mungkin ke unit Anda yang sedang diuji, itu meningkatkan kemungkinan menemukan bug. Misalnya, diberikan metode — addNewProduct(id, name, isDiscount) — pustaka pendukung akan memanggil metode ini dengan banyak kombinasi (angka, string, boolean) seperti (1, “iPhone”, false), (2, “Galaxy ", TRUE). Anda dapat menjalankan pengujian berbasis properti menggunakan test runner favorit Anda (Mocha, Jest, dll) menggunakan library seperti [js-verify](https://github.com/jsverify/jsverify) atau [testcheck](https://github.com/leebyron/testcheck-js) (dokumentasi yang jauh lebih baik). Pembaruan: Nicolas Dubien menyarankan di komentar di bawah untuk [checkout fast-check](https://github.com/dubzzz/fast-check#readme) yang tampaknya menawarkan beberapa fitur tambahan dan juga dipelihara secara aktif
<br/>

❌ **Jika tidak:** Secara tidak sadar, Anda memilih input pengujian yang hanya mencakup jalur kode yang berfungsi dengan baik. Sayangnya, ini menurunkan efisiensi pengujian sebagai sarana untuk mengungkap bug

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Menguji banyak permutasi input dengan "fast-check"

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
import fc from "fast-check";

describe("Product service", () => {
  describe("Adding new", () => {
    //this will run 100 times with different random properties
    it("Add new product with random yet valid properties, always successful", () =>
      fc.assert(
        fc.property(fc.integer(), fc.string(), (id, name) => {
          expect(addNewProduct(id, name).status).toEqual("approved");
        })
      ));
  });
});
```

</details>

<br/><br/>

## ⚪ ️ 1.8 Jika perlu, gunakan hanya snapshots short & inline

:white_check_mark: **Lakukan:** Bila ada kebutuhan untuk [snapshot testing](https://jestjs.io/docs/en/snapshot-testing), gunakan hanya snapshot pendek dan terfokus (yaitu 3-7 baris) yang disertakan sebagai bagian dari pengujian ([Inline Snapshot](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)) dan bukan di dalam file eksternal. Menjaga pedoman ini akan memastikan tes Anda tetap cukup jelas dan tidak rapuh.

Di sisi lain, tutorial dan alat 'snapshot klasik' mendorong untuk menyimpan file besar (misalnya markup rendering komponen, hasil API JSON) melalui beberapa media eksternal dan memastikan setiap kali pengujian berjalan untuk membandingkan hasil yang diterima dengan versi yang disimpan. Ini, misalnya, secara implisit dapat menggabungkan pengujian kami ke 1000 baris dengan 3000 nilai data yang tidak pernah dibaca dan dipikirkan oleh penulis pengujian. Mengapa ini salah? Dengan melakukan itu, ada 1000 alasan mengapa pengujian Anda gagal - cukup untuk mengubah satu baris agar snapshot menjadi tidak valid dan ini mungkin sering terjadi. Seberapa sering? untuk setiap spasi, komentar, atau perubahan kecil CSS/HTML. Tidak hanya itu, nama tes tidak akan memberikan petunjuk tentang kegagalan karena hanya memeriksa bahwa 1000 baris tidak berubah, juga mendorong penulis uji untuk menerima sebagai dokumen panjang yang diinginkan yang tidak dapat dia periksa dan verifikasi. Semua ini adalah gejala ujian yang tidak jelas dan bersemangat yang tidak fokus dan bertujuan untuk mencapai terlalu banyak

Perlu dicatat bahwa ada beberapa kasus di mana snapshot panjang & eksternal dapat diterima - saat menegaskan skema dan bukan data (mengekstraksi nilai dan fokus pada bidang) atau ketika dokumen yang diterima jarang berubah
<br/>

❌ **Jika tidak:** Tes UI gagal. Kode tampaknya benar, layar menampilkan piksel sempurna, apa yang terjadi? pengujian snapshot Anda baru saja menemukan perbedaan dari dokumen Asal ke dokumen yang diterima saat ini - satu karakter spasi ditambahkan ke markdown...

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Menggabungkan pengujian kami ke 2000 baris kode yang tidak terlihat

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
it("TestJavaScript.com is renderd correctly", () => {
  //Arrange

  //Act
  const receivedPage = renderer
    .create(
      <DisplayPage page="http://www.testjavascript.com">
        {" "}
        Test JavaScript{" "}
      </DisplayPage>
    )
    .toJSON();

  //Assert
  expect(receivedPage).toMatchSnapshot();
  //We now implicitly maintain a 2000 lines long document
  //every additional line break or comment - will break this test
});
```

<br/>

### :clap: Melakukannya dengan Benar Contoh: Harapan terlihat dan terfokus

```javascript
it("When visiting TestJavaScript.com home page, a menu is displayed", () => {
  //Arrange

  //Act
  const receivedPage = renderer
    .create(
      <DisplayPage page="http://www.testjavascript.com">
        {" "}
        Test JavaScript{" "}
      </DisplayPage>
    )
    .toJSON();

  //Assert

  const menu = receivedPage.content.menu;
  expect(menu).toMatchInlineSnapshot(`
<ul>
<li>Home</li>
<li> About </li>
<li> Contact </li>
</ul>
`);
});
```

</details>

<br/><br/>

## ⚪ ️Salin kode, tetapi hanya yang diperlukan

:white_check_mark: **Lakukan:** Sertakan semua detail yang diperlukan yang memengaruhi hasil tes, tetapi tidak lebih. Sebagai contoh, pertimbangkan tes yang harus memfaktorkan 100 baris input JSON - Menempel ini di setiap tes itu membosankan. Mengekstraknya di luar ke transferFactory.getJSON() akan membuat pengujian menjadi kabur - Tanpa data, sulit untuk mengkorelasikan hasil pengujian dengan penyebabnya ("mengapa harus mengembalikan status 400?"). Buku klasik pola x-unit menamai pola ini 'tamu misterius' - Sesuatu yang tidak terlihat memengaruhi hasil pengujian kami, kami tidak tahu persisnya. Kita dapat melakukan lebih baik dengan mengekstrak bagian panjang yang berulang di luar DAN menyebutkan secara eksplisit detail spesifik mana yang penting untuk pengujian. Mengikuti contoh di atas, pengujian dapat melewati parameter yang menyoroti apa yang penting: transferFactory.getJSON({sender: undefined}). Dalam contoh ini,
<br/>

❌ **Jika tidak:** Menyalin 500 baris JSON akan membuat pengujian Anda tidak dapat dipertahankan dan tidak dapat dibaca. Memindahkan segala sesuatu di luar akan berakhir dengan tes samar yang sulit dipahami

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Kegagalan pengujian tidak jelas karena semua penyebabnya adalah eksternal dan bersembunyi di dalam JSON yang besar

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
test("When no credit, then the transfer is declined", async () => {
  // Arrange
  const transferRequest = testHelpers.factorMoneyTransfer(); //get back 200 lines of JSON;
  const transferServiceUnderTest = new TransferService();

  // Act
  const transferResponse = await transferServiceUnderTest.transfer(
    transferRequest
  );

  // Assert
  expect(transferResponse.status).toBe(409); // But why do we expect failure: All seems perfectly valid in the test 🤔
});
```

<br/>

### :clap: Melakukannya dengan Benar Contoh: Tes menyoroti apa penyebab hasil tes

```javascript
test("When no credit, then the transfer is declined ", async () => {
  // Arrange
  const transferRequest = testHelpers.factorMoneyTransfer({
    userCredit: 100,
    transferAmount: 200,
  }); //obviously there is lack of credit
  const transferServiceUnderTest = new TransferService({
    disallowOvercharge: true,
  });

  // Act
  const transferResponse = await transferServiceUnderTest.transfer(
    transferRequest
  );

  // Assert
  expect(transferResponse.status).toBe(409); // Obviously if the user has no credit it should fail
});
```

</details>

<br/><br/>

## ⚪ ️ 1.10 Jangan menangkap kesalahan, harapkan itu

:white_check_mark: **Lakukan:** Saat mencoba menegaskan bahwa beberapa input memicu kesalahan, mungkin terlihat benar untuk menggunakan try-catch-finally dan menegaskan bahwa klausa catch telah dimasukkan. Hasilnya adalah kasus uji yang canggung dan bertele-tele (contoh di bawah) yang menyembunyikan maksud pengujian sederhana dan harapan hasil

Alternatif yang lebih elegan adalah menggunakan pernyataan Chai khusus satu baris: expect(method).to.throw (atau di Jest: expect(method).toThrow()). Sangatlah wajib untuk juga memastikan pengecualian berisi properti yang memberi tahu jenis kesalahan, jika tidak, hanya karena kesalahan umum, aplikasi tidak akan dapat berbuat banyak daripada menunjukkan pesan yang mengecewakan kepada pengguna

<br/>

❌ **Jika tidak:** Akan sulit untuk menyimpulkan dari laporan pengujian (misalnya laporan CI) apa yang salah

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-pola: Kasus uji panjang yang mencoba menegaskan keberadaan kesalahan dengan try-catch

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
it("When no product name, it throws error 400", async () => {
  let errorWeExceptFor = null;
  try {
    const result = await addNewProduct({});
  } catch (error) {
    expect(error.code).to.equal("InvalidInput");
    errorWeExceptFor = error;
  }
  expect(errorWeExceptFor).not.to.be.null;
  //if this assertion fails, the tests results/reports will only show
  //that some value is null, there won't be a word about a missing Exception
});
```

<br/>

### :clap: Melakukannya dengan Benar Contoh: Harapan yang dapat dibaca manusia yang dapat dipahami dengan mudah, bahkan mungkin oleh QA atau PM teknis

```javascript
it("When no product name, it throws error 400", async () => {
  await expect(addNewProduct({}))
    .to.eventually.throw(AppError)
    .with.property("code", "InvalidInput");
});
```

</details>

<br/><br/>

## ⚪ ️ 1.11 Tandai tes Anda

:white_check_mark: **Lakukan:** Tes yang berbeda harus dijalankan pada skenario yang berbeda: quick smoke, IO-less, tes harus dijalankan saat pengembang menyimpan atau mengkomit file, tes end-to-end penuh biasanya dijalankan saat pull request baru diajukan, dll. dicapai dengan menandai tes dengan kata kunci seperti #cold #api #sanity sehingga Anda dapat memahami harness pengujian Anda dan memanggil subset yang diinginkan. Misalnya, ini adalah bagaimana Anda hanya memanggil grup uji kewarasan dengan Mocha: mocha — grep 'sanity'
<br/>

❌ **Jika tidak:** Menjalankan semua pengujian, termasuk pengujian yang melakukan lusinan kueri DB, setiap kali pengembang membuat perubahan kecil dapat menjadi sangat lambat dan menjauhkan pengembang dari menjalankan pengujian

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Memberi tag pada pengujian sebagai '#cold-test' memungkinkan pelari pengujian hanya menjalankan pengujian cepat (Cold===tes cepat yang tidak melakukan IO dan dapat sering dijalankan bahkan saat pengembang sedang mengetik)

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
//this test is fast (no DB) and we're tagging it correspondigly
//now the user/CI can run it frequently
describe("Order service", function () {
  describe("Add new order #cold-test #sanity", function () {
    test("Scenario - no currency was supplied. Expectation - Use the default currency #sanity", function () {
      //code logic here
    });
  });
});
```

</details>

<br/><br/>

## ⚪ ️ 1.12 Mengkategorikan tes di bawah setidaknya 2 level

:white_check_mark: **Lakukan:** Terapkan beberapa struktur ke rangkaian pengujian Anda sehingga pengunjung sesekali dapat dengan mudah memahami persyaratan (tes adalah dokumentasi terbaik) dan berbagai skenario yang sedang diuji. Metode umum untuk ini adalah dengan menempatkan setidaknya 2 blok 'describe' di atas pengujian Anda: yang pertama adalah untuk nama unit yang sedang diuji dan yang kedua untuk tingkat kategorisasi tambahan seperti skenario atau kategori khusus (lihat contoh kode dan cetak layar di bawah). Melakukannya juga akan sangat meningkatkan laporan pengujian: Pembaca akan dengan mudah menyimpulkan kategori pengujian, mempelajari bagian yang diinginkan dan menghubungkan pengujian yang gagal. Selain itu, akan lebih mudah bagi pengembang untuk menavigasi kode suite dengan banyak tes. Ada beberapa struktur alternatif untuk test suite yang mungkin Anda pertimbangkan seperti [given-when-then](https://github.com/searls/jasmine-given) dan [RITE](https://github.com/ericelliott/riteway)

<br/>

❌ **Jika tidak:** Saat melihat laporan dengan daftar tes yang datar dan panjang, pembaca harus membaca sekilas teks yang panjang untuk menyimpulkan skenario utama dan menghubungkan kesamaan tes yang gagal. Pertimbangkan kasus berikut: Ketika tes 7/100 gagal, melihat daftar datar akan menuntut membaca teks tes yang gagal untuk melihat bagaimana mereka berhubungan satu sama lain. Namun, dalam laporan hierarkis semuanya bisa berada di bawah aliran atau kategori yang sama dan pembaca akan dengan cepat menyimpulkan apa atau setidaknya di mana akar penyebab kegagalan.

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Penataan suite dengan nama unit yang sedang diuji dan skenario akan mengarah ke laporan praktis yang ditunjukkan di bawah ini

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
// Unit under test
describe("Transfer service", () => {
  //Scenario
  describe("When no credit", () => {
    //Expectation
    test("Then the response status should decline", () => {});

    //Expectation
    test("Then it should send email to admin", () => {});
  });
});
```

![alt text](assets/hierarchical-report.png)

<br/>

### :thumbsdown: Contoh Anti-pola: Daftar tes yang datar akan mempersulit pembaca untuk mengidentifikasi cerita pengguna dan menghubungkan tes yang gagal

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Mocha")

```javascript
test("Then the response status should decline", () => {});

test("Then it should send email", () => {});

test("Then there should not be a new transfer record", () => {});
```

![alt text](assets/flat-report.png)

<br/>

</details>

<br/><br/>

## ⚪ ️1.13 Kebersihan pengujian umum yang baik lainnya

:white_check_mark: **Lakukan:** Posting ini difokuskan pada saran pengujian yang terkait dengan, atau setidaknya dapat dicontohkan dengan Node JS. Butir ini, bagaimanapun, mengelompokkan beberapa tip terkait non-Node yang terkenal

Pelajari dan latih prinsip [TDD principles](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) — prinsip itu sangat berharga bagi banyak orang tetapi jangan terintimidasi jika tidak sesuai dengan gaya Anda, Anda bukan satu-satunya. Pertimbangkan untuk menulis tes sebelum kode dalam gaya [red-green-refactor style](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html), pastikan setiap tes memeriksa satu hal, ketika Anda menemukan bug — sebelum memperbaiki tulis tes yang akan mendeteksi bug ini di masa mendatang, biarkan setiap tes gagal setidaknya sekali sebelum berubah menjadi hijau, mulai modul dengan menulis kode cepat dan sederhana yang memenuhi pengujian - kemudian refactor secara bertahap dan bawa ke tingkat kelas produksi, hindari ketergantungan pada lingkungan (jalur, OS, dll)
<br/>

❌ **Jika tidak:** Anda akan kehilangan mutiara kebijaksanaan yang dikumpulkan selama beberapa dekade

<br/><br/>

# Bagian 2️⃣: Pengujian Backend

## ⚪ ️2.1 Perkaya portofolio pengujian Anda: Lihat melampaui pengujian unit dan piramida

:white_check_mark: **Lakukan:** [Testing pyramid](https://martinfowler.com/bliki/TestPyramid.html), meskipun berusia 10> tahun, adalah model hebat dan relevan yang menyarankan tiga jenis pengujian dan memengaruhi sebagian besar strategi pengujian pengembang. Pada saat yang sama, lebih dari segelintir teknik pengujian baru yang mengkilap muncul dan bersembunyi di bayang-bayang piramida pengujian. Mengingat semua perubahan dramatis yang telah kita lihat dalam 10 tahun terakhir (Microservices, cloud, tanpa server), apakah mungkin satu model yang cukup lama akan cocok untuk semua jenis aplikasi? bukankah seharusnya dunia pengujian mempertimbangkan untuk menyambut teknik pengujian baru?

Jangan salah paham, pada tahun 2019 piramida pengujian, TDD, dan pengujian unit masih merupakan teknik yang kuat dan mungkin paling cocok untuk banyak aplikasi. Hanya seperti model lainnya, meskipun kegunaannya, [ kadang-kadang pasti salah](https://en.wikipedia.org/wiki/All_models_are_wrong). Misalnya, pertimbangkan aplikasi IoT yang menyerap banyak peristiwa ke dalam bus pesan seperti Kafka/RabbitMQ, yang kemudian mengalir ke beberapa gudang data dan akhirnya ditanyai oleh beberapa UI analitik. Haruskah kita benar-benar menghabiskan 50% dari anggaran pengujian untuk menulis pengujian unit untuk aplikasi yang berpusat pada integrasi dan hampir tidak memiliki logika? Ketika keragaman jenis aplikasi meningkat (bot, crypto, Alexa-skills) semakin besar peluang untuk menemukan skenario di mana piramida pengujian bukan yang paling cocok.

Saatnya untuk memperkaya portofolio pengujian Anda dan menjadi akrab dengan lebih banyak jenis pengujian (poin berikutnya menyarankan beberapa ide), model pikiran seperti piramida pengujian tetapi juga mencocokkan jenis pengujian dengan masalah dunia nyata yang Anda hadapi ('Hei, API kami rusak, mari kita tulis pengujian kontrak berbasis konsumen!'), diversifikasi pengujian Anda seperti investor yang membangun portofolio berdasarkan analisis risiko — menilai di mana masalah mungkin muncul dan mencocokkan beberapa tindakan pencegahan untuk mengurangi potensi risiko tersebut

Sebuah kata peringatan: argumen TDD di dunia perangkat lunak mengambil wajah dikotomi palsu yang khas, beberapa berkhotbah untuk menggunakannya di mana-mana, yang lain berpikir itu iblis. Setiap orang yang berbicara secara mutlak salah :]

<br/>

❌ **Jika tidak:** Anda akan kehilangan beberapa alat dengan ROI yang luar biasa, beberapa seperti Fuzz, lint, dan mutasi dapat memberikan nilai dalam 10 menit

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Cindy Sridharan menyarankan portofolio pengujian yang kaya dalam postingannya yang luar biasa 'Menguji Layanan Mikro — dengan cara yang sama'

![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Contoh: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️2.2 Pengujian komponen mungkin menjadi urusan terbaik Anda

:white_check_mark: **Lakukan:** Setiap pengujian unit mencakup sebagian kecil dari aplikasi dan mahal untuk mencakup keseluruhan, sedangkan pengujian end-to-end dengan mudah mencakup banyak hal tetapi rapuh dan lebih lambat, mengapa tidak menerapkan pendekatan yang seimbang dan menulis tes yang lebih besar dari pengujian unit tetapi lebih kecil dari pengujian ujung ke ujung? Pengujian komponen adalah lagu tanpa tanda jasa dari dunia pengujian — mereka memberikan yang terbaik dari kedua dunia: kinerja yang wajar dan kemungkinan untuk menerapkan pola TDD + cakupan yang realistis dan hebat.

Tes komponen fokus pada 'unit' Microservice, mereka bekerja melawan API, tidak mengejek apa pun yang menjadi milik Microservice itu sendiri (misalnya DB nyata, atau setidaknya versi dalam memori dari DB itu) tetapi mematikan apa pun yang bersifat eksternal seperti panggilan ke layanan Micro lainnya. Dengan melakukan itu, kami menguji apa yang kami terapkan, mendekati aplikasi dari luar ke dalam dan mendapatkan kepercayaan diri yang besar dalam waktu yang wajar.

[Kami memiliki panduan lengkap yang hanya didedikasikan untuk menulis tes komponen dengan cara yang benar](https://github.com/testjavascript/nodejs-integration-tests-best-practices)

<br/>

❌ **Jika tidak:** Anda mungkin menghabiskan waktu berhari-hari untuk menulis tes unit untuk mengetahui bahwa Anda hanya mendapatkan cakupan sistem 20%

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Supertest memungkinkan pendekatan Express API dalam proses (cepat dan mencakup banyak lapisan)

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) allows approaching Express API in-process (fast and cover many layers)")

</details>

<br/><br/>

## ⚪ ️2.3 Pastikan rilis baru tidak merusak API menggunakan tes kontrak

:white_check_mark: **Lakukan:** Jadi Microservice Anda memiliki banyak klien, dan Anda menjalankan beberapa versi layanan untuk alasan kompatibilitas (membuat semua orang senang). Kemudian Anda mengubah beberapa bidang dan 'booming!', beberapa klien penting yang bergantung pada bidang ini marah. Ini adalah Catch-22 dari dunia integrasi: Sangat menantang bagi sisi server untuk mempertimbangkan semua harapan klien ganda — Di sisi lain, klien tidak dapat melakukan pengujian apa pun karena server mengontrol tanggal rilis. Ada spektrum teknik yang dapat mengurangi masalah kontrak, beberapa sederhana, lainnya lebih kaya fitur dan menuntut kurva pembelajaran yang lebih curam. Dalam pendekatan yang sederhana dan direkomendasikan, penyedia API menerbitkan paket npm dengan pengetikan API (mis. JSDoc, TypeScript). Kemudian konsumen dapat mengambil perpustakaan ini dan memanfaatkan kecerdasan dan validasi waktu codign. Pendekatan yang lebih menarik untuk digunakan [PACT](https://docs.pact.io/) yang lahir untuk meresmikan proses ini dengan pendekatan yang sangat mengganggu — bukan server yang menentukan rencana pengujian itu sendiri, melainkan klien yang menentukan pengujian dari… server! PACT dapat merekam ekspektasi klien dan meletakkannya di lokasi bersama, "broker", sehingga server dapat menarik ekspektasi dan berjalan di setiap build menggunakan pustaka PACT untuk mendeteksi kontrak yang rusak — ekspektasi klien yang tidak terpenuhi. Dengan melakukannya, semua ketidakcocokan API server-klien ditangkap lebih awal selama build/CI dan mungkin menghemat banyak frustrasi Anda
<br/>

❌ **Jika tidak:** Alternatifnya melelahkan pengujian manual atau ketakutan penyebaran

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh:

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "Examples with PACT")

![alt text](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪ ️ 2.4 Uji middlewares Anda secara terpisah

:white_check_mark: **Lakukan:** Banyak yang menghindari pengujian Middleware karena mereka mewakili sebagian kecil dari sistem dan memerlukan server Express langsung. Kedua alasan tersebut salah — Middleware berukuran kecil tetapi memengaruhi semua atau sebagian besar permintaan dan dapat diuji dengan mudah sebagai fungsi murni yang mendapatkan objek JS {req,res}. Untuk menguji fungsi middleware, seseorang harus memanggilnya dan memata-matai ([ menggunakan Sinon misalnya](https://www.npmjs.com/package/sinon)) pada interaksi dengan objek {req,res} untuk memastikan fungsi melakukan tindakan yang benar. Perpustakaan [node-mock-http](https://www.npmjs.com/package/node-mocks-http) membawanya lebih jauh dan memfaktorkan objek {req,res} bersama dengan memata-matai perilakunya. Misalnya, dapat menegaskan apakah status http yang ditetapkan pada objek res sesuai dengan harapan (Lihat contoh di bawah)
<br/>

❌ **Jika tidak:** Bug di middleware Express === bug di semua atau sebagian besar permintaan

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Menguji middleware secara terpisah tanpa mengeluarkan panggilan jaringan dan membangunkan seluruh mesin Express

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
//the middleware we want to test
const unitUnderTest = require("./middleware");
const httpMocks = require("node-mocks-http");
//Jest syntax, equivelant to describe() & it() in Mocha
test("A request without authentication header, should return http status 403", () => {
  const request = httpMocks.createRequest({
    method: "GET",
    url: "/user/42",
    headers: {
      authentication: "",
    },
  });
  const response = httpMocks.createResponse();
  unitUnderTest(request, response);
  expect(response.statusCode).toBe(403);
});
```

</details>

<br/><br/>

## ⚪ ️2.5 Ukur dan refactor menggunakan alat analisis statis

:white_check_mark: **Lakukan:** Menggunakan alat analisis statis membantu dengan memberikan cara objektif untuk meningkatkan kualitas kode dan menjaga agar kode Anda tetap dapat dipelihara. Anda dapat menambahkan alat analisis statis ke CI build Anda untuk dibatalkan ketika menemukan kode berbau. Nilai jual utamanya dibandingkan linting biasa adalah kemampuan untuk memeriksa kualitas dalam konteks beberapa file (misalnya mendeteksi duplikasi), melakukan analisis lanjutan (misalnya kompleksitas kode) dan mengikuti sejarah dan kemajuan masalah kode. Dua contoh alat yang dapat Anda gunakan adalah [SonarQube](https://www.sonarqube.org/) (4,900+ [stars](https://github.com/SonarSource/sonarqube)) dan [Code Climate](https://codeclimate.com/) (2,000+ [stars](https://github.com/codeclimate/codeclimate))

Credit: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **Jika tidak:** Dengan kualitas kode yang buruk, bug dan kinerja akan selalu menjadi masalah yang tidak dapat diperbaiki oleh perpustakaan baru yang mengkilap atau fitur canggih

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: CodeClimate, alat komersial yang dapat mengidentifikasi metode kompleks:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Examples with CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png "CodeClimate, a commercial tool that can identify complex methods:")

</details>

<br/><br/>

## ⚪ ️ 2.6 Periksa kesiapan Anda untuk kekacauan terkait Node

:white_check_mark: **Do:** Anehnya, sebagian besar pengujian perangkat lunak hanya tentang logika & data, tetapi beberapa hal terburuk yang terjadi (dan sangat sulit untuk dikurangi) adalah masalah infrastruktur. Misalnya, apakah Anda pernah menguji apa yang terjadi ketika memori proses Anda kelebihan beban, atau ketika server/proses mati, atau apakah sistem pemantauan Anda menyadari ketika API menjadi 50% lebih lambat?. Untuk menguji dan mengurangi jenis hal buruk ini —  [Chaos engineering](https://principlesofchaos.org/) (rekayasa kekacauan) lahir oleh Netflix. Ini bertujuan untuk memberikan kesadaran, kerangka kerja, dan alat untuk menguji ketahanan aplikasi kami untuk masalah kacau. Misalnya, salah satu alat terkenalnya, [the chaos monkey](https://github.com/Netflix/chaosmonkey), secara acak membunuh server untuk memastikan bahwa layanan kami masih dapat melayani pengguna dan tidak bergantung pada satu server (ada juga versi Kubernetes, [kube-monkey](https://github.com/asobti/kube-monkey), that kills pods). Semua alat ini berfungsi pada tingkat hosting/platform, tetapi bagaimana jika Anda ingin menguji dan menghasilkan kekacauan Node murni seperti memeriksa bagaimana proses Node Anda mengatasi kesalahan yang tidak tertangkap, penolakan janji yang tidak tertangani, memori v8 kelebihan beban dengan maksimum yang diizinkan 1,7GB atau apakah UX Anda tetap memuaskan ketika loop acara sering diblokir? untuk mengatasi ini saya telah menulis, [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) yang menyediakan semua jenis tindakan kacau terkait Node
<br/>

❌ **Jika tidak:** Tidak ada jalan keluar di sini, hukum Murphy akan memukul produksi Anda tanpa ampun

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: : Node-chaos dapat menghasilkan semua jenis lelucon Node.js sehingga Anda dapat menguji seberapa tahan aplikasi Anda terhadap kekacauan

![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/>

## ⚪ ️2.7 Hindari perlengkapan dan benih tes global, tambahkan data per tes

:white_check_mark: **Lakukan:** Mengikuti aturan emas (butir 0), setiap pengujian harus menambahkan dan bertindak pada kumpulan baris DB-nya sendiri untuk mencegah kopling dan dengan mudah menjelaskan tentang alur pengujian. Pada kenyataannya, ini sering dilanggar oleh penguji yang menyemai DB dengan data sebelum menjalankan pengujian (juga dikenal sebagai 'perlengkapan pengujian') demi peningkatan kinerja. Sementara kinerja memang menjadi perhatian yang valid — itu dapat dikurangi (lihat butir "Pengujian komponen"), namun, kompleksitas pengujian adalah kesedihan yang sangat menyakitkan yang harus mengatur pertimbangan lain sebagian besar waktu. Secara praktis, buat setiap kasus uji secara eksplisit menambahkan catatan DB yang dibutuhkan dan bertindak hanya pada catatan tersebut. Jika kinerja menjadi perhatian kritis — kompromi yang seimbang mungkin muncul dalam bentuk penyemaian satu-satunya rangkaian pengujian yang tidak mengubah data (misalnya kueri)
<br/>

❌ **Jika tidak:** Beberapa tes gagal, penerapan dibatalkan, tim kami akan menghabiskan waktu yang berharga sekarang, apakah kami memiliki bug? mari kita selidiki, oh tidak — sepertinya dua tes mengubah data benih yang sama

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: pengujian tidak independen dan bergantung pada beberapa kait global untuk memberi makan data DB global

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
before(async () => {
  //adding sites and admins data to our DB. Where is the data? outside. At some external json or migration framework
  await DB.AddSeedDataFromJson("seed.json");
});
it("When updating site name, get successful confirmation", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(
    siteToUpdate,
    "newName"
  );
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Failure! The previous test change the name :[
});
```

<br/>

### :clap: elakukannya dengan Benar Contoh: Kita dapat tetap berada di dalam pengujian, setiap pengujian bekerja pada kumpulan datanya sendiri

```javascript
it("When updating site name, get successful confirmation", async () => {
  //test is adding a fresh new records and acting on the records only
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest",
  });
  const updateNameResult = await SiteService.changeName(
    siteUnderTest,
    "newName"
  );
  expect(updateNameResult).to.be(true);
});
```

</details>

<br/>

## ⚪ ️2.8 Pilih strategi pembersihan data yang jelas: After-all (disarankan) atau after-each

:white_check_mark: **Lakukan:** Waktu ketika tes membersihkan database menentukan cara tes ditulis. Dua opsi yang paling layak adalah pembersihan setelah semua pengujian vs pembersihan setelah setiap pengujian. Memilih opsi terakhir, pembersihan setelah setiap pengujian menjamin tabel yang bersih dan membangun fasilitas pengujian yang nyaman bagi developer. Tidak ada catatan lain saat pengujian dimulai, seseorang dapat memiliki kepastian data mana yang ditanyakan dan bahkan mungkin tergoda untuk menghitung baris selama pernyataan. Ini datang dengan kerugian parah: Saat berjalan dalam mode multi-proses, pengujian cenderung saling mengganggu. Sementara proses-1 membersihkan tabel, pada saat proses-2 meminta data dan gagal (karena DB tiba-tiba dihapus oleh proses-1). Selain itu, Lebih sulit untuk memecahkan masalah tes yang gagal - Mengunjungi DB tidak akan menunjukkan catatan.

Opsi kedua adalah membersihkan setelah semua file pengujian selesai (atau bahkan setiap hari!). Pendekatan ini berarti bahwa DB yang sama dengan catatan yang ada melayani semua pengujian dan proses. Untuk menghindari menginjak kaki satu sama lain, tes harus menambahkan dan bertindak pada catatan tertentu yang telah mereka tambahkan. Perlu memeriksa bahwa beberapa catatan telah ditambahkan? Asumsikan bahwa ada ribuan rekaman dan kueri lainnya untuk rekaman yang ditambahkan secara eksplisit. Perlu memeriksa bahwa catatan telah dihapus? Tidak dapat menganggap tabel kosong, periksa apakah catatan khusus ini tidak ada. Teknik ini membawa beberapa keuntungan yang kuat: Ia bekerja secara native dalam mode multi-proses, ketika pengembang ingin memahami apa yang terjadi - data ada di sana dan tidak dihapus. Ini juga meningkatkan kemungkinan menemukan bug karena DB penuh dengan catatan dan tidak kosong secara artifisial. [See the full comparison table here](https://github.com/testjavascript/nodejs-integration-tests-best-practices/blob/master/graphics/db-clean-options.png).
<br/>

❌ **Jika tidak:** Tanpa strategi untuk memisahkan catatan atau membersihkan - Tes akan menginjak kaki satu sama lain; Menggunakan transaksi hanya akan berfungsi untuk DB relasional dan cenderung menjadi rumit setelah ada transaksi dalam

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Membersihkan setelah SEMUA tes. Tidak perlu setelah setiap lari. Semakin banyak data yang kami miliki saat pengujian berjalan - Semakin mirip dengan fasilitas produksi

```javascript
// After-all clean up (recommended)
// global-teardown.js
module.exports = async () => {
  // ...
  if (Math.ceil(Math.random() * 10) === 10) {
    await new OrderRepository().cleanup();
  }
};
```

</details>

<br/>

## ⚪ ️2.9 Pisahkan komponen dari dunia menggunakan pencegat HTTP

:white_check_mark: **Lakukan:** Pisahkan komponen yang sedang diuji dengan mencegat setiap permintaan HTTP keluar dan memberikan respons yang diinginkan sehingga HTTP API kolaborator tidak akan terkena. Nock adalah alat yang hebat untuk misi ini karena menyediakan sintaks yang nyaman untuk mendefinisikan perilaku layanan eksternal. Isolasi adalah suatu keharusan untuk mencegah kebisingan dan kinerja yang lambat tetapi sebagian besar untuk mensimulasikan berbagai skenario dan tanggapan - Simulator penerbangan yang baik bukan tentang melukis langit biru jernih melainkan membawa badai dan kekacauan yang aman. Ini diperkuat dalam arsitektur Microservice di mana fokusnya harus selalu pada satu komponen tanpa melibatkan seluruh dunia. Meskipun mungkin untuk mensimulasikan perilaku layanan eksternal menggunakan uji ganda (mengejek), lebih baik untuk tidak menyentuh kode yang diterapkan dan bertindak pada tingkat jaringan untuk menjaga pengujian murni kotak hitam.
<br/>

❌ **Jika Tidak:** Beberapa layanan menyediakan versi palsu yang dapat digunakan oleh pemanggil secara lokal, biasanya menggunakan Docker - Ini akan memudahkan pengaturan dan meningkatkan kinerja tetapi tidak akan membantu dengan mensimulasikan berbagai tanggapan; Beberapa layanan menyediakan lingkungan 'kotak pasir', sehingga layanan sebenarnya terkena tetapi tidak ada biaya atau efek samping yang dipicu - Ini akan mengurangi kebisingan pengaturan layanan pihak ke-3 tetapi juga tidak mengizinkan skenario simulasi

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Mencegah panggilan jaringan ke komponen eksternal memungkinkan skenario simulasi dan meminimalkan kebisingan

```javascript
// Intercept requests for 3rd party APIs and return a predefined response
beforeEach(() => {
  nock("http://localhost/user/").get(`/1`).reply(200, {
    id: 1,
    name: "John",
  });
});
```

</details>

## ⚪ ️2.10 Uji skema respons, sebagian besar ketika ada bidang yang dibuat secara otomatis

:white_check_mark: **Lakukan:** Jika tidak mungkin untuk menegaskan data tertentu, periksa keberadaan dan jenis bidang wajib. Terkadang, respons berisi bidang penting dengan data dinamis yang tidak dapat diprediksi saat menulis tes, seperti tanggal dan angka yang bertambah. Jika kontrak API menjanjikan bahwa bidang ini tidak akan kosong dan memiliki tipe yang tepat, Anda harus mengujinya. Sebagian besar pustaka pernyataan mendukung jenis pemeriksaan. Jika responsnya kecil, periksa kembali data dan ketik bersama-sama dalam pernyataan yang sama (lihat contoh kode). Satu opsi lagi adalah memverifikasi seluruh respons terhadap dokumen OpenAPI (Swagger). Sebagian besar test runner memiliki ekstensi komunitas yang memvalidasi respons API terhadap dokumentasi mereka.

<br/>

❌ **Jika Tidak:** Meskipun pemanggil kode/API bergantung pada beberapa bidang dengan data dinamis (misalnya, ID, tanggal), itu tidak akan kembali dan melanggar kontrak

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Menegaskan bahwa bidang dengan nilai dinamis ada dan memiliki tipe yang tepat

```javascript
test("When adding a new valid order, Then should get back approval with 200 response", async () => {
  // ...
  //Assert
  expect(receivedAPIResponse).toMatchObject({
    status: 200,
    data: {
      id: expect.any(Number), // Any number satisfies this test
      mode: "approved",
    },
  });
});
```

</details>

<br/>

## ⚪ ️2.12 Periksa kasus sudut integrasi dan kekacauan

:white_check_mark: **Lakukan:** Saat memeriksa integrasi, lewati jalur bahagia dan sedih. Periksa tidak hanya tanggapan yang salah (misalnya, kesalahan HTTP 500) tetapi juga anomali tingkat jaringan seperti tanggapan yang lambat dan waktu habis. Ini akan membuktikan bahwa kode tersebut tangguh dan dapat menangani berbagai skenario jaringan seperti mengambil jalur yang benar setelah batas waktu, tidak memiliki kondisi balapan yang rapuh, dan berisi pemutus sirkuit untuk percobaan ulang. Alat pencegat yang bereputasi baik dapat dengan mudah mensimulasikan berbagai perilaku jaringan seperti layanan sibuk yang terkadang gagal. Ia bahkan dapat menyadari ketika nilai batas waktu klien HTTP default lebih lama dari waktu respons yang disimulasikan dan langsung membuang pengecualian batas waktu tanpa menunggu

<br/>

❌ **Jika tidak:** Semua tes Anda lulus, hanya produksi yang akan mogok atau tidak akan melaporkan kesalahan dengan benar ketika pihak ketiga mengirim tanggapan yang luar biasa

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Memastikan bahwa pada kegagalan jaringan, pemutus sirkuit dapat menyelamatkan hari

```javascript
test("When users service replies with 503 once and retry mechanism is applied, then an order is added successfully", async () => {
  //Arrange
  nock.removeInterceptor(userServiceNock.interceptors[0]);
  nock("http://localhost/user/")
    .get("/1")
    .reply(503, undefined, { "Retry-After": 100 });
  nock("http://localhost/user/").get("/1").reply(200);
  const orderToAdd = {
    userId: 1,
    productId: 2,
    mode: "approved",
  };

  //Act
  const response = await axiosAPIClient.post("/order", orderToAdd);

  //Assert
  expect(response.status).toBe(200);
});
```

</details>

<br/>

## ⚪ ️2.13 Uji lima hasil potensial

:white_check_mark: **Lakukan:** Saat merencanakan pengujian Anda, pertimbangkan untuk mencakup lima keluaran aliran yang khas. Saat pengujian Anda memicu beberapa tindakan (misalnya, panggilan API), reaksi sedang terjadi, sesuatu yang berarti terjadi, dan panggilan untuk pengujian. Perhatikan bahwa kami tidak peduli tentang bagaimana segala sesuatunya bekerja. Fokus kami adalah pada hasil, hal-hal yang terlihat dari luar dan mungkin memengaruhi pengguna. Hasil/reaksi ini dapat dimasukkan ke dalam 5 kategori:

• Respons - Tes memanggil tindakan (misalnya, melalui API) dan mendapat respons. Sekarang berkaitan dengan memeriksa kebenaran data respons, skema, dan status HTTP

• Status baru - Setelah menjalankan tindakan, beberapa data yang **dapat diakses publik** mungkin dimodifikasi

• Panggilan eksternal - Setelah menjalankan suatu tindakan, aplikasi mungkin memanggil komponen eksternal melalui HTTP atau transportasi lainnya. Misalnya, panggilan untuk mengirim SMS, email atau menagih kartu kredit

• Antrian pesan - Hasil dari suatu aliran mungkin berupa pesan dalam antrean

• Observabilitas - Beberapa hal harus dipantau, seperti kesalahan atau peristiwa bisnis yang luar biasa. Ketika transaksi gagal, tidak hanya kami mengharapkan respons yang tepat tetapi juga penanganan kesalahan yang benar dan pencatatan/metrik yang tepat. Informasi ini langsung ke pengguna yang sangat penting - Pengguna operasi (yaitu, SRE/admin produksi)

</details>

<br/><br/>

# Bagian 3️⃣: Pengujian Frontend

## ⚪ ️ 3.1 Pisahkan UI dari fungsionalitas

:white_check_mark: **Lakukan:** Saat berfokus pada logika komponen pengujian, detail UI menjadi noise yang harus diekstraksi, sehingga pengujian Anda dapat fokus pada data murni. Secara praktis, ekstrak data yang diinginkan dari markup dengan cara abstrak yang tidak terlalu digabungkan dengan implementasi grafik, tegaskan hanya pada data murni (vs detail grafik HTML/CSS) dan nonaktifkan animasi yang melambat. Anda mungkin tergoda untuk menghindari rendering dan pengujian hanya bagian belakang UI (mis. layanan, tindakan, penyimpanan) tetapi ini akan menghasilkan pengujian fiktif yang tidak menyerupai kenyataan dan tidak akan mengungkapkan kasus di mana data yang benar tidak' t bahkan tiba di UI

<br/>

❌ **Jika tidak:** Data kalkulasi murni dari pengujian Anda mungkin siap dalam 10 md, tetapi kemudian seluruh tes akan berlangsung 500 md (100 tes = 1 mnt) karena beberapa animasi yang mewah dan tidak relevan

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Memisahkan detail UI

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
test("When users-list is flagged to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [
    { id: 1, name: "Yoni Goldberg", vip: false },
    { id: 2, name: "John Doe", vip: true },
  ];

  // Act
  const { getAllByTestId } = render(
    <UsersList users={allUsers} showOnlyVIP={true} />
  );

  // Assert - Extract the data from the UI first
  const allRenderedUsers = getAllByTestId("user").map(
    (uiElement) => uiElement.textContent
  );
  const allRealVIPUsers = allUsers
    .filter((user) => user.vip)
    .map((user) => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); //compare data with data, no UI here
});
```

<br/>

### :thumbsdown: Contoh Anti-Pola: Asersi campuran detail UI dan data

```javascript
test("When flagging to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [
    { id: 1, name: "Yoni Goldberg", vip: false },
    { id: 2, name: "John Doe", vip: true },
  ];

  // Act
  const { getAllByTestId } = render(
    <UsersList users={allUsers} showOnlyVIP={true} />
  );

  // Assert - Mix UI & data in assertion
  expect(getAllByTestId("user")).toEqual(
    '[<li data-test-id="user">John Doe</li>]'
  );
});
```

</details>

<br/><br/>

## ⚪ ️ 3.2 Elemen HTML kueri berdasarkan atribut yang tidak mungkin berubah

:white_check_mark: **Lakukan:** Membuat kueri elemen HTML berdasarkan atribut yang cenderung bertahan dari perubahan grafik tidak seperti pemilih CSS dan label formulir yang disukai. Jika elemen yang ditunjuk tidak memiliki atribut seperti itu, buat atribut pengujian khusus seperti 'test-id-submit-button'. Mengikuti rute ini tidak hanya memastikan bahwa pengujian fungsional/logika Anda tidak pernah rusak karena perubahan tampilan & nuansa, tetapi juga menjadi jelas bagi seluruh tim bahwa elemen dan atribut ini digunakan oleh pengujian dan tidak boleh dihapus

<br/>

❌ **Jika tidak:** Anda ingin menguji fungsionalitas login yang mencakup banyak komponen, logika, dan layanan, semuanya sudah diatur dengan sempurna - stub, mata-mata, panggilan Ajax diisolasi. Semua tampak sempurna. Kemudian pengujian gagal karena desainer mengubah kelas CSS div dari 'thick-border' menjadi 'thin-border'

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Membuat kueri elemen menggunakan atribut khusus untuk pengujian

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React")

```html
// the markup code (part of React component)
<h3>
  <Badge pill className="fixed_badge" variant="dark">
    <span data-test-id="errorsLabel">{value}</span>
    <!-- note the attribute data-test-id -->
  </Badge>
</h3>
```

```javascript
// this example is using react-testing-library
test("Whenever no data is passed to metric, show 0 as default", () => {
  // Arrange
  const metricValue = undefined;

  // Act
  const { getByTestId } = render(<dashboardMetric value={undefined} />);

  expect(getByTestId("errorsLabel").text()).toBe("0");
});
```

<br/>

### :thumbsdown: Contoh Anti-Pola: Mengandalkan atribut CSS

```html
<!-- the markup code (part of React component) -->
<span id="metric" className="d-flex-column">{value}</span>
<!-- what if the designer changes the classs? -->
```

```javascript
// this exammple is using enzyme
test("Whenever no data is passed, error metric shows zero", () => {
  // ...

  expect(wrapper.find("[className='d-flex-column']").text()).toBe("0");
});
```

</details>

<br/>

## ⚪ ️ 3.3 Bila memungkinkan, uji dengan komponen yang realistis dan sepenuhnya dirender

:white_check_mark: **Lakukan:** Kapan pun ukurannya wajar, uji komponen Anda dari luar seperti yang dilakukan pengguna Anda, render UI sepenuhnya, tindak lanjuti, dan nyatakan bahwa UI yang dirender berperilaku seperti yang diharapkan. Hindari semua jenis ejekan, rendering parsial dan dangkal - pendekatan ini dapat mengakibatkan bug yang tidak terperangkap karena kurangnya detail dan memperkeras pemeliharaan karena pengujian mengacaukan internal (lihat butir ['pengujian kotak hitam yang disukai'](https://github.com/goldbergyoni/javascript-testing-best-practices#-%EF%B8%8F-14-stick-to-black-box-testing-test-only-public-methods)). Jika salah satu komponen anak melambat secara signifikan (misalnya animasi) atau mempersulit pengaturan - pertimbangkan untuk menggantinya secara eksplisit dengan yang palsu

Dengan semua itu, sebuah kata peringatan adalah agar: teknik ini bekerja untuk komponen kecil/menengah yang mengemas komponen anak dengan ukuran yang wajar. Render sepenuhnya komponen dengan terlalu banyak anak akan mempersulit alasan tentang kegagalan pengujian (analisis akar penyebab) dan mungkin menjadi terlalu lambat. Dalam kasus seperti itu, tulis hanya beberapa tes terhadap komponen induk gemuk itu dan lebih banyak tes terhadap anak-anaknya

<br/>

❌ **Jika tidak:** Saat menyodok ke internal komponen dengan menerapkan metode pribadinya, dan memeriksa keadaan bagian dalam - Anda harus memfaktorkan ulang semua tes saat memfaktorkan ulang implementasi komponen. Apakah Anda benar-benar memiliki kapasitas untuk tingkat pemeliharaan ini?

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Bekerja secara realistis dengan komponen yang dirender sepenuhnya

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20Enzyme-blue.svg "Examples with Enzyme")

```javascript
class Calendar extends React.Component {
  static defaultProps = { showFilters: false };

  render() {
    return (
      <div>
        A filters panel with a button to hide/show filters
        <FiltersPanel showFilter={showFilters} title="Choose Filters" />
      </div>
    );
  }
}

//Examples use React & Enzyme
test("Realistic approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = mount(<Calendar showFilters={false} />);

  // Act
  wrapper.find("button").simulate("click");

  // Assert
  expect(wrapper.text().includes("Choose Filter"));
  // This is how the user will approach this element: by text
});
```

### :thumbsdown: Contoh Anti-Pola: Mocking kenyataan dengan rendering yang dangkal

```javascript
test("Shallow/mocked approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = shallow(
    <Calendar showFilters={false} title="Choose Filter" />
  );

  // Act
  wrapper.find("filtersPanel").instance().showFilters();
  // Tap into the internals, bypass the UI and invoke a method. White-box approach

  // Assert
  expect(wrapper.find("Filter").props()).toEqual({ title: "Choose Filter" });
  // what if we change the prop name or don't pass anything relevant?
});
```

</details>

<br/>

## ⚪ ️ 3.4 Jangan tidur, gunakan dukungan bawaan kerangka kerja untuk acara asinkron. Juga cobalah untuk mempercepat

:white_check_mark: **Lakukan:** Dalam banyak kasus, waktu penyelesaian unit yang diuji tidak diketahui (misalnya animasi menangguhkan tampilan elemen) - dalam hal ini, hindari tidur (misalnya setTimeOut) dan pilih metode yang lebih deterministik yang disediakan sebagian besar platform. Beberapa perpustakaan memungkinkan menunggu operasi (misalnya [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), yang lain menyediakan API untuk menunggu seperti [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance). Terkadang cara yang lebih elegan adalah dengan mematikan sumber daya yang lambat, seperti API misalnya, dan kemudian setelah momen respons menjadi deterministik, komponen tersebut dapat dirender ulang secara eksplisit. Ketika tergantung pada beberapa komponen eksternal yang tidur, mungkin berguna untuk [mempercepat jam](https://jestjs.io/docs/en/timer-mocks). Tidur adalah pola yang harus dihindari karena memaksa tes Anda menjadi lambat atau berisiko (ketika menunggu dalam waktu yang terlalu singkat). Setiap kali tidur dan polling tidak dapat dihindari dan tidak ada dukungan dari kerangka pengujian, beberapa perpustakaan npm seperti [wait-for-expect](https://www.npmjs.com/package/wait-for-expect) dapat membantu dengan solusi semi-deterministik
<br/>

❌ **Jika tidak:** Saat tidur untuk waktu yang lama, tes akan menjadi urutan besarnya lebih lambat. Saat mencoba tidur untuk jumlah kecil, pengujian akan gagal ketika unit yang diuji tidak merespons secara tepat waktu. Jadi itu bermuara pada trade-off antara kerapuhan dan kinerja buruk

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: E2E API yang diselesaikan hanya ketika operasi asinkron selesai (Cypress)

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")
![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: Melakukannya dengan Benar Contoh: Menguji pustaka yang menunggu elemen DOM

```javascript
// @testing-library/dom
test("movie title appears", async () => {
  // element is initially not present...

  // wait for appearance
  await wait(() => {
    expect(getByText("the lion king")).toBeInTheDocument();
  });

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

### :thumbsdown: Contoh Anti-Pola: kode tidur khusus

```javascript
test("movie title appears", async () => {
  // element is initially not present...

  // custom wait logic (caution: simplistic, no timeout)
  const interval = setInterval(() => {
    const found = getByText("the lion king");
    if (found) {
      clearInterval(interval);
      expect(getByText("the lion king")).toBeInTheDocument();
    }
  }, 100);

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

</details>

<br/>

## ⚪ ️ 3.5 Perhatikan bagaimana konten disajikan melalui jaringan

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Examples with Lighthouse")

✅ **Lakukan:** Terapkan beberapa monitor aktif yang memastikan pemuatan halaman di bawah jaringan nyata dioptimalkan - ini termasuk masalah UX seperti pemuatan halaman yang lambat atau bundel yang tidak diperkecil. Pasar alat inspeksi tidak pendek: alat dasar seperti [pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) dapat dengan mudah dikonfigurasi untuk melihat apakah server hidup dan merespons di bawah SLA yang wajar. Ini hanya menggores permukaan dari apa yang mungkin salah, oleh karena itu lebih baik memilih alat yang berspesialisasi dalam frontend (misalnya. [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) dan melakukan analisis yang lebih kaya. Fokusnya harus pada gejala, metrik yang secara langsung memengaruhi UX, seperti waktu buka halaman, [cat yang bermakna](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [waktu sampai halaman menjadi interaktif (TTI)](https://calibreapp.com/blog/time-to-interactive/). Selain itu, Anda juga dapat memperhatikan penyebab teknis seperti memastikan konten dikompresi, waktu ke byte pertama, mengoptimalkan gambar, memastikan ukuran DOM yang wajar, SSL, dan banyak lainnya. Dianjurkan untuk memiliki monitor kaya ini baik selama pengembangan, sebagai bagian dari CI dan yang paling penting - 24x7 melalui server/CDN produksi

<br/>

❌ **Jika tidak:** Pasti mengecewakan untuk menyadari bahwa setelah sangat hati-hati untuk membuat UI, tes fungsional 100% lulus dan bundling canggih - UX mengerikan dan lambat karena kesalahan konfigurasi CDN

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

### :clap: Doing It Right Example: Lighthouse page load inspection report

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

</details>

<br/>

## ⚪ ️ 3.6 Sumber daya yang tidak stabil dan lambat seperti API backend

:white_check_mark: **Lakukan:** Saat mengkodekan pengujian arus utama Anda (bukan pengujian E2E), hindari melibatkan sumber daya apa pun yang berada di luar tanggung jawab dan kendali Anda seperti API backend dan gunakan stub sebagai gantinya (yaitu uji ganda). Praktis, alih-alih panggilan jaringan nyata ke API, gunakan beberapa perpustakaan uji ganda (seperti [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), dll) untuk mematikan respons API. Manfaat utamanya adalah mencegah kerapuhan - pengujian atau pementasan API menurut definisi tidak terlalu stabil dan dari waktu ke waktu akan gagal dalam pengujian Anda meskipun komponen ANDA berperilaku baik (env produksi tidak dimaksudkan untuk pengujian dan biasanya membatasi permintaan). Melakukan hal ini akan memungkinkan simulasi berbagai perilaku API yang seharusnya mendorong perilaku komponen Anda seperti saat tidak ada data yang ditemukan atau kasus saat API melontarkan kesalahan. Last but not least, panggilan jaringan akan sangat memperlambat tes

<br/>

❌ **Jika tidak:** Tes rata-rata berjalan tidak lebih dari beberapa md, panggilan API tipikal berlangsung 100 md>, ini membuat setiap pengujian ~20x lebih lambat

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: 👏Melakukannya dengan Benar Contoh: Menghentikan atau mencegat panggilan API

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// unit under test
export default function ProductsList() {
  const [products, setProducts] = useState(false);

  const fetchProducts = async () => {
    const products = await axios.get("api/products");
    setProducts(products);
  };

  useEffect(() => {
    fetchProducts();
  }, []);

  return products ? (
    <div>{products}</div>
  ) : (
    <div data-test-id="no-products-message">No products</div>
  );
}

// test
test("When no products exist, show the appropriate message", () => {
  // Arrange
  nock("api").get(`/products`).reply(404);

  // Act
  const { getByTestId } = render(<ProductsList />);

  // Assert
  expect(getByTestId("no-products-message")).toBeTruthy();
});
```

</details>

<br/>

## ⚪ ️ 3.7 Memiliki sangat sedikit pengujian ujung ke ujung yang mencakup seluruh sistem

:white_check_mark: **Lakukan:** Meskipun E2E (end-to-end) biasanya berarti pengujian hanya UI dengan browser nyata (lihat [butir 3.6](https://github.com/goldbergyoni/javascript-testing-best-practices#-%EF%B8%8F-36-stub-flaky-and-slow-resources-like-backend-apis)), untuk yang lain itu berarti pengujian yang meregangkan seluruh sistem termasuk backend yang sebenarnya. Jenis tes yang terakhir sangat berharga karena mencakup bug integrasi antara frontend dan backend yang mungkin terjadi karena pemahaman yang salah tentang skema pertukaran. Mereka juga merupakan metode yang efisien untuk menemukan masalah integrasi backend-to-backend (misalnya Microservice A mengirim pesan yang salah ke Microservice B) dan bahkan untuk mendeteksi kegagalan penerapan - tidak ada kerangka kerja backend untuk pengujian E2E yang ramah dan matang seperti UI kerangka kerja seperti [Cypress](https://www.cypress.io/) dan [Puppeteer](https://github.com/GoogleChrome/puppeteer). Kelemahan dari tes semacam itu adalah tingginya biaya untuk mengonfigurasi lingkungan dengan begitu banyak komponen, dan sebagian besar kerapuhannya - mengingat 50 layanan mikro, bahkan jika salah satu gagal maka seluruh E2E gagal total. Untuk alasan itu, kita harus menggunakan teknik ini dengan hemat dan mungkin memiliki 1-10 di antaranya dan tidak lebih. Meskipun demikian, bahkan sejumlah kecil tes E2E cenderung menangkap jenis masalah yang menjadi target mereka - kesalahan penerapan & integrasi. Disarankan untuk menjalankannya di lingkungan pementasan seperti produksi

<br/>

❌ **Jika tidak:** UI mungkin berinvestasi banyak dalam menguji fungsinya hanya untuk menyadari sangat terlambat bahwa backend mengembalikan payload (skema data yang harus digunakan UI) sangat berbeda dari yang diharapkan

<br/>

## ⚪ ️ 3.8 Mempercepat tes E2E dengan menggunakan kembali kredensial login

:white_check_mark: **Lakukan:** Dalam pengujian E2E yang melibatkan backend nyata dan bergantung pada token pengguna yang valid untuk panggilan API, tidak ada gunanya mengisolasi pengujian ke tingkat di mana pengguna dibuat dan masuk dalam setiap permintaan. Sebagai gantinya, login hanya sekali sebelum eksekusi tes dimulai (yaitu sebelum semua hook), simpan token di beberapa penyimpanan lokal dan gunakan kembali di seluruh permintaan. Ini tampaknya melanggar salah satu prinsip pengujian inti - menjaga pengujian tetap otonom tanpa sambungan sumber daya. Meskipun ini adalah kekhawatiran yang valid, dalam pengujian E2E, kinerja adalah perhatian utama dan membuat 1-3 permintaan API sebelum memulai setiap pengujian individu dapat menyebabkan waktu eksekusi yang mengerikan. Menggunakan kembali kredensial tidak berarti pengujian harus dilakukan pada catatan pengguna yang sama - jika mengandalkan catatan pengguna (mis uji riwayat pembayaran pengguna) daripada pastikan untuk membuat catatan tersebut sebagai bagian dari pengujian dan hindari berbagi keberadaannya dengan pengujian lain. Juga ingat bahwa backend dapat dipalsukan - jika pengujian Anda difokuskan pada frontend, mungkin lebih baik untuk mengisolasinya dan mematikan API backend (lihat [butir 3.6](https://github.com/goldbergyoni/javascript-testing-best-practices#-%EF%B8%8F-36-stub-flaky-and-slow-resources-like-backend-apis)).

<br/>

❌ **Jika tidak:** Diberikan 200 kasus uji dan dengan asumsi login=100ms = 20 detik hanya untuk login berulang kali

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Masuk sebelum semua dan bukan sebelum masing-masing

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
let authenticationToken;

// happens before ALL tests run
before(() => {
  cy.request('POST', 'http://localhost:3000/login', {
    username: Cypress.env('username'),
    password: Cypress.env('password'),
  })
  .its('body')
  .then((responseFromLogin) => {
    authenticationToken = responseFromLogin.token;
  })
})

// happens before EACH test
beforeEach(setUser => () {
  cy.visit('/home', {
    onBeforeLoad (win) {
      win.localStorage.setItem('token', JSON.stringify(authenticationToken))
    },
  })
})

```

</details>

<br/>

## ⚪ ️ 3.9 Memiliki satu tes asap E2E yang baru saja melintasi peta situs

:white_check_mark: **Lakukan:** Untuk pemantauan produksi dan pemeriksaan kewarasan waktu pengembangan, jalankan satu tes E2E yang mengunjungi semua/sebagian besar halaman situs dan memastikan tidak ada yang rusak. Jenis pengujian ini memberikan pengembalian investasi yang besar karena sangat mudah untuk ditulis dan dipelihara, tetapi dapat mendeteksi segala jenis kegagalan termasuk masalah fungsional, jaringan, dan penerapan. Gaya pemeriksaan asap dan kewarasan lainnya tidak dapat diandalkan dan lengkap - beberapa tim operasi hanya melakukan ping ke halaman beranda (produksi) atau pengembang yang menjalankan banyak tes integrasi yang tidak menemukan masalah pengemasan dan browser. Tak perlu dikatakan bahwa tes asap tidak menggantikan tes fungsional, melainkan hanya bertujuan untuk berfungsi sebagai pendeteksi asap cepat

<br/>

❌ **Jika tidak:** Semuanya mungkin tampak sempurna, semua tes lulus, pemeriksaan kesehatan produksi juga positif tetapi komponen Pembayaran memiliki beberapa masalah pengemasan dan hanya /Rute pembayaran yang tidak ditampilkan

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Asap mengembara di semua halaman

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
it("When doing smoke testing over all page, should load them all successfully", () => {
  // exemplified using Cypress but can be implemented easily
  // using any E2E suite
  cy.visit("https://mysite.com/home");
  cy.contains("Home");
  cy.visit("https://mysite.com/Login");
  cy.contains("Login");
  cy.visit("https://mysite.com/About");
  cy.contains("About");
});
```

</details>

<br/>

## ⚪ ️ 3.10 Mengekspos tes sebagai dokumen kolaboratif langsung

:white_check_mark: **Lakukan:** Selain meningkatkan keandalan aplikasi, pengujian menghadirkan peluang menarik lainnya - berfungsi sebagai dokumentasi aplikasi langsung. Karena tes secara inheren berbicara dengan bahasa yang kurang teknis dan produk/UX, menggunakan alat yang tepat, tes dapat berfungsi sebagai artefak komunikasi yang sangat menyelaraskan semua rekan - pengembang dan pelanggan mereka. Misalnya, beberapa kerangka kerja memungkinkan mengekspresikan aliran dan harapan (yaitu rencana pengujian) menggunakan bahasa yang dapat dibaca manusia sehingga setiap pemangku kepentingan, termasuk manajer produk, dapat membaca, menyetujui, dan berkolaborasi dalam pengujian yang baru saja menjadi dokumen persyaratan langsung. Teknik ini juga disebut sebagai 'tes penerimaan' karena memungkinkan pelanggan untuk menentukan kriteria penerimaannya dalam bahasa yang sederhana. Ini adalah [BDD (behavior-driven testing)](https://en.wikipedia.org/wiki/Behavior-driven_development) pada bentuknya yang paling murni. Salah satu framework populer yang mengaktifkan ini adalah [Cucumber which has a JavaScript flavor](https://github.com/cucumber/cucumber-js), lihat contoh di bawah ini. Kesempatan lain yang serupa namun berbeda, [StoryBook](https://storybook.js.org/), memungkinkan mengekspos komponen UI sebagai katalog grafis di mana seseorang dapat berjalan melalui berbagai status setiap komponen (misalnya membuat kisi tanpa filter, membuat kisi itu dengan beberapa baris atau tanpa tidak ada, dll), lihat bagaimana tampilannya, dan bagaimana memicu keadaan itu - ini dapat menarik juga bagi orang-orang produk tetapi sebagian besar berfungsi sebagai dokumen langsung untuk pengembang yang menggunakan komponen tersebut.

❌ **Jika tidak:** Setelah menginvestasikan sumber daya teratas pada pengujian, sayang sekali untuk tidak memanfaatkan investasi ini dan memenangkan nilai yang besar

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Menggambarkan tes dalam bahasa manusia menggunakan cucumber-js

![](https://img.shields.io/badge/🔨%20Example%20using%20Cucumber-blue.svg "Examples using Cucumber")

```javascript
// this is how one can describe tests using cucumber: plain language that allows anyone to understand and collaborate

Feature: Twitter new tweet

  I want to tweet something in Twitter

  @focus
  Scenario: Tweeting from the home page
    Given I open Twitter home
    Given I click on "New tweet" button
    Given I type "Hello followers!" in the textbox
    Given I click on "Submit" button
    Then I see message "Tweet saved"

```

### :clap: Melakukannya dengan Benar Contoh: Memvisualisasikan komponen kami, berbagai status dan inputnya menggunakan Storybook

![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Using StoryBook")

![alt text](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪ ️ 3.11 Mendeteksi masalah visual dengan alat otomatis

:white_check_mark: **Lakukan:** Siapkan alat otomatis untuk mengambil tangkapan layar UI saat perubahan ditampilkan dan mendeteksi masalah visual seperti konten yang tumpang tindih atau rusak. Hal ini memastikan bahwa tidak hanya data yang benar yang disiapkan tetapi juga pengguna dapat dengan mudah melihatnya. Teknik ini tidak diadopsi secara luas, pola pikir pengujian kami condong ke tes fungsional tetapi visualnya adalah pengalaman pengguna dan dengan begitu banyak jenis perangkat, sangat mudah untuk mengabaikan beberapa bug UI yang buruk. Beberapa alat gratis dapat memberikan dasar-dasarnya - menghasilkan dan menyimpan tangkapan layar untuk pemeriksaan mata manusia. Meskipun pendekatan ini mungkin cukup untuk aplikasi kecil, itu cacat seperti pengujian manual lainnya yang menuntut tenaga manusia setiap kali ada perubahan. Di sisi lain, itu' s cukup menantang untuk mendeteksi masalah UI secara otomatis karena kurangnya definisi yang jelas - di sinilah bidang 'Regresi Visual' berpadu dan memecahkan teka-teki ini dengan membandingkan UI lama dengan perubahan terbaru dan mendeteksi perbedaan. Beberapa OSS/alat gratis dapat menyediakan beberapa fungsi ini ([wraith](https://github.com/BBC-News/wraith) , [PhantomCSS](<[https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)>) tetapi mungkin membebani waktu pengaturan yang signifikan. Lini alat komersial (misalnya [Applitools](https://applitools.com/) , [Percy.io](https://percy.io/) ) mengambil langkah lebih jauh dengan menghaluskan instalasi dan mengemas fitur-fitur canggih seperti UI manajemen, peringatan, penangkapan cerdas dengan menghilangkan 'gangguan visual' (misalnya iklan, animasi) dan bahkan akar masalah analisis perubahan DOM/CSS yang menyebabkan masalah

<br/>

❌ **Jika tidak:** Seberapa bagus halaman konten yang menampilkan konten hebat (100% tes lulus), dimuat secara instan tetapi setengah dari area konten disembunyikan?

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Regresi visual yang khas - konten yang benar yang disajikan dengan buruk

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>

### :clap: Melakukannya dengan Benar Contoh: Mengonfigurasi wraith untuk menangkap dan membandingkan snapshot UI

![](https://img.shields.io/badge/🔨%20Example%20using%20Wraith-blue.svg "Using Wraith")

```
​# Add as many domains as necessary. Key will act as a label​

domains:
  english: "http://www.mysite.com"​

​# Type screen widths below, here are a couple of examples​

screen_widths:

  - 600​
  - 768​
  - 1024​
  - 1280​

​# Type page URL paths below, here are a couple of examples​
paths:
  about:
    path: /about
    selector: '.about'​
  subscribe:
      selector: '.subscribe'​
    path: /subscribe
```

### :clap: Melakukannya dengan Benar Contoh: Menggunakan Applitools untuk mendapatkan perbandingan snapshot dan fitur lanjutan lainnya

![](https://img.shields.io/badge/🔨%20Example%20using%20AppliTools-blue.svg "Using Applitools") ![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
import * as todoPage from "../page-objects/todo-page";

describe("visual validation", () => {
  before(() => todoPage.navigate());
  beforeEach(() => cy.eyesOpen({ appName: "TAU TodoMVC" }));
  afterEach(() => cy.eyesClose());

  it("should look good", () => {
    cy.eyesCheckWindow("empty todo list");
    todoPage.addTodo("Clean room");
    todoPage.addTodo("Learn javascript");
    cy.eyesCheckWindow("two todos");
    todoPage.toggleTodo(0);
    cy.eyesCheckWindow("mark as completed");
  });
});
```

</details>

<br/><br/>

# Bagian 4️⃣: Mengukur Efektivitas Tes

<br/><br/>

## ⚪ ️ 4.1 Dapatkan cakupan yang cukup untuk menjadi percaya diri, ~80% tampaknya menjadi angka keberuntungan

:white_check_mark: **Do:** Tujuan pengujian adalah untuk mendapatkan kepercayaan diri yang cukup untuk bergerak cepat, jelas semakin banyak kode yang diuji semakin percaya diri tim. Cakupan adalah ukuran berapa banyak baris kode (dan cabang, pernyataan, dll) yang dicapai oleh tes. Jadi berapa cukup? 10–30% jelas terlalu rendah untuk memahami kebenaran build, di sisi lain 100% sangat mahal dan mungkin mengalihkan fokus Anda dari jalur kritis ke sudut kode yang eksotis. Jawaban panjangnya adalah bahwa itu tergantung pada banyak faktor seperti jenis aplikasi — jika Anda sedang membangun generasi berikutnya dari Airbus A380 dari 100% adalah suatu keharusan, untuk situs web gambar kartun 50% mungkin terlalu banyak. Meskipun sebagian besar penggemar pengujian mengklaim bahwa ambang cakupan yang tepat adalah kontekstual, sebagian besar dari mereka juga menyebutkan angka 80% sebagai aturan praktis ([Fowler: di atas 80-an atau 90-an”](https://martinfowler.com/bliki/TestCoverage.html)) yang mungkin harus memenuhi sebagian besar aplikasi.

Kiat penerapan: Anda mungkin ingin mengonfigurasi continuous integration (CI) Anda agar memiliki ambang cakupan (([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean))) dan menghentikan build yang tidak sesuai dengan standar ini (juga dimungkinkan untuk mengonfigurasi ambang batas per komponen, lihat contoh kode di bawah) . Selain itu, pertimbangkan untuk mendeteksi penurunan cakupan build (ketika kode yang baru dikomit memiliki cakupan yang lebih sedikit) — ini akan mendorong pengembang untuk meningkatkan atau setidaknya mempertahankan jumlah kode yang diuji. Semua yang dikatakan, cakupan hanyalah satu ukuran, yang berbasis kuantitatif, yang tidak cukup untuk memberi tahu ketahanan pengujian Anda. Dan itu juga bisa ditipu seperti yang diilustrasikan dalam peluru berikutnya

<br/>

❌ **Jika tidak:** Keyakinan dan angka berjalan beriringan, tanpa benar-benar mengetahui bahwa Anda menguji sebagian besar sistem — juga akan ada ketakutan dan ketakutan akan memperlambat Anda

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Contoh: Laporan liputan tipikal

![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: Melakukannya dengan Benar Contoh: Menyiapkan cakupan per komponen (menggunakan Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Using Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)")

</details>

<br/><br/>

## ⚪ ️ 4.2 Periksa laporan cakupan untuk mendeteksi area yang belum diuji dan keanehan lainnya

:white_check_mark: **Lakukan:** Beberapa masalah menyelinap di bawah radar dan sangat sulit ditemukan menggunakan alat tradisional. Ini bukan benar-benar bug tetapi lebih dari perilaku aplikasi mengejutkan yang mungkin berdampak parah. Misalnya, seringkali beberapa area kode tidak pernah atau jarang dipanggil — Anda mengira bahwa kelas 'PricingCalculator' selalu menetapkan harga produk tetapi ternyata sebenarnya tidak pernah dipanggil meskipun kami memiliki 10.000 produk di DB dan banyak penjualan… Cakupan kode laporan membantu Anda menyadari apakah aplikasi berperilaku seperti yang Anda yakini. Selain itu, ia juga dapat menyoroti jenis kode mana yang tidak diuji — diberi tahu bahwa 80% dari kode yang diuji tidak memberi tahu apakah bagian penting tercakup. Membuat laporan itu mudah — cukup jalankan aplikasi Anda dalam produksi atau selama pengujian dengan pelacakan cakupan, lalu lihat laporan penuh warna yang menyoroti seberapa sering setiap area kode dipanggil. Jika Anda meluangkan waktu untuk melihat sekilas data ini — Anda mungkin menemukan beberapa kesalahan
<br/>

❌ **Jika tidak:** Jika Anda tidak tahu bagian mana dari kode Anda yang belum diuji, Anda tidak tahu dari mana masalah itu berasal

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Apa yang salah dengan laporan liputan ini?

Berdasarkan skenario dunia nyata di mana kami melacak penggunaan aplikasi kami di QA dan menemukan pola login yang menarik (Petunjuk: jumlah kegagalan login tidak proporsional, ada sesuatu yang jelas salah. Akhirnya ternyata beberapa bug frontend terus memukul API masuk backend)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report?")

</details>

<br/><br/>

## ⚪ ️ 4.3 Ukur cakupan logis menggunakan pengujian mutasi

:white_check_mark: **Lakukan:** Metrik Cakupan Tradisional sering kali berbohong: Ini mungkin menunjukkan cakupan kode 100%, tetapi tidak ada fungsi Anda, bahkan tidak satu pun, yang mengembalikan respons yang benar. Bagaimana bisa? itu hanya mengukur baris kode mana yang dikunjungi tes, tetapi tidak memeriksa apakah tes benar-benar menguji apa pun — ditegaskan untuk respons yang benar. Seperti seseorang yang bepergian untuk bisnis dan menunjukkan stempel paspornya — ini tidak membuktikan pekerjaan apa pun yang dilakukan, hanya saja dia mengunjungi beberapa bandara dan hotel.

Pengujian berbasis mutasi hadir untuk membantu dengan mengukur jumlah kode yang sebenarnya DIUJI bukan hanya DIKUNJUNGI. [Stryker](https://stryker-mutator.io/) adalah pustaka JavaScript untuk pengujian mutasi dan implementasinya sangat rapi:

(1) sengaja mengubah kode dan "menanam bug". Misalnya kode newOrder.price===0 menjadi newOrder.price!=0. "Bug" ini disebut mutasi

(2) menjalankan tes, jika semua berhasil maka kita punya masalah — tes tidak melayani tujuan mereka menemukan bug, mutasi disebut bertahan. Jika tes gagal, maka bagus, mutasi terbunuh.

Mengetahui bahwa semua atau sebagian besar mutasi terbunuh memberikan kepercayaan yang jauh lebih tinggi daripada cakupan tradisional dan waktu penyiapannya serupa
<br/>

❌ **Jika tidak:** Anda akan tertipu untuk percaya bahwa cakupan 85% berarti pengujian Anda akan mendeteksi bug di 85% kode Anda

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: cakupan 100%, pengujian 0%

![](https://img.shields.io/badge/🔨%20Example%20using%20Stryker-blue.svg "Using Stryker")

```javascript
function addNewOrder(newOrder) {
  logger.log(`Adding new order ${newOrder}`);
  DB.save(newOrder);
  Mailer.sendMail(newOrder.assignee, `A new order was places ${newOrder}`);

  return { approved: true };
}

it("Test addNewOrder, don't use such test names", () => {
  addNewOrder({ assignee: "John@mailer.com", price: 120 });
}); //Triggers 100% code coverage, but it doesn't check anything
```

<br/>

### :clap: Melakukannya dengan Benar Contoh: Stryker report, alat untuk pengujian mutasi, mendeteksi dan menghitung jumlah kode yang tidak diuji (Mutations)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>

<br/><br/>

## ⚪ ️4.4 Mencegah masalah kode pengujian dengan linter Uji

:white_check_mark: **Lakukan:** Satu set plugin ESLint dibuat khusus untuk memeriksa pola kode pengujian dan menemukan masalah. Misalnya, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) akan memperingatkan saat tes ditulis di tingkat global (bukan anak dari pernyataan deskripsi()) atau saat tes [dilewati](https://mochajs.org/#inclusive-tests) yang mungkin mengarah pada keyakinan salah bahwa semua tes lulus. Demikian pula, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) dapat, misalnya, memperingatkan ketika tes tidak memiliki pernyataan sama sekali (tidak memeriksa apa pun)

<br/>

❌ **Jika tidak:** Melihat cakupan kode 90% dan tes hijau 100% akan membuat wajah Anda tersenyum lebar hanya sampai Anda menyadari bahwa banyak tes tidak menyatakan apa pun dan banyak rangkaian tes dilewati. Mudah-mudahan, Anda tidak menyebarkan apa pun berdasarkan pengamatan yang salah ini

<br/>
<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Kasus uji penuh kesalahan, untungnya semua ditangkap oleh Linters

```javascript
describe("Too short description", () => {
  const userToken = userService.getDefaultToken() // *error:no-setup-in-describe, use hooks (sparingly) instead
  it("Some description", () => {});//* error: valid-test-description. Must include the word "Should" + at least 5 words
});

it.skip("Test name", () => {// *error:no-skipped-tests, error:error:no-global-tests. Put tests only under describe or suite
  expect("somevalue"); // error:no-assert
});

it("Test name", () => {*//error:no-identical-title. Assign unique titles to tests
});
```

</details>

<br/><br/>

# Bagian 5️⃣: CI dan Ukuran Kualitas Lainnya

<br/><br/>

## ⚪ ️ 5.1 Perkaya linter Anda dan batalkan build yang memiliki masalah linting

:white_check_mark: **Do:** Linters are a free lunch, with 5 min setup you get for free an auto-pilot guarding your code and catching significant issue as you type. Gone are the days where linting was about cosmetics (no semi-colons!). Nowadays, Linters can catch severe issues like errors that are not thrown correctly and losing information. On top of your basic set of rules (like [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) or [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), consider including some specializing Linters like [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) that can discover tests without assertions, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) can discover promises with no resolve (your code will never continue), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) which can discover eager regex expressions that might get used for DOS attacks, and [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) is capable of alarming when the code uses utility library methods that are part of the V8 core methods like Lodash.\_map(…)

:white_check_mark: **Lakukan:** Linter adalah makan siang gratis, dengan pengaturan 5 menit Anda mendapatkan auto-pilot gratis yang menjaga kode Anda dan menangkap masalah signifikan saat Anda mengetik. Lewatlah sudah hari-hari di mana linting adalah tentang kosmetik (tidak ada titik koma!). Saat ini, Linters dapat menangkap masalah parah seperti kesalahan yang tidak terlempar dengan benar dan kehilangan informasi. Selain seperangkat aturan dasar Anda (seperti [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) atau [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), pertimbangkan untuk menyertakan beberapa Linter khusus seperti [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) yang dapat menemukan pengujian tanpa pernyataan, eslint-plugin-promise dapat menemukan janji tanpa penyelesaian ( kode tidak akan pernah berlanjut), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) yang dapat menemukan ekspresi regex bersemangat yang mungkin digunakan untuk serangan DOS, dan [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) mampu mengkhawatirkan ketika kode menggunakan metode pustaka utilitas yang merupakan bagian dari metode inti V8 seperti Lodash. \_peta(…)

<br/>

❌ **Otherwise:** Pertimbangkan hari hujan di mana produksi Anda terus mogok tetapi log tidak menampilkan jejak tumpukan kesalahan. Apa yang terjadi? Kode Anda secara keliru melemparkan objek non-kesalahan dan jejak tumpukan hilang, alasan yang bagus untuk membenturkan kepala Anda ke dinding bata. Penyiapan linter 5 menit dapat mendeteksi TYPO ini dan menghemat hari Anda

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :thumbsdown: Contoh Anti-Pola: Objek Kesalahan yang salah dilemparkan secara keliru, tidak ada jejak-tumpukan yang akan muncul untuk kesalahan ini. Untungnya, ESLint menangkap bug produksi berikutnya

![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>

<br/><br/>

## ⚪ ️ 5.2 Persingkat loop umpan balik dengan pengembang lokal-CI

:white_check_mark: **Lakukan:** Menggunakan CI dengan pemeriksaan kualitas yang bagus seperti pengujian, linting, pemeriksaan kerentanan, dll? Bantu pengembang menjalankan saluran ini juga secara lokal untuk mengumpulkan umpan balik instan dan mempersingkat [feedback loop](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/) . Mengapa? proses pengujian yang efisien terdiri dari banyak pengulangan dan pengulangan: (1) uji coba -> (2) umpan balik -> (3) refactor. Semakin cepat umpan baliknya, semakin banyak iterasi peningkatan yang dapat dilakukan pengembang per modul dan menyempurnakan hasilnya. Sebaliknya, ketika umpan balik terlambat datang, lebih sedikit iterasi peningkatan yang dapat dikemas dalam satu hari, tim mungkin sudah beralih ke topik/tugas/modul lain dan mungkin tidak siap untuk menyempurnakan modul itu.

Praktis, beberapa vendor CI (Contoh: [CircleCI local CLI](https://circleci.com/docs/2.0/local-cli/) ) memungkinkan menjalankan pipeline secara lokal. Beberapa alat komersial seperti [walabi memberikan wawasan yang sangat berharga & pengujian](https://wallabyjs.com/) sebagai prototipe pengembang (tanpa afiliasi). Atau, Anda dapat menambahkan skrip npm ke package.json yang menjalankan semua perintah kualitas (mis. pengujian, lint, kerentanan) — gunakan alat seperti [concurrently](https://www.npmjs.com/package/concurrently) untuk paralelisasi dan kode keluar bukan nol jika salah satu alat gagal. Sekarang pengembang hanya perlu menjalankan satu perintah — misalnya 'npm run quality' — untuk mendapatkan umpan balik instan. Pertimbangkan juga untuk membatalkan komit jika pemeriksaan kualitas gagal menggunakan githook ( husky dapat membantu )

<br/>

❌ **Jika tidak:** Ketika hasil kualitas tiba sehari setelah kode, pengujian tidak menjadi bagian pengembangan yang lancar, melainkan artefak formal setelah fakta

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: skrip npm yang melakukan pemeriksaan kualitas kode, semuanya dijalankan secara paralel sesuai permintaan atau saat pengembang mencoba mendorong kode baru

```javascript
"scripts": {
    "inspect:sanity-testing": "mocha **/**--test.js --grep \"sanity\"",
    "inspect:lint": "eslint .",
    "inspect:vulnerabilities": "npm audit",
    "inspect:license": "license-checker --failOn GPLv2",
    "inspect:complexity": "plato .",

    "inspect:all": "concurrently -c \"bgBlue.bold,bgMagenta.bold,yellow\" \"npm:inspect:quick-testing\" \"npm:inspect:lint\" \"npm:inspect:vulnerabilities\" \"npm:inspect:license\""
  },
  "husky": {
    "hooks": {
      "precommit": "npm run inspect:all",
      "prepush": "npm run inspect:all"
    }
}

```

</details>

<br/><br/>

## ⚪ ️5.3 Lakukan pengujian e2e melalui cermin produksi yang sebenarnya

:white_check_mark: **Lakukan:** Pengujian ujung ke ujung (e2e) adalah tantangan utama setiap saluran CI — membuat cermin produksi singkat yang identik dengan cepat dengan semua layanan cloud terkait bisa jadi membosankan dan mahal. Menemukan kompromi terbaik adalah permainan Anda: [Docker-compose](https://serverless.com/) memungkinkan pembuatan lingkungan docker yang terisolasi dengan wadah identik menggunakan satu file teks biasa tetapi teknologi dukungan (misalnya jaringan, model penyebaran) berbeda dari produksi dunia nyata. Anda dapat menggabungkannya dengan [‘AWS Local’](https://github.com/localstack/localstack) untuk bekerja dengan rintisan layanan AWS yang sebenarnya. Jika Anda menggunakan beberapa kerangka kerja tanpa server seperti [serverless](https://serverless.com/) dan [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) memungkinkan pemanggilan lokal kode FaaS .

Ekosistem Kubernetes yang besar belum memformalkan alat standar yang nyaman untuk pencerminan lokal dan CI meskipun banyak alat baru sering diluncurkan. Salah satu pendekatan adalah menjalankan 'Kubernetes yang diperkecil' menggunakan alat seperti [Minikube](https://kubernetes.io/docs/setup/minikube/) dan [MicroK8s](https://microk8s.io/) yang menyerupai aslinya hanya dengan biaya overhead yang lebih sedikit. Pendekatan lain adalah pengujian melalui 'real-Kubernetes' jarak jauh, beberapa penyedia CI (misalnya [Codefresh](https://codefresh.io/) ) memiliki integrasi asli dengan lingkungan Kubernetes dan memudahkan untuk menjalankan pipeline CI melalui hal yang nyata, yang lain mengizinkan skrip kustom terhadap Kubernetes jarak jauh.

<br/>

❌ **Jika tidak:** Menggunakan teknologi berbeda untuk produksi dan pengujian menuntut mempertahankan dua model penerapan dan memisahkan pengembang dan tim operasi

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Contoh: pipeline CI yang menghasilkan cluster Kubernetes dengan cepat <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credit: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪ ️5.4 Parallelize eksekusi tes

:white_check_mark: **Lakukan:** Jika dilakukan dengan benar, pengujian adalah teman 24/7 Anda yang memberikan umpan balik yang hampir instan. Dalam praktiknya, menjalankan 500 unit test CPU-bounded pada satu thread bisa memakan waktu terlalu lama. Untungnya, test runner modern dan platform CI (seperti ekstensi [Jest](https://github.com/facebook/jest) , [AVA](https://github.com/avajs/ava) dan [Mocha extensions](https://github.com/yandex/mocha-parallel-tests) ) dapat memparalelkan pengujian ke dalam beberapa proses dan mencapai peningkatan yang signifikan dalam waktu umpan balik. Beberapa vendor CI juga memparalelkan pengujian di seluruh container (!) yang memperpendek loop umpan balik lebih jauh. Baik secara lokal melalui beberapa proses, atau melalui beberapa CLI cloud menggunakan beberapa mesin — memparalelkan permintaan menjaga agar pengujian tetap otonom karena masing-masing dapat berjalan pada proses yang berbeda

❌ **Jika tidak:** Mendapatkan hasil pengujian 1 jam setelah mendorong kode baru, karena Anda sudah mengkodekan fitur berikutnya, adalah resep yang bagus untuk membuat pengujian menjadi kurang relevan

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh: Mocha parallel & Jest dengan mudah mengungguli Mocha tradisional berkat pengujian paralelisasi ([Credit: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))

![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>

<br/><br/>

## ⚪ ️5.5 Jauhi masalah hukum menggunakan lisensi dan cek plagiarisme

:white_check_mark: **Do:** Licensing and plagiarism issues are probably not your main concern right now, but why not tick this box as well in 10 minutes? A bunch of npm packages like [license check](https://www.npmjs.com/package/license-checker) and [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commercial with free plan) can be easily baked into your CI pipeline and inspect for sorrows like dependencies with restrictive licenses or code that was copy-pasted from Stack Overflow and apparently violates some copyrights

Masalah lisensi dan plagiarisme mungkin bukan masalah utama Anda saat ini, tetapi mengapa tidak mencentang kotak ini juga dalam 10 menit? Sekelompok paket npm seperti [license check](https://www.npmjs.com/package/license-checker) dan [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (komersial dengan paket gratis) dapat dengan mudah dimasukkan ke dalam pipa CI Anda dan memeriksa kesedihan seperti dependensi dengan lisensi atau kode terbatas yang disalin dari Stack Overflow dan tampaknya melanggar beberapa hak cipta

❌ **Jika tidak:** Secara tidak sengaja, pengembang mungkin menggunakan paket dengan lisensi yang tidak sesuai atau menyalin kode komersial dan mengalami masalah hukum

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Melakukannya dengan Benar Contoh:

```javascript
//install license-checker in your CI environment or also locally
npm install -g license-checker

//ask it to scan all licenses and fail with exit code other than 0 if it found unauthorized license. The CI system should catch this failure and stop the build
license-checker --summary --failOn BSD

```

<br/>

![alt text](assets/bp-25-nodejs-licsense.png)

</details>

<br/><br/>

## ⚪ ️5.6 Selalu periksa dependensi yang rentan

:white_check_mark: **Lakukan:** Bahkan dependensi paling terkemuka seperti Express telah mengetahui kerentanannya. Ini dapat dengan mudah dijinakkan menggunakan alat komunitas seperti [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), atau alat komersial seperti [snyk](https://snyk.io/) (menawarkan juga versi komunitas gratis). Keduanya dapat dipanggil dari CI Anda di setiap build

❌ **Jika tidak:** Menjaga kode Anda tetap bersih dari kerentanan tanpa alat khusus akan mengharuskan Anda untuk terus-menerus mengikuti publikasi online tentang ancaman baru. Cukup membosankan

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Contoh: Hasil Audit NPM

![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>

<br/><br/>

## ⚪ ️5.7 Mengotomatiskan pembaruan ketergantungan

:white_check_mark: **Lakukan:** yarn dan npm pengenalan terbaru dari package-lock.json memperkenalkan tantangan serius (jalan menuju neraka diaspal dengan niat baik) — secara default sekarang, paket tidak lagi mendapatkan pembaruan. Bahkan tim yang menjalankan banyak penerapan baru dengan 'npm install' & 'npm update' tidak akan mendapatkan pembaruan baru. Ini mengarah ke versi paket yang bergantung di bawah standar atau kode yang rentan paling buruk. Tim sekarang mengandalkan niat baik dan memori pengembang untuk memperbarui package.json secara manual atau menggunakan alat seperti [ncu](https://www.npmjs.com/package/npm-check-updates) secara manual. Cara yang lebih andal adalah dengan mengotomatiskan proses mendapatkan versi ketergantungan yang paling andal, meskipun tidak ada solusi peluru perak namun ada dua kemungkinan jalan otomatisasi:

(1) CI dapat gagal membangun yang memiliki dependensi usang — menggunakan alat seperti 'npm usang' atau 'npm-check-updates (ncu)' . Melakukannya akan memaksa pengembang untuk memperbarui dependensi.

(2) Gunakan alat komersial yang memindai kode dan secara otomatis mengirim permintaan tarik dengan dependensi yang diperbarui. Satu pertanyaan menarik yang tersisa adalah apa yang seharusnya menjadi kebijakan pembaruan ketergantungan — pembaruan pada setiap tambalan menghasilkan terlalu banyak overhead, memperbarui tepat ketika mayor dirilis mungkin mengarah ke versi yang tidak stabil (banyak paket yang ditemukan rentan pada hari-hari pertama setelah dirilis, [lihat eslint-scope ](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/)).

Kebijakan pembaruan yang efisien memungkinkan beberapa 'periode vesting' — biarkan kode tertinggal di belakang @latest untuk beberapa waktu dan versi sebelum mempertimbangkan salinan lokal sebagai usang (misalnya versi lokal adalah 1.3.1 dan versi repositori adalah 1.3.8)
<br/>

❌ **Otherwise:** Produksi Anda akan menjalankan paket yang secara eksplisit ditandai oleh pembuatnya sebagai berisiko
<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Contoh: [ncu](https://www.npmjs.com/package/npm-check-updates) dapat digunakan secara manual atau dalam pipa CI untuk mendeteksi sejauh mana kode tertinggal di belakang versi terbaru

![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")

</details>

<br/><br/>

## ⚪ ️ 5.8 Lainnya, tidak terkait Node, kiat CI

:white_check_mark: **Lakukan:** Posting ini difokuskan pada saran pengujian yang terkait dengan, atau setidaknya dapat dicontohkan dengan Node JS. Peluru ini, bagaimanapun, mengelompokkan beberapa tip terkait non-Node yang terkenal

1. Gunakan sintaks deklaratif. Ini adalah satu-satunya pilihan untuk sebagian besar vendor tetapi versi Jenkins yang lebih lama memungkinkan penggunaan kode atau UI
2. Pilih vendor yang memiliki dukungan Docker asli
3. Gagal lebih awal, jalankan tes tercepat Anda terlebih dahulu. Buat langkah/tonggak 'Pengujian asap' yang mengelompokkan beberapa pemeriksaan cepat (misalnya linting, pengujian unit) dan memberikan umpan balik yang cepat kepada pembuat kode
4. Permudah untuk menelusuri semua artefak build termasuk laporan pengujian, laporan cakupan, laporan mutasi, log, dll
5. Buat beberapa saluran/pekerjaan untuk setiap acara, gunakan kembali langkah-langkah di antaranya. Misalnya, konfigurasikan pekerjaan untuk komitmen cabang fitur dan yang berbeda untuk PR master. Biarkan setiap logika penggunaan kembali menggunakan langkah bersama (kebanyakan vendor menyediakan beberapa mekanisme untuk penggunaan kembali kode)
6. Jangan pernah menyematkan rahasia dalam deklarasi pekerjaan, ambil dari toko rahasia atau dari konfigurasi pekerjaan
7. Bunyikan versi secara eksplisit dalam versi rilis atau setidaknya pastikan pengembang melakukannya
8. Build hanya sekali dan lakukan semua inspeksi pada artefak build tunggal (mis. gambar Docker)
9. Uji di lingkungan singkat yang tidak mengubah status antar build. Caching node_modules mungkin satu-satunya pengecualian

   <br/>

❌ **Jika tidak:** Anda akan kehilangan kebijaksanaan selama bertahun-tahun

<br/><br/>

## ⚪ ️ 5.9 Bangun matriks: Jalankan langkah CI yang sama menggunakan beberapa versi Node

:white_check_mark: **Lakukan:** Pemeriksaan kualitas adalah tentang kebetulan, semakin banyak dasar yang Anda cakup, semakin beruntung Anda dalam mendeteksi masalah lebih awal. Saat mengembangkan paket yang dapat digunakan kembali atau menjalankan produksi multipelanggan dengan berbagai konfigurasi dan versi Node, CI harus menjalankan jalur pengujian pada semua permutasi konfigurasi. Misalnya, dengan asumsi kita menggunakan MySQL untuk beberapa pelanggan dan Postgres untuk yang lain — beberapa vendor CI mendukung fitur yang disebut 'Matrix' yang memungkinkan menjalankan setelan pengujian terhadap semua permutasi MySQL, Postgres, dan beberapa versi Node seperti 8, 9 dan 10. Ini dilakukan hanya dengan menggunakan konfigurasi tanpa upaya tambahan apa pun (dengan asumsi Anda memiliki pengujian atau pemeriksaan kualitas lainnya). CI lain yang tidak mendukung Matrix mungkin memiliki ekstensi atau penyesuaian untuk memungkinkannya
<br/>

❌ **Jika tidak:** Jadi setelah melakukan semua kerja keras pengujian penulisan, apakah kita akan membiarkan bug menyelinap masuk hanya karena masalah konfigurasi?

<br/>

<details><summary>✏ <b>Contoh Kode</b></summary>

<br/>

### :clap: Contoh: Menggunakan definisi build Travis (vendor CI) untuk menjalankan pengujian yang sama pada beberapa versi Node

<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# Tim

## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Peran:** Penulis

**Tentang:** Saya seorang konsultan independen yang bekerja dengan perusahaan Fortune 500 dan startup garasi dalam memoles aplikasi JS & Node.js mereka. Lebih dari topik lain yang membuat saya terpesona dan bertujuan untuk menguasai seni pengujian. Saya juga penulis [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

**📗 Kursus Online:** Menyukai panduan ini dan ingin meningkatkan keterampilan pengujian Anda? Pertimbangkan untuk mengunjungi kursus komprehensif saya [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com)

<br/>

**Follow:**

- [🐦 Twitter](https://twitter.com/goldbergyoni/)
- [📞 Contact](https://testjavascript.com/contact-2/)
- [✉️ Newsletter](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**Peran:** Peninjau dan penasihat teknologi

Berhati-hatilah untuk merevisi, meningkatkan, merapikan, dan memoles semua teks

**Tentang:** web engineer full-stack, penggemar Node.js & GraphQL

<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Peran:** Konsep, desain, dan saran bagus

**Tentang:** Pengembang frontend yang cerdas, pakar CSS, dan penggila emoji

## [Kyle Martin](https://github.com/js-kyle)

**Peran:** Membantu proyek ini tetap berjalan, dan meninjau praktik terkait keamanan

**Tentang:** Suka mengerjakan proyek Node.js dan keamanan aplikasi web.

## Kontributor ✨

Terima kasih untuk orang-orang hebat yang telah berkontribusi pada repositori ini!

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://geospatialscott.blogspot.com/"><img src="https://avatars3.githubusercontent.com/u/1326248?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Scott Davis</b></sub></a><br /><a href="#content-stdavis" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AdrienRedon"><img src="https://avatars2.githubusercontent.com/u/5978436?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Adrien REDON</b></sub></a><br /><a href="#content-AdrienRedon" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/NoriSte"><img src="https://avatars0.githubusercontent.com/u/173663?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Stefano Magni</b></sub></a><br /><a href="#content-NoriSte" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.joer.im"><img src="https://avatars2.githubusercontent.com/u/47742486?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yeoh Joer</b></sub></a><br /><a href="#content-yjoer" title="Content">🖋</a></td>
    <td align="center"><a href="http://jhonnymoreira.dev"><img src="https://avatars0.githubusercontent.com/u/2177742?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jhonny Moreira</b></sub></a><br /><a href="#content-jhonnymoreira" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Germanika"><img src="https://avatars2.githubusercontent.com/u/8846678?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ian Germann</b></sub></a><br /><a href="#content-Germanika" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AbdelrahmanHafez"><img src="https://avatars3.githubusercontent.com/u/19984935?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Hafez</b></sub></a><br /><a href="#content-AbdelrahmanHafez" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://www.ruxandrafediuc.com"><img src="https://avatars1.githubusercontent.com/u/11021586?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ruxandra Fediuc</b></sub></a><br /><a href="#content-ruxandrafed" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jacklee814"><img src="https://avatars0.githubusercontent.com/u/9951291?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jack</b></sub></a><br /><a href="#content-jacklee814" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.petercarrero.com"><img src="https://avatars0.githubusercontent.com/u/231727?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Peter Carrero</b></sub></a><br /><a href="#content-aloyr" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/huhgawz"><img src="https://avatars3.githubusercontent.com/u/369338?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Huhgawz</b></sub></a><br /><a href="#content-huhgawz" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/haakonmb"><img src="https://avatars1.githubusercontent.com/u/7099302?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Haakon Borch</b></sub></a><br /><a href="#content-haakonmb" title="Content">🖋</a></td>
    <td align="center"><a href="https://jaimemendoza.com/"><img src="https://avatars3.githubusercontent.com/u/5395811?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jaime Mendoza</b></sub></a><br /><a href="#content-jaimemendozadev" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/camerondunford"><img src="https://avatars0.githubusercontent.com/u/840612?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Cameron Dunford</b></sub></a><br /><a href="#content-camerondunford" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/shadowspawn"><img src="https://avatars1.githubusercontent.com/u/15719847?v=4?s=100" width="100px;" alt=""/><br /><sub><b>John Gee</b></sub></a><br /><a href="#content-shadowspawn" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/aurelijusrozenas"><img src="https://avatars0.githubusercontent.com/u/3273544?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Aurelijus Rožėnas</b></sub></a><br /><a href="#content-aurelijusrozenas" title="Content">🖋</a></td>
    <td align="center"><a href="http://aaronshivers.com"><img src="https://avatars2.githubusercontent.com/u/42848750?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Aaron</b></sub></a><br /><a href="#content-aaronshivers" title="Content">🖋</a></td>
    <td align="center"><a href="https://tomdoes.tech/"><img src="https://avatars1.githubusercontent.com/u/8683577?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Tom Nagle</b></sub></a><br /><a href="#content-tomanagle" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/yvesyao"><img src="https://avatars0.githubusercontent.com/u/7723729?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yves yao</b></sub></a><br /><a href="#content-yvesyao" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Userbit"><img src="https://avatars1.githubusercontent.com/u/34487074?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Userbit</b></sub></a><br /><a href="#content-Userbit" title="Content">🖋</a></td>
    <td align="center"><a href="https://glaucialemos.netlify.com/"><img src="https://avatars0.githubusercontent.com/u/1631477?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Glaucia Lemos</b></sub></a><br /><a href="#maintenance-glaucia86" title="Maintenance">🚧</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://twitter.com/koooge"><img src="https://avatars2.githubusercontent.com/u/7419215?v=4?s=100" width="100px;" alt=""/><br /><sub><b>koooge</b></sub></a><br /><a href="#content-koooge" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/michalbiesiada"><img src="https://avatars0.githubusercontent.com/u/18367606?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Michal</b></sub></a><br /><a href="#content-mbiesiad" title="Content">🖋</a></td>
    <td align="center"><a href="http://roywalker.me"><img src="https://avatars0.githubusercontent.com/u/611846?v=4?s=100" width="100px;" alt=""/><br /><sub><b>roywalker</b></sub></a><br /><a href="#content-roywalker" title="Content">🖋</a></td>
    <td align="center"><a href="https://dangen-effy.github.io/"><img src="https://avatars3.githubusercontent.com/u/23185799?v=4?s=100" width="100px;" alt=""/><br /><sub><b>dangen</b></sub></a><br /><a href="#content-dangen-effy" title="Content">🖋</a></td>
    <td align="center"><a href="https://dev.to/mbiesiad"><img src="https://avatars1.githubusercontent.com/u/60202305?v=4?s=100" width="100px;" alt=""/><br /><sub><b>biesiadamich</b></sub></a><br /><a href="#content-biesiadamich" title="Content">🖋</a></td>
    <td align="center"><a href="https://tarojsx.github.io"><img src="https://avatars3.githubusercontent.com/u/127009?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yanlin Jiang</b></sub></a><br /><a href="#content-cncolder" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/sanguino"><img src="https://avatars2.githubusercontent.com/u/2077168?v=4?s=100" width="100px;" alt=""/><br /><sub><b>sanguino</b></sub></a><br /><a href="#content-sanguino" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/MorganGeek"><img src="https://avatars0.githubusercontent.com/u/3721240?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Morgan</b></sub></a><br /><a href="#content-MorganGeek" title="Content">🖋</a></td>
    <td align="center"><a href="https://luk4s.dev"><img src="https://avatars0.githubusercontent.com/u/8350985?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Lukas Bischof</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=lukasbischof" title="Tests">⚠️</a> <a href="#content-lukasbischof" title="Content">🖋</a></td>
    <td align="center"><a href="https://juanmaruiz.surge.sh"><img src="https://avatars2.githubusercontent.com/u/1837650?v=4?s=100" width="100px;" alt=""/><br /><sub><b>JuanMa Ruiz</b></sub></a><br /><a href="#content-JuanMaRuiz" title="Content">🖋</a></td>
    <td align="center"><a href="https://luisangelorjr.com.br"><img src="https://avatars3.githubusercontent.com/u/22268900?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Luís Ângelo Rodrigues Jr.</b></sub></a><br /><a href="#content-luisangelorjr" title="Content">🖋</a></td>
    <td align="center"><a href="https://jfernandezpe.wordpress.com/"><img src="https://avatars0.githubusercontent.com/u/12046620?v=4?s=100" width="100px;" alt=""/><br /><sub><b>José Fernández</b></sub></a><br /><a href="#content-jfernandezpe" title="Content">🖋</a></td>
    <td align="center"><a href="http://www.linkedin.com/in/AlejandroGutierrezB"><img src="https://avatars3.githubusercontent.com/u/56408597?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Alejandro Gutierrez Barcenilla</b></sub></a><br /><a href="#content-AlejandroGutierrezB" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jasonandmonte"><img src="https://avatars1.githubusercontent.com/u/30088000?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jason</b></sub></a><br /><a href="#content-jasonandmonte" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/otavionetoca"><img src="https://avatars.githubusercontent.com/u/11263232?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Otavio Araujo</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=otavionetoca" title="Tests">⚠️</a> <a href="#content-otavionetoca" title="Content">🖋</a></td>
    <td align="center"><a href="https://contributor.pw"><img src="https://avatars.githubusercontent.com/u/5027939?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Alex Ivanov</b></sub></a><br /><a href="#content-contributorpw" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/YeeJone"><img src="https://avatars.githubusercontent.com/u/20400822?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yiqiao Xu</b></sub></a><br /><a href="#content-YeeJone" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/yubinTW"><img src="https://avatars.githubusercontent.com/u/31545456?v=4?s=100" width="100px;" alt=""/><br /><sub><b>YuBin, Hsu</b></sub></a><br /><a href="#translation-yubinTW" title="Translation">🌍</a> <a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=yubinTW" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->
