# <h1 align="center">Laporan Praktikum Modul 4 - Linked list Circular</h1>
<p align="center">Mohammad Alfan Naraya - 2311102170</p>
<p align="center">IF - 11 - E</p>

## Dasar Teori

### Linked List Circular

Linked List Circular adalah daftar tertaut yang semua nodenya terhubung membentuk lingkaran. Dalam daftar tertaut melingkar, simpul pertama dan simpul terakhir dihubungkan satu sama lain sehingga membentuk lingkaran. Tidak ada NULL di akhir. Umumnya ada dua jenis daftar tertaut melingkar:[1]

*Daftar tertaut tunggal melingkar*: Dalam daftar tertaut tunggal melingkar, simpul terakhir dari daftar berisi penunjuk ke simpul pertama dari daftar. Kami melintasi daftar tertaut tunggal melingkar hingga kami mencapai simpul yang sama tempat kami memulai. Daftar tertaut tunggal melingkar tidak memiliki awal atau akhir. Tidak ada nilai null di bagian selanjutnya dari node mana pun.[1]

*Daftar Tertaut Ganda Melingkar*: Daftar Tertaut Ganda Melingkar memiliki properti daftar tertaut ganda dan daftar tertaut melingkar di mana dua elemen berurutan dihubungkan atau dihubungkan oleh penunjuk sebelumnya dan berikutnya dan simpul terakhir menunjuk ke simpul pertama dengan penunjuk berikutnya dan juga simpul pertama menunjuk ke simpul terakhir dengan penunjuk sebelumnya.[1]

### Linked List Non Circular

Linked list non-circular adalah struktur data linear di mana setiap elemen terhubung ke elemen berikutnya, namun elemen terakhir tidak terhubung kembali ke elemen pertama atau ke elemen mana pun dalam linked list. Sebagai akibatnya, traversing dari awal ke akhir linked list akan berakhir ketika mencapai elemen terakhir yang menunjuk ke nilai NULL. Ini membuat manipulasi dan pengelolaan data menjadi lebih sederhana dan jelas, namun tidak memungkinkan traversing langsung kembali ke elemen pertama setelah mencapai elemen terakhir.[2]

   
## Guided 

### 1. Linked List Non Circular

