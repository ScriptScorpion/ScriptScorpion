# Reverse Engineering:

1.Ghidra 

2.Hexedit or another one Hex editor

3.Radare2

# Network & Wireless Security:

1.Nmap

2.Wireshark

3.Aircrack-ng 

# Web Hacking:

1.Burp Suite Community

2.Sqlmap

3.Metasploit Framework

# Cryptography & Steganography:

1.Medusa

2.Hydra

3.John the Ripper

4.Steghide

# OSINT:

1.Sherlock 

2.TheHarvester

3.SpiderFoot


# RE3 configuration info:

## Radare2 commands:

start editing file: `r2 -nw ./файл` (n - means don't analyse, w - means load in write mode)

analysing some of functions: `aa`

analysing all functions and other things: `aaa`

write assembly code: `wa инструкции ассемблера` (you can do it also in 'Va' mode, just go to address of the line you want to change, and type `wa инструкции ассемблера` or `Va`. After you enter 'Va' mode, you can type Assembly instructions.)

write string: `w строка` (If you want to change string, i recommend doing this in `V` mode or use `hexedit`)

go to address: `s адрес`

print disassembly: `pd количество строк чтобы вывести`

print disassembly of one value at the address provided: `pd 1@адрес`

print all disassembly in current section: `pda`

print deep disassembly: `pA количество строк чтобы вести`

list all function: `afl`

list all Assembler sections: `iS` (look into 'vaddr' not 'paddr')

list Assembler defined variables and Assembler tags: `is`

name the function address: `afn имя hex-адрес-функции`

show value in different numeral systems + ASCII: `? значение`

enter visual mode(for editing hex values. Keybindings like in VIM): `V`

if you don't know what command does or wanna see all variants of the command, type '?' near command, example: `p?`


## my radare2 dotfile settings:

create `~/.radare2rc` file, and add this lines in file you created:

`e anal.vars=false`

`e bin.cache=true`
