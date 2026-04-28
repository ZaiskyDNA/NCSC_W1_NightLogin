# Write-up: ASCII Numbers (PicoCTF)

## Deskripsi
> Convert the following string of ASCII numbers into a readable string:
> 
`0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x34 0x35 0x63 0x31 0x31 0x5f 0x6e 0x30 0x5f 0x71 0x75 0x33 0x35 0x37 0x31 0x30 0x6e 0x35 0x5f 0x31 0x6c 0x6c 0x5f 0x74 0x33 0x31 0x31 0x5f 0x79 0x33 0x5f 0x6e 0x30 0x5f 0x6c 0x31 0x33 0x35 0x5f 0x34 0x34 0x35 0x64 0x34 0x31 0x38 0x30 0x7d`

## Penyelesaian
Tantangan ini merupakan dasar dari kriptografi (*basic crypto*). Perhatikan bahwa setiap angka memiliki awalan `0x`, yang merupakan penanda untuk bilangan **Hexadecimal**. Oleh karena itu, kita hanya perlu mengonversi deretan Hex tersebut menjadi teks ASCII yang dapat dibaca.

**Langkah-langkah:**
1. Salin deretan angka Hexadecimal pada soal.
2. Gunakan *tool online* seperti [CyberChef](https://gchq.github.io/CyberChef/) (sangat direkomendasikan dan populer untuk CTF).
3. Masukkan deretan angka tersebut ke kolom *Input*.
4. Gunakan *recipe* **From Hex**.
5. *Flag* akan langsung muncul di kolom *Output*. 

Meskipun di platform tertulis sebagai tantangan tingkat medium, cara penyelesaiannya sebenarnya sangat mudah.

## Flag
`picoCTF{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_445d4180}`