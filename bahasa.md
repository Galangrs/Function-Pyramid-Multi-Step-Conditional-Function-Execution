# Function Pyramid (Konsep Pemrograman)

## Gambaran Umum
**Function Pyramid** adalah pendekatan yang terstruktur untuk mengatur fungsi dan mengeksekusinya berdasarkan kondisi tertentu. Konsep ini dirancang untuk menyelesaikan masalah logika yang kompleks, di mana beberapa fungsi perlu dieksekusi dalam urutan tertentu, tergantung pada nilai atau hasil yang sudah ditentukan. Fungsi-fungsi tersebut dieksekusi **secara berurutan**, dan setiap fungsi dapat mengubah status atau nilai yang digunakan oleh fungsi berikutnya.

**Function Pyramid** membantu dalam mengelola alur eksekusi dalam skenario seperti validasi, algoritma pencarian, atau proses pengambilan keputusan yang kompleks, di mana fungsi-fungsi perlu bekerja bersama dalam urutan tertentu tanpa konflik.

---

## Keuntungan Utama
- **Eksekusi Bertingkat**: Fungsi dapat disusun atau dinesting, memungkinkan mereka untuk menyimpan dan memanipulasi status secara aman.
- **Logika Berdasarkan Kondisi**: Sistem ini memungkinkan eksekusi berdasarkan kondisi tertentu (misalnya, nilai atau hasil) secara terstruktur.
- **Penerapan Global**: Fungsi-fungsi ini dapat digunakan secara global dalam suatu sistem, memastikan tidak ada kesalahan logika atau konflik saat eksekusi.
- **Penggunaan Ulang**: Fungsi yang sama dapat digunakan kembali tanpa perlu duplikasi, selama kondisi yang dipenuhi sesuai.

---

## Kasus Penggunaan Utama
- **Eksekusi Fungsi Berdasarkan Kondisi**: Fungsi dieksekusi berdasarkan nilai kembali atau hasil tertentu.
- **Manajemen Status**: Fungsi dapat mempertahankan dan memperbarui status antara eksekusi.
- **Eksekusi Secara Berurutan**: Fungsi dieksekusi langkah demi langkah, memastikan bahwa setiap langkah hanya terjadi jika langkah sebelumnya memenuhi kondisi tertentu.

---

## Struktur Dasar Function Pyramid

### Pseudocode Logika:
Pseudocode berikut menggambarkan operasi dasar dari logika **Function Pyramid**.

```plaintext
UNTUK setiap fungsi dalam daftar fungsi:
    JIKA nilai kembali fungsi sama dengan nilai target:
        EKSEKUSI fungsi
```

---

## Implementasi Contoh

### 1. Contoh JavaScript
```javascript
const pyramid = [
    {
        func: async () => {
            console.log("Eksekusi fungsi dengan return 2");
        },
        return: 2
    },
    {
        func: async () => {
            console.log("Eksekusi fungsi dengan return 1");
        },
        return: 1
    }
];

const nilaiTarget = 2;

(async () => {
    for (let i = 0; i < pyramid.length; i++) {
        if (pyramid[i].return === nilaiTarget) {
            await pyramid[i].func();
        }
    }
})();
```

### 2. Contoh Lua
```lua
local pyramid = {
    {
        func = function()
            print("Eksekusi fungsi dengan return 2")
        end,
        result = 2
    },
    {
        func = function()
            print("Eksekusi fungsi dengan return 1")
        end,
        result = 1
    },
}

local nilai_target = 2

for i = 1, #pyramid do
    if pyramid[i].result == nilai_target then
        pyramid[i].func()
    end
end
```

### 3. Contoh Python
```python
pyramid = [
    {
        "func": lambda: print("Eksekusi fungsi dengan return 2"),
        "result": 2
    },
    {
        "func": lambda: print("Eksekusi fungsi dengan return 1"),
        "result": 1
    }
]

nilai_yang_dimau = 2

for item in pyramid:
    if item["result"] == nilai_yang_dimau:
        item["func"]()
```

---

## Contoh Lanjutan

Dalam contoh yang lebih lanjut, fungsi dapat memodifikasi hasil mereka sendiri dan mengeksekusi secara rekursif, memperbarui status hingga nilai target tercapai.

### JavaScript
```javascript
const pyramid = [
    {
        result: 1,
        async func(maxValue) {
            console.log(`Eksekusi fungsi 1, result = ${this.result}`);
            if (this.result < maxValue) {
                this.result += 1;
                await this.func(maxValue);
            }
        }
    },
    {
        result: 10,
        async func(maxValue) {
            console.log(`Eksekusi fungsi 2, result = ${this.result}`);
            if (this.result < maxValue) {
                this.result += 1;
                await this.func(maxValue);
            }
        }
    },
    {
        result: 3,
        async func(maxValue) {
            console.log(`Eksekusi fungsi 3, result = ${this.result}`);
            if (this.result < maxValue) {
                this.result += 1;
                await this.func(maxValue);
            }
        }
    }
];

const maxValue = 10;

(async function main() {
    for (let i = 0; i < pyramid.length; i++) {
        if (pyramid[i].result < maxValue) {
            await pyramid[i].func.call(pyramid[i], maxValue);
        }
    }

    console.log(
        `\nHasil akhir:\nFungsi 1: ${pyramid[0].result}, Fungsi 2: ${pyramid[1].result}, Fungsi 3: ${pyramid[2].result}`
    );
})();
```

