# Mr. President

For this challenge, we are tasked with finding the name of an secret asset that is to be extracted. All we are given is a .wav audio file and and that we'll need a secret password that contains the word "Jupiter".

## Getting Started

Lets start by listening to the audio file....

Alright that didnt give us anything to go on, we'll have to work harder to get the secret

As usual, I like to start by running the `strings` command on non-human readable files, incase there is any plain text in the file data

    ┌──(ben㉿kali)-[~/CTFs/ISS_2023/forensics]
    └─$ strings main.wav     
    RIFFF
    WAVEfmt 
    LIST
    INFOISFT
    Lavf57.27.100
    data
    Ov'x%
    0wQW
    n<Mjz
    '~we
    ,4acLQ
    eY14\
    iVr%
    D'5F
    gTAp
    \gI,
    \BDs
    %~FA3m
    Lk3h
    #'x&
    9qP5
    C["`K$
    5K$s
    7uGH
    evXo
    +c!d
    B=>oz
    k>M)|
    @^A]
    Jk?nGar
            'E9A
    Lwf@!v9
    Jupiter_Missle

Look at that! we found a string that contains "Jupiter", thats gotta be the password. Unfortunately, we still dont have the name of the asset. We'll have to dig deeper.

## Digging Deeper

In CTF challenges where youre only given a media file (jpg, png, bmp, wav), its always good to check if data has been hidden in them through **steganography**. Steganography is a method of hiding data within other files by replacing unimportant bytes in a media file with bytes from the secret someone is trying to hide. Luckily there are many tools that we can use to try an extract the secret data, if it exists in the .wav

The steganography tool `steghide` supports the .wav format, so lets give it a try.

    ──(ben㉿kali)-[~/CTFs/ISS_2023/forensics]
    └─$ steghide extract -sf main.wav
    Enter passphrase:

Steghide is asking us for a password, so lets try that Jupiter_Missle string we found earlier

    ┌──(ben㉿kali)-[~/CTFs/ISS_2023/forensics]
    └─$ steghide extract -sf main.wav
    Enter passphrase: 
    wrote extracted data to "message.txt".

And it works! steghide extracted a hidden text file named `message.txt`. Now lets see whats in it

    ===================================
            ***** Confidential *****
    ===================================
    Hello Agent Null, We are letting you know that you must extract Dr. Billy Joe from CUBA.
    He has important information that will help us determine where certain missle silos are located.
    ===================================
            ***** Confidential *****
    ===================================

Now we got the name - Dr. Billy Joe, lets submit the flag.

    flag:EspionageCTF{BillyJoe}


