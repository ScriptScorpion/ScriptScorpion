Команды в ASM:

NOP Ничего не делает 

INT Вызов прерывания INT 0x80 (вызов ядра Linux)

HLT Остановка процессора

SYSCALL Быстрый вызов ядра (в современных ОС)

PUSH Кладёт значение в стек (уменьшает ESP) 

POP Забирает значение из стека (увеличивает ESP) 

CALL Вызов функции (кладёт адрес возврата в стек)

RET Возврат из функции (берёт адрес из стека и прыгает)

JMP Безусловный переход JMP label (переход на метку)

JE/JZ Переход, если равно, если ZF=1 

JNE/JNZ Переход, если НЕ равно, если ZF=0 

JG Переход, если больше (знаковый)

JA Переход, если больше (беззнаковый) 

JL Переход, если меньше (знаковый) 

JB Переход, если меньше (беззнаковый) 

CMP Сравнение (вычитает, но не сохраняет результат, только флаги)

TEST Логическое И (без сохранения, только флаги)

AND Побитовое И, AND eax, 0xFF (оставляет младший байт)

OR Побитовое ИЛИ, OR eax, 0x80 (устанавливает старший бит, подробное обеяснение: true if a==1 or b==1 or both==1)

XOR Побитовое исключающее ИЛИ, XOR eax, eax (обнуляет eax, подробное обьяснение: true if a==1 or b==1 but not both == 1)

NOT Побитовое НЕ, NOT eax (инвертирует все биты eax)

SHL Сдвиг влево (работает одинаково для знаковых и беззнаковых, аналог << в C)

SHR Сдвиг вправо (беззнаковый, >> в C)

SAR Арифметический сдвиг вправо (знаковый, сохраняет знак)

ADD Сложение         ADD eax, 5 (eax += 5)

SUB Вычитание          SUB ebx, 10 (ebx -= 10)

INC      Увеличить на 1  INC ecx (ecx++)

DEC Уменьшить на 1  DEC edx (edx--)

MUL Умножение (безнаковое, не может быть отрицательным)

IMUL Умножение (знаковое, может быть отрицательным)

DIV        Деление (беззнаковое, не может быть отрицательным)

IDIV  Деление (знаковое, может быть отрицательным)

MOV Копирует данные (регистр регистр, регистр память, но не память память!) mov destination, source

LEA Загружает адрес (аналог & в C), LEA eax, [ebx+4] (eax = адрес ebx+4)

XCHG Меняет местами два значения, XCHG eax, ebx (теперь eax = старое ebx, и наоборот)

$ - в NASM означает позицию начала текущей строки кода

$$ - в NASM означает позицию начала текущей секции 

Типы переменных(NASM):

db - define byte (8 бит)

dw - define word (16 бит)

dd - define double word (32 бита)

dq - define quad word (64 бита)

Для массивов (во сновном используються для хранилищя ввода, по типу `auto arr[размер]` 'auto' - в этом выражении символизирует что тип который могут хранить массив в ассемблере определяеться автоматически):

resb - reserve byte (8 нулей если указать resb 1)

resw -  reserve word (16 нулей если указать resw 1)

resd -  reserve double word (32 нулей если указать resd 1)

resq -  reserve quad word (64 нулей если указать resq 1)

Типы переменных(GAS):

.byte 1 байт

.word 2 байта

.long 4 байта

.quad 8 байт

.ascii    строка ASCII

GAS Documentation: https://en.wikibooks.org/wiki/X86_Assembly/GNU_assembly_syntax

NASM Documentation: https://en.wikibooks.org/wiki/X86_Assembly/NASM_Syntax

Регистры в Assembler:

pdf: https://liujunming.top/pdf/syscall/Linux%20System%20Call%20Table%20for%20x86%2064%20·%20Ryan%20A.%20Chapman.pdf
website: https://hackeradam.com/x86-64-linux-syscalls/

в ассемблер после вызова функции или после прочтение и тд. значение по умолчание записываеться в rax.

в GDB чтобы узнать значение переменной в Assembler:
```
# Вывести как строку
print (char*)&(переменная)

# Вывести как целое число (если переменная числовая)
print (int)&(переменная)
```

https://en.wikipedia.org/wiki/Bitwise_operations_in_C

В nasm использование [] значит переместить адресс указанный в скобках куда то, но надо ещё указать размер адреса, иногда размер указывать не надо, например когда переносим значение из памяти в регистр

лучшая комбинация для Дисассемблирования файла используя objdump: `objdump -d --visualize-jumps -M intel файл`

лучшая комбинация для изменения файла используя hexedit + hexdump: `hexdump -C файл | grep "текст"` и `hexedit файл` и нажимаешь CTRL + G и вводишь адресс строки с hexdump который показан в самом левом углу(без нулей)

# x64 NASM cheat sheet

## Registers

|                         | 64 bit | 32 bit | 16 bit | 8 bit |
|-------------------------|--------|--------|--------|-------|
| A (accumulator)         | `RAX`  | `EAX`  | `AX`   | `AL`  |
| B (base, addressing)    | `RBX`  | `EBX`  | `BX`   | `BL`  |
| C (counter, iterations) | `RCX`  | `ECX`  | `CX`   | `CL`  |
| D (data)                | `RDX`  | `EDX`  | `DX`   | `DL`  |
|                         | `RDI`  | `EDI`  | `DI`   | `DIL` |
|                         | `RSI`  | `ESI`  | `SI`   | `SIL` |
| Numbered (n=8..15)      | `Rn`   | `RnD`  | `RnW`  | `RnB` |
| Stack pointer           | `RSP`  | `ESP`  | `SP`   | `SPL` |
| Frame pointer           | `RBP`  | `EBP`  | `BP`   | `BPL` |

As well as XMM0 .. XMM15 for 128 bit floating point numbers.


## Calling C

Put function arguments (first to last) in the following registers (64 bit
representations): RDI, RSI, RDX, RCX, R8, R9, then push to stack (in reverse,
has to be cleaned up by the caller!) XMM0 - XMM7 for floats

Return values are stored in RAX (`int`) or XMM0 (`float`)

RBP, RBX, R12, R13, R14, R15 will not be changed by the called function, all
others may be

Align stack pointer (RSP) to 16 byte, calling pushes 8 bytes!

Keep in mind that strings (in C) are 0-terminated

Like in a normal C program, the label that is called first is
`main`, with the args `argc` in RDI, and the `char** argv` in RSI
(the commandline arguments as in C's main function).


## Data

| Definition size    | Definition instruction |
|--------------------|------------------------|
| 8 bit              | `db`                   |
| 16 bit             | `dw`                   |
| 32 bit             | `dd`                   |
| 64 bit             | `ddq`/`do`             |
| float              | `dd`                   |
| double             | `dq`                   |
| extended precision | `dt`                   |


Many suffixes, including:

- `a` (above, >)
- `ae` (above or equal, >=)
- `b` (below, <)
- `be` (below or equal, <=)
- `e` (equal, =)
- `ne` (not equal, !=)


## Program structure

- `global <entry>` -> exposes entry point
- `extern <function>` -> declares a function in another linked .o file (e.g. C
  function, other asm file)
- `section <sectiontype>` -> sets section, usually:
  - `.text` -> program code
  - `.data` -> data

The program entry point of a standalone program is the label `_start`.  When
compiled with gcc, C provides `_start`, which inits and then jumps to `main`,
which should then be implemented by the program.


## Syscalls

- put syscall number in EAX (e.g. on Linux: 60 for exit, 1 for write to stdout)
- put arguments in the registers (see above) like when calling a C function
- execute the `syscall` instruction