### Lua
```lua
local pyramid = {
    [1] = {
        func = function(self, max_nilai)
            print("Eksekusi fungsi 1, result =", self.result)
            if self.result < max_nilai then
                self.result = self.result + 1
                self:func(max_nilai)
            end
        end,
        result = 1
    },
    [2] = {
        func = function(self, max_nilai)
            print("Eksekusi fungsi 2, result =", self.result)
            if self.result < max_nilai then
                self.result = self.result + 1
                self:func(max_nilai)
            end
        end,
        result = 10
    },
    [3] = {
        func = function(self, max_nilai)
            print("Eksekusi fungsi 3, result =", self.result)
            if self.result < max_nilai then
                self.result = self.result + 1
                self:func(max_nilai)
            end
        end,
        result = 3
    },
}

local max_nilai = 10

function main()
    for i = 1, #pyramid do
        if pyramid[i].result < max_nilai then
            pyramid[i]:func(max_nilai)
        end
    end
end

main()

print(pyramid[1].result, pyramid[2].result, pyramid[3].result)
```

### Python
```python
class PyramidFunction:
    def __init__(self, result):
        self.result = result

    def func(self, max_value):
        print(f"Eksekusi fungsi, result = {self.result}")
        if self.result < max_value:
            self.result += 1
            self.func(max_value)

pyramid = [
    PyramidFunction(1),
    PyramidFunction(10),
    PyramidFunction(3)
]

max_value = 10

def main():
    for pf in pyramid:
        if pf.result < max_value:
            pf.func(max_value)

main()

print("\nHasil akhir:")
for i, pf in enumerate(pyramid):
    print(f"Fungsi {i+1}: {pf.result}")
```

---

## Middleware Pipeline & Validasi Multi-Tahap

### Pola Middleware Pipeline
Selain **function pyramid**, **pola middleware pipeline** dapat digunakan di mana setiap langkah dalam proses bertindak sebagai middleware. Setiap fungsi mengubah konteks dan meneruskannya ke langkah berikutnya.

### Pseudocode untuk Middleware Pipeline:
1. Buat daftar fungsi middleware.
2. Setiap middleware mengubah konteks dan meneruskannya ke fungsi berikutnya.
3. Eksekusi semua fungsi middleware secara berurutan.

```plaintext
UNTUK setiap middleware dalam daftar middleware:
    UBAH konteks
    LANJUTKAN konteks ke middleware berikutnya
```

---

## Function Pyramid vs. Fungsi Biasa

### Function Pyramid:
1. **Eksekusi Secara Berurutan Berdasarkan Kondisi**: Fungsi dalam pyramid dieksekusi dalam urutan tertentu, masing-masing bergantung pada kondisi tertentu (misalnya, nilai yang cocok). Mereka dapat saling memanggil dan memperbarui statusnya dalam cara yang bersarang.
2. **Manajemen Status**: Setiap fungsi dapat mempertahankan statusnya dan memperbarui status tersebut, memungkinkan eksekusi yang lebih dinamis dan fleksibel.
3. **Kemampuan Rekursif**: Fungsi dapat memanggil dirinya sendiri secara rekursif untuk melanjutkan eksekusi hingga kondisi yang diinginkan tercapai.
4. **Penerapan Global**: Sistem memastikan bahwa setiap fungsi dalam pyramid bekerja bersama tanpa konflik atau kesalahan.

### Fungsi Biasa:
1. **Eksekusi Independen**: Fungsi biasanya dieksekusi secara independen, tanpa urutan yang dijamin kecuali didefinisikan secara eksplisit.
2. **Tanpa Manajemen Status Bawaan**: Fungsi biasa biasanya tidak mempertahankan atau meneruskan status kecuali secara eksplisit dibagikan melalui variabel atau objek.
3. **Tanpa Eksekusi Rekursif Otomatis atau Berdasarkan Kondisi**: Fungsi tidak secara otomatis menyesuaikan alur eksekusinya berdasarkan kondisi atau panggilan rekursif kecuali diprogram untuk melakukan hal tersebut.
4. **Konteks Terbatas**: Fungsi biasa mungkin tidak selalu memiliki akses ke status atau konteks fungsi lainnya kecuali diteruskan secara eksplisit.

---

## Kesimpulan
**Function Pyramid** adalah konsep yang kuat untuk mengelola eksekusi fungsi secara berurutan dalam skenario yang kompleks. Ini dapat digunakan untuk berbagai aplikasi seperti pemrosesan bersyarat, validasi bertingkat, dan pipeline middleware. Dengan menggabungkan pendekatan ini, pengembang dapat menangani alur kerja multi-tahap dan menjaga kode yang bersih dan mudah dikelola.
