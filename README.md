# Tugas OAK (Perulangan)

```assembly
section .bss
    char resb 1

section .text
    global _start

_start:
    mov esi, 1

print_loop:
    cmp esi, 10
    jge exit

    mov eax, esi
    add eax, '0'
    mov [char], al

    mov eax, 4
    mov ebx, 1
    mov ecx, char
    mov edx, 1
    int 0x80

    inc esi
    jmp print_loop

exit:
    mov eax, 1
    xor ebx, ebx
    int 0x80
```

## **Menjalankan Program**
![Screenshot 2025-04-14 151025](https://github.com/user-attachments/assets/5291e708-d705-41ce-9b85-491db0c0c3f4)

## **Penjelasan Analisis Kode**
![Screenshot 2025-04-14 152009](https://github.com/user-attachments/assets/6e58e395-fba6-440b-8269-ef2a2af89b86)
- bss adalah section untuk deklarasi variabel tak terinisialisasi.
- char resb 1 artinya: cadangkan 1 byte dengan nama char. Ini digunakan nanti untuk menyimpan satu karakter angka yang akan ditampilkan.
  
![Screenshot 2025-04-14 152020](https://github.com/user-attachments/assets/c42fba2f-6403-47e2-8d28-c1f9eeaf6651)
- .text adalah section untuk kode program (instruksi).

- global _start memberi tahu linker bahwa titik masuk program dimulai dari label _start.

![Screenshot 2025-04-14 152029](https://github.com/user-attachments/assets/e22b48fb-1af2-4291-9e95-fabac72941ce)
- Memulai eksekusi program.

- mov esi, 1: isi register ESI dengan angka 1. Register ESI akan digunakan sebagai counter angka dari 1 sampai 9.


![Screenshot 2025-04-14 152048](https://github.com/user-attachments/assets/f7299978-fefe-4193-9587-51a0eecb2369)
- Cek apakah esi >= 10. Jika ya, lompat ke exit.

- Ini artinya: selama esi < 10, kita akan mencetak angka.


![Screenshot 2025-04-14 152201](https://github.com/user-attachments/assets/f7f42591-6021-474b-a481-f0fba826caed)
- Salin isi esi ke eax.

- add eax, '0' → Menambahkan nilai ASCII dari karakter '0' (yaitu 48 desimal).
    Misalnya, esi = 1, maka eax = 1 + 48 = 49, yaitu ASCII dari '1'.

- mov [char], al → simpan byte rendah dari eax (yaitu karakter angka) ke variabel char.
  
![Screenshot 2025-04-14 152221](https://github.com/user-attachments/assets/c1e92649-adf6-4163-899e-58debbfac4ac)

Ini bagian penting: menggunakan int 0x80 untuk melakukan system call write.
- eax = 4 → kode system call write.

- ebx = 1 → file descriptor 1 (stdout / layar).

- ecx = char → alamat karakter yang ingin ditulis.

- edx = 1 → hanya 1 byte yang ditulis.
  
![Screenshot 2025-04-14 152233](https://github.com/user-attachments/assets/94d3a6e2-8e92-4957-bc7a-1796e56b38a6)
- inc esi → tambahkan 1 ke counter (esi).

- jmp print_loop → ulangi perulangan.


![Screenshot 2025-04-14 152240](https://github.com/user-attachments/assets/155ae03a-f29f-488f-a16a-c31c387ff662)
- eax = 1 → kode system call exit.

- xor ebx, ebx → set ebx = 0 (exit code 0).

- int 0x80 → keluar dari program.