```C++
//MOHAMMAD ALFAN NARAYA
//2311102170

#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

Node *head;
Node *tail;

// inialisasi Node
void init()
{
    head = NULL;
    tail = NULL;
}

// pengecekan
bool isEmpty()
{
    if (head == NULL)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// tambah depan
void insertDepan(int nilai)
{
    // buat node baru
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;

    if (isEmpty())
    {
        head = tail = baru;
        tail->next = NULL;
    }
    else
    {
        baru->next = head;
        head = baru;
    }
}

// tambah belakang
void insertBelakang(int nilai)
{
    // buat node baru
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;

    if (isEmpty())
    {
        head = tail = baru;
        tail->next = NULL;
    }
    else
    {
        tail->next = baru;
        tail = baru;
    }
}

// hitung jumlah list
int hitungList()
{
    Node *hitung;
    hitung = head;
    int jumlah = 0;

    while (hitung != NULL)
    {
        jumlah++;
        hitung = hitung->next;
    }

    return jumlah;
}

// tambah tengah
void insertTengah(int data, int posisi)
{
    if (posisi < 1 || posisi > hitungList())
    {
        cout << "Posisi diluar jangkauan" << endl;
    }
    else if (posisi == 1)
    {
        cout << "Posisi bukan di tengah" << endl;
    }
    else
    {
        Node *baru, *bantu;
        baru = new Node();
        baru->data = data;

        // tranversing
        bantu = head;
        int nomor = 1;

        while (nomor < posisi - 1)
        {
            bantu = bantu->next;
            nomor++;
        }

        baru->next = bantu->next;
        bantu->next = baru;
    }
}

// hapus depan
void hapusDepan()
{
    Node *hapus;

    if (!isEmpty())
    {
        if (head->next != NULL)
        {
            hapus = head;
            head = head->next;
            delete hapus;
        }
        else
        {
            head = tail = NULL;
        }
    }
    else
    {
        cout << "List Kosong!" << endl;
    }
}

// hapus belakang
void hapusBelakang()
{
    Node *hapus;
    Node *bantu;

    if (!isEmpty())
    {
        if (head != tail)
        {
            hapus = tail;
            bantu = head;

            while (bantu->next != tail)
            {
                bantu = bantu->next;
            }

            tail = bantu;
            tail->next = NULL;
            delete hapus;
        }
        else
        {
            head = tail = NULL;
        }
    }
    else
    {
        cout << "List Kosong!" << endl;
    }
}

// hapsu tengah
void hapusTengah(int posisi)
{
    Node *hapus, *bantu, *bantu2;

    if (posisi < 1 || posisi > hitungList())
    {
        cout << "Posisi di luar jangkauan" << endl;
    }
    else if (posisi == 1)
    {
        cout << "Posisi bukan di tengah" << endl;
    }
    else
    {
        int nomor = 1;
        bantu = head;

        while (nomor <= posisi)
        {
            if (nomor == posisi - 1)
            {
                bantu2 = bantu;
            }

            if (nomor == posisi)
            {
                hapus = bantu;
            }

            bantu = bantu->next;
            nomor++;
        }
        bantu2->next = bantu;
        delete hapus;
    }
}

// ubah depan
void ubahDepan(int data)
{
    if (!isEmpty())
    {
        head->data = data;
    }
    else
    {
        cout << "List masih kosong!" << endl;
    }
}

// ubah tengah
void ubahTengah(int data, int posisi)
{
    Node *bantu;

    if (!isEmpty())
    {
        if (posisi < 1 || posisi > hitungList())
        {
            cout << "Posisi di luar jangkauan" << endl;
        }
        else if (posisi == 1)
        {
            cout << "Posisi bukan di tengah" << endl;
        }
        else
        {
            bantu = head;
            int nomor = 1;

            while (nomor < posisi)
            {
                bantu = bantu->next;
                nomor++;
            }

            bantu->data = data;
        }
    }
    else
    {
        cout << "List masih kosong" << endl;
    }
}

// ubah belakang
void ubahBelakang(int data)
{
    if (!isEmpty())
    {
        tail->data = data;
    }
    else
    {
        cout << "List masih kosong" << endl;
    }
}

// hapus list
void clearList()
{
    Node *bantu, *hapus;
    bantu = head;

    while (bantu != NULL)
    {
        hapus = bantu;
        bantu = bantu->next;
        delete hapus;
    }

    head = tail = NULL;
    cout << "List berhasil terhapus!" << endl;
}

// tampilkan list
void tampil()
{
    Node *bantu;
    bantu = head;

    if (!isEmpty())
    {
        while (bantu != NULL)
        {
            cout << bantu->data << ends;
            bantu = bantu->next;
        }

        cout << endl;
    }
    else
    {
        cout << "List masih kosong!" << endl;
    }
}

int main()
{
    init();

    insertDepan(3);
    tampil();
    insertBelakang(5);
    tampil();
    insertDepan(2);
    tampil();
    insertDepan(1);
    tampil();
    hapusDepan();
    tampil();
    hapusBelakang();
    tampil();
    insertTengah(7, 2);
    tampil();
    hapusTengah(2);
    tampil();
    ubahDepan(1);
    tampil();
    ubahBelakang(8);
    tampil();
    ubahTengah(11, 2);
    tampil();
    
    return 0;
}
```

#### Output :
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/4e8176f2-02f1-4bc2-8b04-1907621fed6f)

Program diatas memungkinkan penambahan, penghapusan, dan perubahan elemen di depan, di belakang, dan di tengah linked list. Pada awalnya, program mendefinisikan struktur Node yang berisi data dan pointer ke node selanjutnya. Kemudian, program menyediakan fungsi-fungsi untuk operasi dasar linked list, seperti penambahan, penghapusan, dan perubahan elemen. 
Di dalam main(), serangkaian operasi tersebut dijalankan untuk menguji fungsi-fungsi tersebut, seperti menambahkan dan menghapus elemen di berbagai posisi, serta mengubah nilai elemen. Hasilnya ditampilkan setiap kali ada perubahan pada linked list.


