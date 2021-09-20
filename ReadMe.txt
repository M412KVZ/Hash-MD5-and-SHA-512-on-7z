WinCryptHashers

http://www.tc4shell.com/en/7zip/wincrypthashers/
Copyright (C) 2016-2017 Dec Software.

WinCryptHashers is a small plugin for the popular 7-Zip archiver. The plugin
enables 7-Zip to display the hash values produced by additional hashing
algorithms like MD5. WinCryptHashers also enables 7-Zip to generate text files
with checksums.

The plugin can add support for the following hashing algorithms:

 - MD2
 - MD4
 - MD5
 - SHA-384
 - SHA-512

Important! SHA-384 and SHA-512 may be unavailable in Windows XP unless the
Service Packs have been installed.

You can also install the ViPNet CSP cryptographic provider to add support for
the following hashing algorithms:

 - GOST R 34.11-94
 - GOST 34.11-2012 256
 - GOST 34.11-2012 512

You can download the ViPNet CSP cryptographic provider from the official page at
infotecs.ru (the website currently has only the Russian version):
http://infotecs.ru/downloads/besplatnye-produkty/

INSTALLATION

To install the plugin into the 7-Zip installation folder, you need to create the
"Codecs" subfolder. After that, copy WinCryptHashers.64.dll or
WinCryptHashers.32.dll (depending on your 7-Zip edition) and WinCryptHashers.ini
to that subfolder. If you do that, each time you launch 7-Zip, it will
automatically find the WinCryptHashers plugin and use it when displaying
checksums.

CONFIGURATION

WinCryptHashers.ini is a plain-text file that allows you to configure the
plugin. If you open the file, you will see something like this:

[Main]
MD2=0
MD4=0
MD5=1

SHA-1=0
SHA-256=0
SHA-384=0
SHA-512=0

; ViPNet CSP 4.2
GOST R 34.11-94=0
GOST 34.11-2012 256=0
GOST 34.11-2012 512=0

[Create]
MD5=md5:%HASH% *%FILENAME%
;SHA-256=sha256:%HASH% *%FILENAME%
;SHA-384=sha354:%HASH% *%FILENAME%
;SHA-512=sha512:%HASH% *%FILENAME%

;CRC32=sfv:%FILENAME% %HASH%
;CRC64=crc64:%HASH% *%FILENAME%
;BLAKE2sp=blake2sp:%HASH% *%FILENAME%

The Main section defines additional checksum algorithms. Each "0" value means
means that 7-Zip will not use the hashing algorithm, and each "1" value means
that 7-Zip will use it.

Important! Enabling the additional hashing algorithms will increase the total
time required for calculating the checksums. So we recommend that you enable
only the algorithms that you actually need.

The Create section defines algorithms that can be used to generate text files
with checksums. The algorithm list in this section is independent of the list in
the Main section. Use the following format when specifying the parameters:

NAME=ext:mask

Here "NAME" is the name of the algorithm, "ext" is the file extension for the
pseudo-archive checksum file, and “mask” defines the structure of each line in
the checksum file. In the text file generated, there will be a line for each
"packed" file. %HASH% will be replaced with a string representation of the
calculated hash value, and %FILENAME% will be replaced with the "packed" file’s
name.

For example, you can use the mask "Hash value of %FILENAME%: %HASH%" to produce
the following text file:

Hash value of File1.dat: 765F90AC
Hash value of Dir\File2.dat: AA45BCF0

USAGE

If you need to display a list of checksums for a file in 7-Zip, use the
CRC SHA\* command in the popup menu. 7-Zip will calculate the checksums and
display them in a separate window. You can copy the content of that window to
the clipboard by using the Ctrl+C hotkey.

If you want to generate a checksum file, select the appropriate format in the
file packing dialog. Then click the "OK" button, and 7zip will generate the
checksum file.

Important! DO NOT enable the "Delete files after compression" option when
generating checksum files, or you will lose your files!

You can also specify the mask directly in the packing dialog by specifying a
string in the format "f=mask" in the Parameters field; please note that the
"mask" string should not contain any spaces. If you need to use a space, use the
underscore character _ instead; each underscore character will be replaced with
a space in the resulting file.

