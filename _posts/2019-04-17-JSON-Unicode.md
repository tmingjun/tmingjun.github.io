---
title: "JSON支持Unicode"
athor: xiaotan
data: 2019-04-17
layout: post
description: "为了让自己的JSON库可以识别utf-8编码，然后添加JSON支持Unicode，主要记录了JSON库的学习过程。"
tag: JSON
---

 >为了让自己的JSON库可以识别utf-8编码，然后添加JSON支持Unicode，主要记录了JSON库的学习过程,方便以后进行查阅，算是知识累积的一种方法吧。


主要学习内容：
1. [Unicode相关知识](##1.-Unicode-相关知识)
2. [utf-8相关知识](##2.-utf-8-相关知识)

## 1. Unicode 相关知识

Unicode 是一套多语言的统一**编码系统**，收录 135 种语言共 128237 个字符，这些字符被收录为统一的字符集（Universal Coded Character Set, UCS）,每个字符被映射为一个整数码点，码点的范围是 **0-10FFFF** ，码点又通常记作 **U+XXXX**，当中 XXXX 为 16 进位数字。

由于 Unicode 无法想 ASSIC 码这样以一个字节存储，因此 Unicode 制定了各种存储码点的方式，这种方式称为 Unicode 转换格式（Uniform Transformation Format, UTF）。现时流行的 UTF 为 UTF-8、UTF-16 和 UTF-32。每种 UTF 会把一个码点储存为一至多个编码单元（code unit）。例如 UTF-8 的编码单元是 8 位的字节、UTF-16 为 16 位、UTF-32 为 32 位。除 UTF-32 外，UTF-8 和 UTF-16 都是可变长度编码。


## 2. utf-8 相关知识

### urf-8 的优势

1. 它采用字节为编码单元，不会有字节序（endianness）的问题。
2. 每个 ASCII 字符只需一个字节去储存。
3. 如果程序原来是以字节方式储存字符，理论上不需要特别改动就能处理 UTF-8 的数据。

### UTF-8 的编码方式

UTF-8 的编码单元为 8 位（1 字节），每个码点编码成 1 至 4 个字节。它的编码方式很简单，按照码点的范围，把码点的二进位分拆成 1 至最多 4 个字节：

| 码点范围            | 码点位数  | 字节1     | 字节2    | 字节3    | 字节4     |
|:------------------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| U+0000 ~ U+007F    | 7        | 0xxxxxxx |
| U+0080 ~ U+07FF    | 11       | 110xxxxx | 10xxxxxx |
| U+0800 ~ U+FFFF    | 16       | 1110xxxx | 10xxxxxx | 10xxxxxx |
| U+10000 ~ U+10FFFF | 21       | 11110xxx | 10xxxxxx | 10xxxxxx | 10xxxxxx |

这个编码方法的好处之一是，码点范围 U+0000 ~ U+007F 编码为一个字节，与 ASCII 编码兼容。这范围的 Unicode 码点也是和 ASCII 字符相同的。因此，一个 ASCII 文本也是一个 UTF-8 文本

### 代码实现

解析多字符C语言代码:

~~~c
if (u >= 0x0800 && u <= 0xFFFF) {
    OutputByte(0xE0 | ((u >> 12) & 0xFF)); /* 0xE0 = 11100000 */
    OutputByte(0x80 | ((u >>  6) & 0x3F)); /* 0x80 = 10000000 */
    OutputByte(0x80 | ( u        & 0x3F)); /* 0x3F = 00111111 */
}
~~~