### 2. Linked List Circular

```C++
//MOHAMMAD ALFAN NARAYA
//2311102170

#include <iostream>
using namespace std;


// program single linked list circular

// deklarasi struct node
struct Node
{
    string data;
    Node *next;
};

Node *head, *tail, *baru, *bantu, *hapus;

void init()
{
    head = NULL;
    tail = head;
}

// pengecekan
bool isEmpty()
{
    if (head == NULL)
    {
        return 1; // true
    }
    else
    {
        return 0; // false
    }
}

// buat node baru
void buatNode(string data)
{
    baru = new Node;
    baru->data = data;
    baru->next = NULL;
}

// hitung list
int hitungList()
{
    bantu = head;
    int jumlah = 0;

    while (bantu != NULL)
    {
        jumlah++;
        bantu = bantu->next;
    }

    return jumlah;
}

// tambah depan
void insertDepan(string data)
{
    // buat node baru
    buatNode(data);

    if (isEmpty())
    {
        head = baru;
        tail = head;
        baru->next = head;
    }
    else
    {
        while (tail->next != head)
        {
            tail = tail->next;
        }

        baru->next = head;
        head = baru;
        tail->next = head;
    }
}

// tambah belakan
void insertBelakang(string data)
{
    // buat node baru
    buatNode(data);

    if (isEmpty())
    {
        head = baru;
        tail = head;
        tail->next = head;
    }
    else
    {
        while (tail->next != head)
        {
            tail = tail->next;
        }

        tail->next = baru;
        baru->next = head;
        tail = baru;
    }
}

// tambah tengah
void insertTengah(string data, int posisi)
{
    if (isEmpty())
    {
        head = baru;
        tail = head;
        baru->next = head;
    }
    else
    {
        baru->data = data;

        // transversing
        int nomor = 1;
        bantu = head;

        while (nomor < posisi - 1)
        {
            bantu = bantu->next;
            nomor++;
        }

        baru->next = bantu->next;
        bantu->next = baru;
    }
}

// hapus depan
void hapusDepan()
{
    if (!isEmpty())
    {
        hapus = head;
        tail = head;

        if (hapus->next == head)
        {
            head = NULL;
            tail = NULL;

            delete hapus;
        }
        else
        {
            while (tail->next != hapus)
            {
                tail = tail->next;
            }

            head = head->next;
            tail->next = head;
            hapus->next = NULL;

            delete hapus;
        }
    }
    else
    {
        cout << "List masih kosong!" << endl;
    }
}

// hapus belakang
void hapusBelakang()
{
    if (!isEmpty())
    {
        hapus = head;
        tail = head;

        if (hapus->next == head)
        {
            head = NULL;
            tail = NULL;

            delete hapus;
        }
        else
        {
            while (hapus->next != head)
            {
                hapus = hapus->next;
            }

            while (tail->next != hapus)
            {
                tail = tail->next;
            }

            tail->next = head;
            hapus->next = NULL;

            delete hapus;
        }
    }
    else
    {
        cout << "List masih kosong!" << endl;
    }
}

// hapus tengah
void hapusTengah(int posisi)
{
    if (!isEmpty())
    {
        // transversing
        int nomor = 1;
        bantu = head;

        while (nomor < posisi - 1)
        {
            bantu = bantu->next;
            nomor++;
        }

        hapus = bantu->next;
        bantu->next = hapus->next;

        delete hapus;
    }
    else
    {
        cout << "List masih kosong!" << endl;
    }
}

// hapus list
void clearList()
{
    if (head != NULL)
    {
        hapus = head->next;

        while (hapus != head)
        {
            bantu = hapus->next;
            delete hapus;
            hapus = bantu;
        }

        delete head;
        head = NULL;
    }

    cout << "List berhasil terhapus!" << endl;
}

// tampilkan list
void tampil()
{
    if (!isEmpty())
    {
        tail = head;
        do
        {
            cout << tail->data << ends;
            tail = tail->next;
        } while (tail != head);

        cout << endl;
    }
    else
    {
        cout << "List masih kosong!" << endl;
    }
}

int main()
{
    init();
    insertDepan("Ayam");
    tampil();
    insertDepan("Bebek");
    tampil();
    insertBelakang("Cicak");
    tampil();
    insertBelakang("Domba");
    tampil();
    hapusBelakang();
    tampil();
    hapusDepan();
    tampil();
    insertTengah("Sapi", 2);
    tampil();
    hapusTengah(2);
    tampil();

    return 0;
}
```

