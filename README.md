# JStruct
The python struct library's port to java for reading and writing binary data as in python

## Classes
The file Struct.java defines a single class named struct. Due to the dependability on hardware
and the information of system's byte order is needed. So, it have to be initialized first like:
  Struct struct = new Struct();

this will correctly initialize the library and set everything up for it's use

## USAGE:
To use this, either add a jar dependancy or use the class as is in your file. For possible namespace conflicts
compiling to a jar dependancy is preferred. In that case, kindly use com.quora.weirduniverse.JStruct as package name.
( http://weirduniverse.quora.com happens to be my quora blog -- I love writing on quora )

Due to the typed nature of Java (and trust me, the lack-of-unsignedness hurts the most)
we always deal in longs, and as such unsigned long long (128bit) integers will never be a part of this lib
Though I am thinking of a fork of this which communicates in BigIntegers, since, 128bit ints are rarely used (well, by me at least)
I am working on this over longs, since they process much faster ( I know, I know, don't tell the Knuth's line to me over and over again, but this shit
is pretty low level, so, optimizations does matter *java is not python* )

First, Initialize, by Struct struct = new Struct();
then, the following functions are available

__pack(String fmt, long val)__ : Returns a byte[] (bytearray) of the single value packed accordingly, do note though, currently, no error is thrown if the value is out of range, because, the value is always truncated by a `0xffff...` as needed. Outer bytes are simply ignored. This behavior may change, depends on the support though

__pack(String fmt, long[] vals)__ : Returns a flattenned byte[] (bytearray) of the data. i.e. if it is used like struct.pack("HI", {26952, 1635148106}).toString("UTF-8") will result into "HiJava"

__unpack(String fmt, byte[] vals)__ : Returns a long[] that will hold the appropriate number of values parsed from the vals. vals is a flattenned bytearray,
therefore the length of vals must be equal to the expected length, else it will throw an Exception (I don't know what would be the appropriate Exception, I get confused, an edit here might help :) ) Do note that, it will always be an array even if you are parsing a single value, accessing the 0th index will help.

## Accepted specifiers:
  The first char can be a endianness indicator, the following are available
  * @ : Default endianness (since in java, native and standard are meaningless, so used it as default endianness and no =)
  * < : Little Endian
  * > : Big Endian
  * ! : Network byte order, same as >

  Apart from them the following code specifiers are supported in this version:
  * h : 2's complement Signed Short (2 bytes) 
  * H : Unsigned Short (2 bytes)
  * i : 2's complemen  Signed int (4 bytes)
  * I : Unsigned int (4 bytes)

I will update if people are interested, else, this much suffices my personal interest, updates will be done if I ever need more features.

Finally, Python rocks, I am learning Java for filling up my resume only. And probably for the mantra, "learning never hurts"
(I know, there is no such mantra, and learning always hurt, but you see, you gotta look cool if you have to impress bosses (or teachers))
