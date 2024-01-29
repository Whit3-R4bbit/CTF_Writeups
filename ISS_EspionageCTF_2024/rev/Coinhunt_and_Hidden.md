# Coinhunt and Hidden

In these 2 challenges, weve been given Windows PE32 executables and must find the flags contained within them. Ive combined these challenges as they have essentially the same solution.

## Investigation

As usual, I start by running the `strings` command on each file.


### Coinhunt

    ┌──(ben㉿kali)-[~/CTFs/ISS_2023/rev]
    └─$ strings CoinHunt 
    !This program cannot be run in DOS mode.
    7Rich
    UPX0
    UPX1
    ...(Ive deleted some of the irrelevant lines for brevity)
    .rsrc
    4.10
    bF~FFF
    'zEXE6E
    1/ |(_)'
    #Wrong Coin 
    t!C,U
    d_rY
    ~[Ggh
    Espi+ageCTF{$ilver@_C0In}~

And we got the flag (We know the flag wrapper is EspionageCTF{}, so we can replace the + with an "on")

`flag:EspionageCTF{$ilver@_C0In}`

### Hidden

    ┌──(ben㉿kali)-[~/CTFs/ISS_2023/rev]
    └─$ strings Hidden  
    !This program cannot be run in DOS mode.
    ...(Ive deleted lines for brevity again)
    XS6s
    4S=s
    SRich<s
    .text
    `.rdata
    bad allocation
    Unknown exception
    bad array new length
    To Mr.. 
    The advantage of becoming the first and greatest Intelligence is a must in this day and age. 
    I will allocate $1000 to allow you to pursue creating this department 
    I like forward to hearing from you in the coming years about your department progress! 
    Signed - PM
    EspionageCTF{CL@55iFed_C0nt$nt}

And we got another flag.

`flag:EspionageCTF{CL@55iFed_C0nt$nt}`