#### Output :
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/78aba830-7ccb-4d2d-b11e-6ed9ab537403)

Program ini mendefinisikan struktur Node yang memiliki dua atribut: data dan pointer ke node berikutnya. Kemudian, program menyediakan fungsi-fungsi untuk operasi dasar pada linked list, seperti penambahan dan penghapusan elemen di depan, di belakang, dan di tengah linked list. 
Di dalam fungsi main(), serangkaian operasi tersebut dijalankan untuk menguji fungsi-fungsi tersebut. Misalnya, menambahkan elemen di depan dan di belakang, menghapus elemen di depan dan di belakang, serta menambahkan dan menghapus elemen di tengah. Setiap kali ada perubahan pada linked list, isi linked list ditampilkan.


## Unguided 

### 1. Buatlah menu untuk menambahkan, mengubah, menghapus, dan melihat Nama dan NIM mahasiswa, berikut contoh tampilan output dari nomor 1:

```C++
//MOHAMMAD ALFAN NARAYA
//2311102170

#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    Mahasiswa* next;
};

class LinkedListCircular {
private:
    Mahasiswa* head;

public:
    LinkedListCircular() {
        head = nullptr;
    }

    // Menambahkan mahasiswa di depan
    void tambahDepan(string nama, string nim) {
        Mahasiswa* newMahasiswa = new Mahasiswa;
        newMahasiswa->nama = nama;
        newMahasiswa->nim = nim;

        if (head == nullptr) {
            head = newMahasiswa;
            newMahasiswa->next = head;
        } else {
            Mahasiswa* last = head;
            while (last->next != head) {
                last = last->next;
            }
            newMahasiswa->next = head;
            last->next = newMahasiswa;
            head = newMahasiswa;
        }
        cout << "Mahasiswa berhasil ditambahkan di depan." << endl;
    }

    // Menambahkan mahasiswa di belakang
    void tambahBelakang(string nama, string nim) {
        Mahasiswa* newMahasiswa = new Mahasiswa;
        newMahasiswa->nama = nama;
        newMahasiswa->nim = nim;

        if (head == nullptr) {
            head = newMahasiswa;
            newMahasiswa->next = head;
        } else {
            Mahasiswa* last = head;
            while (last->next != head) {
                last = last->next;
            }
            last->next = newMahasiswa;
            newMahasiswa->next = head;
        }
        cout << "Mahasiswa berhasil ditambahkan di belakang." << endl;
    }

    // Menambahkan mahasiswa di tengah
    void tambahTengah(string nama, string nim, int posisi) {
        if (posisi <= 0) {
            cout << "Posisi harus lebih dari 0." << endl;
            return;
        }
        Mahasiswa* newMahasiswa = new Mahasiswa;
        newMahasiswa->nama = nama;
        newMahasiswa->nim = nim;

        if (head == nullptr) {
            head = newMahasiswa;
            newMahasiswa->next = head;
            cout << "Mahasiswa berhasil ditambahkan di tengah." << endl;
            return;
        }

        Mahasiswa* temp = head;
        int count = 1;
        while (count < posisi - 1 && temp->next != head) {
            temp = temp->next;
            count++;
        }

        if (count < posisi - 1) {
            cout << "Posisi terlalu besar." << endl;
            return;
        }

        newMahasiswa->next = temp->next;
        temp->next = newMahasiswa;
        cout << "Mahasiswa berhasil ditambahkan di tengah." << endl;
    }

    // Ubah data mahasiswa di depan
    void ubahDepan(string nama, string nim) {
        if (head == nullptr) {
            cout << "Linked List Kosong." << endl;
            return;
        }
        head->nama = nama;
        head->nim = nim;
        cout << "Data mahasiswa di depan berhasil diubah." << endl;
    }

    // Ubah data mahasiswa di belakang
    void ubahBelakang(string nama, string nim) {
        if (head == nullptr) {
            cout << "Linked List Kosong." << endl;
            return;
        }
        Mahasiswa* temp = head;
        while (temp->next != head) {
            temp = temp->next;
        }
        temp->nama = nama;
        temp->nim = nim;
        cout << "Data mahasiswa di belakang berhasil diubah." << endl;
    }

    // Ubah data mahasiswa di tengah
    void ubahTengah(string nama, string nim, int posisi) {
        if (head == nullptr) {
            cout << "Linked List Kosong." << endl;
            return;
        }
        Mahasiswa* temp = head;
        int count = 1;
        while (count < posisi && temp->next != head) {
            temp = temp->next;
            count++;
        }
        if (count != posisi) {
            cout << "Posisi terlalu besar." << endl;
            return;
        }
        temp->nama = nama;
        temp->nim = nim;
        cout << "Data mahasiswa di posisi " << posisi << " berhasil diubah." << endl;
    }

    // Hapus data mahasiswa di depan
    void hapusDepan() {
        if (head == nullptr) {
            cout << "Linked List Kosong." << endl;
            return;
        }
        if (head->next == head) {
            delete head;
            head = nullptr;
        } else {
            Mahasiswa* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            Mahasiswa* del = head;
            head = head->next;
            temp->next = head;
            delete del;
        }
        cout << "Data mahasiswa di depan berhasil dihapus." << endl;
    }

    // Hapus data mahasiswa di belakang
    void hapusBelakang() {
        if (head == nullptr) {
            cout << "Linked List Kosong." << endl;
            return;
        }
        if (head->next == head) {
            delete head;
            head = nullptr;
        } else {
            Mahasiswa* temp = head;
            Mahasiswa* prev = nullptr;
            while (temp->next != head) {
                prev = temp;
                temp = temp->next;
            }
            prev->next = head;
            delete temp;
        }
        cout << "Data mahasiswa di belakang berhasil dihapus." << endl;
    }

    // Hapus data mahasiswa di tengah
    void hapusTengah(int posisi) {
        if (head == nullptr) {
            cout << "Linked List Kosong." << endl;
            return;
        }
        if (posisi <= 0) {
            cout << "Posisi harus lebih dari 0." << endl;
            return;
        }
        Mahasiswa* temp = head;
        Mahasiswa* prev = nullptr;
        int count = 1;
        while (count < posisi && temp->next != head) {
            prev = temp;
            temp = temp->next;
            count++;
        }
        if (count != posisi) {
            cout << "Posisi terlalu besar." << endl;
            return;
        }
        if (temp == head) {
            hapusDepan();
            return;
        }
        prev->next = temp->next;
        delete temp;
        cout << "Data mahasiswa di posisi " << posisi << " berhasil dihapus." << endl;
    }

    // Hapus semua data mahasiswa
    void hapusList() {
        if (head == nullptr) {
            cout << "Linked List Kosong" << endl;
            return;
        }
        Mahasiswa* current = head;
        Mahasiswa* next = nullptr;
        while (current->next != head) {
            next = current->next;
            delete current;
            current = next;
        }
        delete current;
        head = nullptr;
        cout << "Semua data mahasiswa berhasil dihapus." << endl;
    }

    // Menampilkan daftar mahasiswa
    void tampilkan() {
        if (head == nullptr) {
            cout << "Linked List Kosong." << endl;
            return;
        }
        Mahasiswa* temp = head;
        do {
            cout << "Nama: " << temp->nama << ", NIM: " << temp->nim << endl;
            temp = temp->next;
        } while (temp != head);
    }
};

int main() {
    LinkedListCircular list;
    int choice;
    string nama, nim;
    int posisi;

    do {
        cout << "------------------------------";
        cout << "\nLIST DATA DAN NIM MAHASISWA\n";
        cout << "------------------------------\n";
        cout << "Menu :\n";
        cout << "1. Tambah Depan\n";
        cout << "2. Tambah Belakang\n";
        cout << "3. Tambah Tengah\n";
        cout << "4. Ubah Depan\n";
        cout << "5. Ubah Belakang\n";
        cout << "6. Ubah Tengah\n";
        cout << "7. Hapus Depan\n";
        cout << "8. Hapus Belakang\n";
        cout << "9. Hapus Tengah\n";
        cout << "10. Hapus List\n";
        cout << "11. Tampilkan Data\n";
        cout << "0. Keluar\n";
        cout << "Pilih Operasi: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Masukkan Nama: ";
                cin >> nama;
                cout << "Masukkan NIM: ";
                cin >> nim;
                list.tambahDepan(nama, nim);
                break;
            case 2:
                cout << "Masukkan Nama: ";
                cin >> nama;
                cout << "Masukkan NIM: ";
                cin >> nim;
                list.tambahBelakang(nama, nim);
                break;
            case 3:
                cout << "Masukkan Nama: ";
                cin >> nama;
                cout << "Masukkan NIM: ";
                cin >> nim;
                cout << "Masukkan Posisi: ";
                cin >> posisi;
                list.tambahTengah(nama, nim, posisi);
                break;
            case 4:
                cout << "Masukkan Nama: ";
                cin >> nama;
                cout << "Masukkan NIM: ";
                cin >> nim;
                list.ubahDepan(nama, nim);
                break;
            case 5:
                cout << "Masukkan Nama: ";
                cin >> nama;
                cout << "Masukkan NIM: ";
                cin >> nim;
                list.ubahBelakang(nama, nim);
                break;
            case 6:
                cout << "Masukkan Nama: ";
                cin >> nama;
                cout << "Masukkan NIM: ";
                cin >> nim;
                cout << "Masukkan Posisi: ";
                cin >> posisi;
                list.ubahTengah(nama, nim, posisi);
                break;
            case 7:
                list.hapusDepan();
                break;
            case 8:
                list.hapusBelakang();
                break;
            case 9:
                cout << "Masukkan Posisi: ";
                cin >> posisi;
                list.hapusTengah(posisi);
                break;
            case 10:
                list.hapusList();
                break;
            case 11:
                list.tampilkan();
                break;
            case 0:
                cout << "Terima kasih:)" << endl;
                break;
            default:
                cout << "Maaf, pilihan tidak valid." << endl;
                break;
        }
    } while (choice != 0);

    return 0;
}
```

