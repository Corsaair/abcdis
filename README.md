abcdis - The ABC disassembler
=============================

From the Redtamarin `/utils` some ActionScript Bytecode (ABC) dissasembler utilities.

For now, those utilities have been ported "as is",
later on we will refactor and reorganise them.

The goal is to build a comprehensive libraries that can work with
the ABC format, the SWF format, the SWC format, etc.


How To Build
------------

Install the [redtamarin-sdk](), this will install the `redbean` build tool.

Build abcdump  
`$ redbean -f build_abcdump.as3`

Build abcdis  
`$ redbean -f build_abcdis.as3`

Build abcdump2  
`$ redbean -f build_abcdisclassic.as3`


If you want to install the executables in `/usr/bin` so you can use them anywhere
follow the same logic as with the redtamarin executables.

For ex:

  - move `abcdump`  
    to `/usr/lib/redtamarin/bin/`
  - create the file `/usr/bin/abcdump`  
    `$ sudo touch /usr/bin/abcdump`  
    `$ sudo chmod +x /usr/bin/abcdump`  
    with the following content
```
#!/bin/bash
/usr/lib/redtamarin/bin/abcdump $@
```

> We improved the redtamarin projectors  
> but we still need to do that for  
> everything to works smoothly



History
-------

In the Tamarin project you coulf find an utility named `abcdump`,
when Redtamarin extended the project we kept this utility around
because it is always useful to be able to decompile stuff and see what's inside ;).

In the mean time, during the years where Tamarin was still udpdated,
came a patch by Alex Macdonald and contributed by Chris Brichford
named `abcdis`.

see [Bug 640986 - abcdump should be better factored and dump more information about the abc](https://bugzilla.mozilla.org/show_bug.cgi?id=640986).

Because we changed the avmplus API with the Redtamatin API,
some bits and bops needed to be adapted, but yeah it's all here
compiling and working as standalone executables.


abcdump
-------

`$ ./abcdump`

```
Displays the contents of abc or swf files

Usage:

    abcdump [options] file ...

Each file can be an ABC or SWF/SWC format file

Options:

 -a   Extract the ABC blocks from the SWF/SWC, but do not
      otherwise display their contents.  The file names are
      of the form file<n>.abc where "file" is the name
      of the input file minus the .swf/.swc extension;
      and <n> is omitted if it is 0.

 -i   Print information about the ABC, but do not dump the byte code.

 -abs Print the bytecode, but no information about the ABC
 -api Print the public API exposed by this abc/swf
 -mdversions Use in conjunction with -api when the abc/swf uses old-style versioning
 -pools Print out the contents of the constant pools
 --decompress-only Write out a decompressed version of the swc and exit
```


abcdis
------

`$ ./abcdis`

```
Error: Too few arguments

[-xml] [-dot] [-abcasm] [-api] inputFileName outputDirectory

	at CmdLine$/usage()
	at CmdLine$/parse()
	at ABCDump$/abcDump()
	at global$init()
```

The XML output format should be compatible with the output orf SWFdump found in the Flex SDK utilities.

The DOT output format is menat to be parsed by GraphViz.

for ex: `$ dot -Tpdf tmp/test123.swf-0-mb-0.dot -o tmp/test123.swf-0-mb-0.pdf`

You can easily install GraphViz under Mac OS X with MacPorts  
`$ sudo port install graphviz`



abcdump2
--------

Originally named `abcdisclassic` we decided to rename it `abcdump2`
because it basically use the code base of abcdis to re-implement the original abcdump.

`$ ./abcdump2 -h`

```
Invalid option: -h

Displays the contents of abc or swf files

Usage:

    abcdump [-i] [-pools] file ...
    abcdump --decompress-only file ...
    abcdump -a file ...
    abcdump -api file ...
    abcdump -abs file ...

Each file can be an ABC or SWF/SWC format file

Options:

 -a   Extract the ABC blocks from the SWF/SWC, but do not
      otherwise display their contents.  The file names are
      of the form file<n>.abc where "file" is the name
      of the input file minus the .swf/.swc extension;
      and <n> is omitted if it is 0.

 -i   Print information about the ABC, but do not dump the byte code.

 -abs Print the bytecode, but no information about the ABC
 -api Print the public API exposed by this abc/swf
 -pools Print out the contents of the constant pools
 --decompress-only Write out a decompressed version of the swc and exit

```

