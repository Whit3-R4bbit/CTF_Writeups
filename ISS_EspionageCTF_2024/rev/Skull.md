# Skull

In this challenge, we have another PE32 executable that we have to analyse to find the flag.

## Initial Investigation

As usual, we begin with running `strings` agaisnt the file to see if that will give us the flag.

    ┌──(ben㉿kali)-[~/CTFs/ISS_2023/rev]
    └─$ strings Skull         
    !This program cannot be run in DOS mode.
    }Rich
    .text
    `.rdata
    @.data
    .pdata
    @_RDATA
    @.rsrc
    @.reloc
    \$0H
    @USVWATAVAWH
    ...

Unfortunately, there's no flag to be found here. Time to dig deeper.

## Digging deeper

To analyse the executable further, ill be using the lighweight disassembler `Cutter`.

Taking a look at the main function, it doesnt seem very helpful.

    int main(int argc, char **argv, char **envp);
    ; var int cy @ stack - 0x408
    ; var UINT fuLoad @ stack - 0x400
    ; var const char *lpData @ stack - 0x3f8
    ; var HWND var_3f0h @ stack - 0x3f0
    ; var int64_t var_3e8h @ stack - 0x3e8
    ; var int64_t var_3e4h @ stack - 0x3e4
    ; var int64_t var_3e0h @ stack - 0x3e0
    ; var HANDLE var_3d8h @ stack - 0x3d8
    ; var int64_t var_3d0h @ stack - 0x3d0
    ; var int64_t var_3c0h @ stack - 0x3c0
    ; var int64_t var_3b0h @ stack - 0x3b0
    ; var int64_t var_3a0h @ stack - 0x3a0
    ; var int64_t var_390h @ stack - 0x390
    ; var int64_t var_380h @ stack - 0x380
    ; var int64_t var_370h @ stack - 0x370
    ; var int64_t var_360h @ stack - 0x360

Scrolling further down past this, we find something that looks interesting

    0x140002112      mov     dword [var_28h], 0x4c40467b ; '{F@L'
    0x14000211c      mov     dword [var_24h], 0x244e3043 ; 'C0N$'
    0x140002126      mov     dword [var_20h], 0x7221425f ; '_B!r'
    0x140002130      mov     word [var_1ch], 0x7d64 ; 'd}'

Now that looks like it could be a flag! If we concatenate the strings at the end of those lines, we get `{F@LC0N$_B!rd}`. If we prepend that with EspionageCTF we get the flag.

`flag:EspionageCTF{F@LC0N$_B!rd}`