#### Output:

#### Tampilan Awal
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/aec1d1b0-d67e-4609-8f80-fd43f9261268)

#### Tampilan Operasi Tambah
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/37adaa75-f997-4ec7-b101-f85c5c5fefe9)
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/b479be0b-7d50-493d-9aa8-cf2cfbaaea81)

#### Tampilan Operasi Hapus
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/012eae15-ca1b-4dfc-b7a9-4e369f61fb7e)
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/fad6f5fc-575e-4a38-939b-623663dff487)


#### Tampilan Operasi Ubah
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/ea07f53f-8805-4553-a6c1-52896a981748)
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/5a78150d-1f10-48e4-8bbc-2cffab9499a3)

#### Tampilan Operasi Tampil Data
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/527a59b8-a99e-488d-8e22-c992880f59b5)


### 2. Setelah membuat menu tersebut, masukkan data sesuai urutan berikut, lalu tampilkan data yang telah dimasukkan. (Gunakan insert depan, belakang atau tengah)
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/a6d49339-9fc5-4b0e-9973-6af3942ea430)

### 3. Lakukan perintah berikut:

#### a) Tambah data Wati 2330004 diantara Farrel dan Denis
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/48eea846-5cc6-45c2-b11d-dc87df8cf730)

#### b) Hapus data Denis
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/b9c10c98-631e-48b7-810e-91b30aea7a44)

