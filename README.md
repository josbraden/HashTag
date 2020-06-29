# HashTag

HashTag: Parse and Identify Password Hashes

## About

Version 0.41

Written by Smeege (SmeegeSec@gmail.com) on 11/05/2013

HashTag.py is a python script written to parse and identify password hashes. It has three main arguments which consist of identifying a single hash type (-sh), parsing and identifying multiple hashes from a file (-f), and traversing subdirectories to locate files which contain hashes  and parse/identify them (-d). Many common hash types are supported by the CPU and GPU cracking tool Hashcat. Using an additional argument (-hc) hashcat modes will be included in the output file(s).

## Documentation

This info was originally in "HashTag.py Documentation.docx"

### Introduction

HashTag.py is a tool written in python which parses and identifies various password hashes based on their type.  HashTag was inspired by attending [PasswordsCon 13](http://www.youtube.com/playlist?list=PLdIqs92nsIzTphHrDlIucuMP2vatvd4UL) in Las Vegas, KoreLogic’s [‘Crack Me If You Can’](http://contest-2013.korelogic.com/) competition at Defcon, and the research of [iphelix](http://thesprawl.org/iphelix/) and his toolkit [PACK](http://thesprawl.org/projects/pack/).  HashTag supports the identification of over 250 hash types along with matching them to over 110 [hashcat](http://hashcat.net/oclhashcat-plus/) modes.  HashTag is able to identify a single hash, parse a single file and identify the hashes within it, or traverse a root directory and all subdirectories for potential hash files and identify any hashes found.

### Hash Identification

One of the biggest aspects of this tool is the identification of password hashes.  The main attributes I used to distinguish between hash types are character set (hexadecimal, alphanumeric, etc.), hash length, hash format (e.g. 32 character hash followed by a colon and a salt), and any specific substrings (e.g. ‘$1$’).  A lot of password hash strings can’t be identified as one specific hash type based on these attributes.  For example, MD5 and NTLM hashes are both 32 character hexadecimal strings.  In these cases I make an exhaustive list of possible types and have the tool output reflect that.   During development I created an excel spreadsheet which contains much of the hash information I used.

### Usage

HashTag.py {-sh hash |-f file |-d directory} [-o output_filename] [-hc] [-n]

-h, --help | show this help message and exit
-sh SINGLEHASH, --singleHash SINGLEHASH | Identify a single hash
-f FILE, --file FILE | Parse a single file for hashes and identify them
-d DIRECTORY, --directory DIRECTORY | Parse, identify, and categorize hashes within a directory and all subdirectories
-o OUTPUT, --output OUTPUT | Filename to output full list of all identified hashes.
--file default filename: HashTag/HashTag_Output_File.txt
--directory default filename: HashTag/HashTag_Hash_File.txt
-hc, --hashcatOutput | --file: Output a file per different hash type found, if corresponding hashcat mode exists
--directory: Appends hashcat mode to end of separate files
-n, --notFound | --file: Include unidentifiable hashes in the output file.  Good for tool debugging (Is it Identifying properly?)
