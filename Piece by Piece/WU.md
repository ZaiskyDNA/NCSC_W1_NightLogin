# Write-up: Piece by Piece (PicoCTF)

## Deskripsi Tantangan
**Description:**
> After logging in, you will find multiple file parts in your home directory. 
> These parts need to be combined and extracted to reveal the flag.
> Additional details will be available after launching your challenge instance.

Ini merupakan salah satu tantangan dari **PicoCTF**. Saat kita menjalankan (*launch*) instance-nya, kita mendapatkan akses server berikut: 
`SSH to dolphin-cove.picoctf.net:57352 and login as ctf-player with password a15d25e1.`

Artinya, kita perlu melakukan login SSH melalui terminal ke alamat yang tertera.

## Langkah Penyelesaian

### 1. Login ke Server Target
Jalankan perintah berikut di terminal:

```bash
ssh ctf-player@dolphin-cove.picoctf.net -p 57352
```

**Penjelasan Perintah:**
- `ctf-player` : *Username* yang digunakan untuk login.
- `@dolphin-cove.picoctf.net` : Alamat *network* / server target.
- `-p 57352` : Menentukan *port* spesifik yang digunakan untuk koneksi.

Setelah itu, masukkan password `a15d25e1` untuk berhasil masuk ke dalam server.

### 2. Memeriksa Isi Direktori
Setelah masuk, kita akan melihat apa saja yang ada di server menggunakan perintah `ls -la`.

```bash
ctf-player@pico-chall$ ls -la
total 28
drwxr-xr-x 1 ctf-player ctf-player  20 Apr 28 04:27 .
drwxr-xr-x 1 root       root        24 Feb  4 22:40 ..
drwx------ 2 ctf-player ctf-player  34 Apr 28 04:27 .cache
-rw-r--r-- 1 root       root        67 Feb  4 22:40 .profile
-rw-r--r-- 1 ctf-player ctf-player 282 Feb  4 21:22 instructions.txt
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_aa
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_ab
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_ac
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_ad
-rw-r--r-- 1 ctf-player ctf-player  35 Feb  4 22:40 part_ae
```
Di situ terlihat ada file `instructions.txt` dan beberapa pecahan file (`part_aa` sampai `part_ae`).

### 3. Membaca Instruksi
Kita baca isi `instructions.txt` terlebih dahulu:

```bash
ctf-player@pico-chall$ cat instructions.txt 
Hint:
- The flag is split into multiple parts as a zipped file.
- Use Linux commands to combine the parts into one file.
- The zip file is password protected. Use this "supersecret" password to extract the zip file.
- After unzipping, check the extracted text file for the flag.
```
**Inti instruksi:** Ada beberapa file yang harus kita gabung menjadi satu file zip, lalu kita ekstrak (*unzip*) dengan password `supersecret` yang sudah diberikan.

### 4. Menggabungkan Pecahan File
Kita bisa menggabungkannya menggunakan perintah `cat` dan menyalurkannya (`>>`) ke dalam satu file baru bernama `gabungan.zip` seperti panduan di bawah ini:

```bash
ctf-player@pico-chall$ cat part_aa part_ab part_ac part_ad part_ae >> gabungan.zip
```

Jika kita cek lagi dengan `ls -la`, file `gabungan.zip` berhasil dibuat:

```bash
ctf-player@pico-chall$ ls -la
total 32
drwxr-xr-x 1 ctf-player ctf-player  40 Apr 28 04:30 .
drwxr-xr-x 1 root       root        24 Feb  4 22:40 ..
drwx------ 2 ctf-player ctf-player  34 Apr 28 04:27 .cache
-rw-r--r-- 1 root       root        67 Feb  4 22:40 .profile
-rw-rw-r-- 1 ctf-player ctf-player 239 Apr 28 04:30 gabungan.zip
-rw-r--r-- 1 ctf-player ctf-player 282 Feb  4 21:22 instructions.txt
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_aa
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_ab
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_ac
-rw-r--r-- 1 ctf-player ctf-player  51 Feb  4 22:40 part_ad
-rw-r--r-- 1 ctf-player ctf-player  35 Feb  4 22:40 part_ae
```

### 5. Ekstraksi dan Mendapatkan Flag
Kita langsung ekstrak (*unzip*) saja file gabungan tersebut. Saat diminta password, masukkan password yang ada di instruksi tadi (`supersecret`):

```bash
ctf-player@pico-chall$ unzip gabungan.zip 
Archive:  gabungan.zip
[gabungan.zip] flag.txt password: 
 extracting: flag.txt                
```

File `flag.txt` berhasil diekstrak. Terakhir, kita tinggal membaca isi file tersebut untuk mendapatkan *flag*-nya:

```bash
ctf-player@pico-chall$ cat flag.txt 
picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_da494d2e}
```

---
**Flag:** `picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_da494d2e}`