#### c) Tambahkan data berikut di awal: Owi 2330000
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/df61b542-8f7f-46f7-bd43-2ee82688746e)

#### d) Tambahkan data berikut di akhir: David 23300100
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/dc0e933a-172a-4f3e-b417-143109833ab3)

#### e) Ubah data Udin menjadi data berikut: Idin 23300045
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/b14055cf-23e9-43c5-907c-fd3bc1acc79e)

#### f) Ubah data terkahir menjadi berikut: Lucy 23300101
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/87136d96-0d40-45ac-b483-2c4ee4fdbc05)

#### g) Hapus data awal
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/417c1554-2f99-4a90-938b-1f93ae9f7987)

#### h) Ubah data awal menjadi berikut: Bagas 2330002
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/d82892fb-cd90-40d5-aea0-b2c9faa5491b)

#### i) Hapus data akhir
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/cd1d1df7-6ad0-4980-8ca2-113d01509791)

#### j) Tampilkan seluruh data
![image](https://github.com/NarayaAlfan19/Struktur-Data-Assigment/assets/162522372/8f5f17ba-6467-4306-a849-405893aa24f5)

Program di atas merupakan implementasi dari linked list circular. Kelas *LinkedListCircular* memiliki beberapa fungsi untuk operasi-operasi dasar pada linked list, seperti menambah, mengubah, dan menghapus data mahasiswa, serta menampilkan seluruh data mahasiswa. Setiap operasi tersebut dapat dilakukan di depan, di belakang, atau di tengah linked list.
Di dalam *main()*, program menyediakan menu untuk pengguna agar dapat memilih operasi yang ingin dilakukan, seperti menambah, mengubah, atau menghapus data mahasiswa, serta menampilkan seluruh data mahasiswa. Pengguna dapat memilih menu sesuai kebutuhan, dan program akan menjalankan operasi yang dipilih. Selama program berjalan, data mahasiswa disimpan dalam linked list circular, yang artinya elemen terakhir terhubung kembali ke elemen pertama, membentuk lingkaran. Hal ini memungkinkan untuk melakukan traversing dari awal ke akhir linked list secara terus menerus.

## Kesimpulan
Linked list circular melingkar adalah varian dari struktur data linked list yang memiliki sifat khusus di mana elemen terakhir terhubung kembali ke elemen pertama, membentuk sebuah lingkaran. Hal ini berbeda dengan linked list biasa yang memiliki elemen terakhir yang menunjuk ke NULL. Linked list circular memiliki keunggulan utama yaitu kemampuannya untuk melakukan traversing dari awal ke akhir linked list secara terus menerus tanpa harus kembali ke elemen pertama. Hal ini memungkinkan pengolahan data yang lebih efisien dalam beberapa kasus penggunaan, terutama ketika diperlukan akses berulang terhadap seluruh elemen dalam linked list. Linked list circular juga memiliki kemiripan dengan linked list ganda (double linked list) dalam hal sifat melingkar. Namun, linked list circular hanya memiliki satu pointer next untuk setiap elemen, sementara linked list ganda memiliki dua pointer (next dan prev) yang menghubungkan setiap elemen dengan elemen sebelum dan sesudahnya. Meskipun demikian, linked list circular juga memiliki kelemahan, seperti kompleksitas dalam penanganan kasus khusus, seperti menemukan elemen terakhir atau melakukan operasi pada elemen terakhir. Selain itu, kesalahan dalam implementasi operasi tambah dan hapus elemen dapat mengakibatkan terjadinya looping tak terbatas. Dengan demikian, penggunaan linked list circular melingkar harus dipertimbangkan dengan cermat sesuai dengan kebutuhan aplikasi dan karakteristik data yang diolah. Kelebihan dan kelemahan dari struktur data ini perlu dipahami dengan baik agar dapat memanfaatkannya secara efektif dalam pengembangan perangkat lunak.

## Referensi
[1] "Pengantar Daftar Tertaut Melingkar" GeeksforGeeks, 2023.
https://www.geeksforgeeks.org/circular-linked-list/

[2] "Struktur Data Linked List: Pengertian, Karakteristik, dan Jenis-jenisnya" Trivusi. 2022
https://www.trivusi.web.id/2022/07/struktur-data-linked-list.html
