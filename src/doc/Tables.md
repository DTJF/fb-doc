Tables  {#pageTables}
======
\tableofcontents

This chapter contains some information on fb-doc in table format.

Overview  {#SecTabOverview}
========

fb-doc is a multi functional tool. The choosen Emitter specifies which
kind of output to generate. And the choosen Run Mode specifies where to
get input from and where to write the output at. Here's a table of all
run modes against the inbuild emitters ("DEF" = default configuration,
"+" = useful combination, "-" = combination not useful).

| Emitter \ Run Mode | default | `--file-mode` | `--list-mode` | `--syntax-mode` | `--geany-mode` |
| -----------------: | :-----: | :-----------: | :-----------: | :-------------: | :------------: |
| C_Source           |   DEF   |      DEF      |       -       |        -        |        +       |
| GtkDocTemplates    |    +    |       +       |       -       |        -        |       DEF      |
| DoxygenTemplates   |    +    |       +       |       -       |        -        |        +       |
| FunctionNames      |    +    |       +       |      DEF      |        -        |        +       |
| SyntaxHighLighting |    +    |       +       |       -       |       DEF       |        +       |


Emitter  {#SecTabEmitter}
=======

fb-doc has five inbuild emitters to generate different kinds of output.
By setting a run mode (\ref sectOptModes) a default emitter gets
specified. Use option `--emitter` (`-e`) after the run mode option to
override the default setting. See chapter \ref ChaEmitter for details.

\note Only one emitter can be in use at a time.

<table>
<tr>
<th> Name
<th> Default in Mode
<th> Function
</th>
<tr>
<td> [C_Source](\ref sectEmitterCSource)
<td> default mode (Doxy-Filter) and `--file-mode`
<td> Translate FB source and documentational comments in intermediate format.
<tr>
<td> [GtkDocTemplates](\ref sectEmitterGtkTempl)
<td> `--geany-mode`
<td> Emit original source code and prepend documentation relevant
     constructs by templates for gtk-doc. Prefered usage in
     `--geany-mode`.
<tr>
<td> [DoxygenTemplates](\ref sectEmitterDoxyTempl)
<td> none
<td> Emit original source code and prepend documentation relevant
     constructs by templates for Doxygen. Prefered usage in
     `--geany-mode`.
<tr>
<td> [FunctionNames](\ref sectEmitterLfn)
<td> `--list-mode`
<td> Emit a list of all function names. Prefered usage in `--list-mode`
     to generate the file *fb-doc.lfn*.
<tr>
<td> [SyntaxHighLighting](\ref sectEmitterSyntax)
<td> `--syntax-mode`
<td> Emit all source code encapsulated by syntax highlighting tags.
     Prefered usage in `--syntax-mode` (for Doxygen output in
     <em>*.html, *.tex</em> and <em>*.xml</em> files; in other run
     modes *html* tags).
</table>


Run Mode  {#SecTabRunModi}
========

The data flow, that is where to get input from and where to write
output at, gets specified by the run mode. The following table shows
the relations between run mode and input / output targets, See \ref
sectOptModes for details.

<table>
<tr>
<th> Option
<th> Default Emitter
<th> Input
<th> Output
</th>
<tr>
<td> none (Doxy-Filter-Mode)
<td> [C_Source](\ref sectEmitterCSource)
<td> one file
<td> stream to STDOUT
<tr>
<td> `-f` *or* `--file-mode`
<td> [C_Source](\ref sectEmitterCSource)
<td> controlled by file specification[s]
<td> *.\em c and *.\em h files
<tr>
<td> `-g` *or* `--geany-mode`
<td> [GtkDocTemplates](\ref sectEmitterGtkTempl)
<td> stream from STDIN
<td> stream to STDOUT
<tr>
<td> `-l` *or* `--list-mode`
<td> [FunctionNames](\ref sectEmitterLfn)
<td> controlled by file specification[s]
<td> file \em fb-doc.lfn
<tr>
<td> `-s` *or* `--syntax-mode`
<td> [SyntaxHighLighting](\ref sectEmitterSyntax)
<td> Doxyfile (+ files *.\em bas, *.\em bi, *.\em html, *.\em tex or *.\em xml)
<td> files *.\em html, *.\em tex or *.\em xml
<tr>
<td> `-h` *or* `--help`
<td> none
<td> none
<td> stream to STDOUT
<tr>
<td> `-v` *or* `--version`
<td> none
<td> none
<td> stream to STDOUT
</table>

\note The default mode is the Doxygen filter mode, since Doxygen 
      doesn't allow to send further options (directly).

\note The modi `--help` (`-h`) and `--version` (`-v`) are not related
      to any FB source. They emit their output always on STDOUT.


Options  {#SecTabOptions}
=======

The following table contains an overview of all fb-doc options. An
option either starts by a minus character followed by a single
character (short form) or by two minus characters followed by a word or
pair of words (LONG form). Both forms have the same meaning.

Some options expect an additional parameter, separated by a whitespace
character. Each further word in the command line (without the leading
'-' character) gets interpreted as a file name or pattern, see \ref
pageOptionDetails .

<table>
<tr>
<th> Option (short) <th> Parameter <th> Description
<tr>
<td> [--asterix (-a)](\ref subsectOptAsterix)
<td> none
<td> The C_Source emitter generates lines in a multi line comment block
     with leading '* ' characters (gtk-doc style).
<tr>
<td> [--cstyle (-c)](\ref subsectOptCstyle)
<td> none
<td> The C_Source emitter generates types in real C syntax
     (instead of FB styled pseudo C syntax). Also used in emitter
     `DoxygenTemplates`.
<tr>
<td> [--emitter (-e)](\ref subsectOptEmitters)
<td> Emitter name
<td> Customized emitter selection. fb-doc compares the parameter with
     the names of the internal emitters. In case of no match it tries to
     find and load an external with this name.
<tr>
<td> [--file-mode (-f)](\ref subsectOptFileMode)
<td> none
<td> Read FB source files and write output to similar named files
     (overriding existend, if any).
<tr>
<td> [--geany-mode (-g)](\ref subsectOptGeanyMode)
<td> Emitter name
<td> Read input from STDIN and write to STDOUT. The parameter is optional. (No file specs.)
<tr>
<td> [--help (-h)](\ref subsectOptHelp)
<td> none
<td> Print the help text and quit.
<tr>
<td> [--list-mode (-l)](\ref subsectOptListMode)
<td> none
<td> Read FB source files and write output to file *fb-doc.lfn*.
<tr>
<td> [--outpath (-o)](\ref subsectOptOutpath)
<td> path
<td> Set folder for file output.
<tr>
<td> [--recursiv (-r)](\ref subsectOptRecursiv)
<td> none
<td> Scan for input files in the working folder and all subfolders.
     Works only in combination with file patterns.
<tr>
<td> [--syntax-mode (-s)](\ref SubSecOptSyntaxMode)
<td> none
<td> Scan a Doxyfile (or multiple) for its output and fix syntax
     highlighting.
<tr>
<td> [--tree (-t)](\ref subsectOptTree)
<td> none
<td> Follow the \#`INCLUDE` statements in the source tree (if
     possible -- not available in \ref subsectOptGeanyMode).
<tr>
<td> [--version (-v)](\ref subsectOptVersion)
<td> none
<td> Print the version information and quit.
</table>

\note An empty command line makes fb-doc to output the help text 
      (as if option `--help` was given).

\note Multiple run modes raise an error message, only one run mode is
      allowed at a time.


File Specifications  {#SecTabFileSpecs}
===================

Any text in the command line not matching an option or its parameter
gets interpreted as a file specification, that is either a file name or
a file pattern. File specs get added to a queue and fb-doc executes
this queue in the given order. Depending on the file spec[s] and the
run mode, fb-doc operates in different ways:

<table>
<tr>
<th> Option (run-mode)
<th> no file specs
<th> file name
<th> file pattern
</th>
<tr>
<td> default
<td> print help text
<td> load file, emit output to STDOUT
<td> load all files matching the pattern, emit output to STDOUT
<tr>
<td> -f *or* --file-mode <td> load all *.\em bas and *.\em 
     bi files, emit output for each file to a *.\em c or *.\em h file 
<td> load file, emit output to a *.\em c or *.\em h file
<td> load all files matching the pattern, emit output for each file 
     to a *.\em c or *.\em h file
<tr>
<td> `-g` *or* `--geany-mode`
<td> ignored
<td> ignored
<td> ignored
<tr>
<td> `-l` *or* `--list-mode` <td> load all *.\em bas and *.
     \em bi files, emit output to one file named \em fb-doc.lfn 
<td> load file, emit output to one file named \em fb-doc.lfn</td>
<td> load all files matching the file spec, emit output to one file
     named \em fb-doc.lfn</td>
</table>

\note A file name may be prepended by a relative or an absolute path.

\note File names or paths including a space character have to be 
      enclosed by single or double quotes.

\note Multiple file names get separated by a space character or by a 
      ; character.

\note Multiple file specs (names and patterns) can get specified in the
      command line.

\note In case of file output the extension of the output file depends
      on the extension of the input file: *.\em bas gets *.\em c and
      *.\em bi gets *.\em h.

\note A file name cannot start with a minus character and cannot 
      include single or double quote characters.

\note On UNIX like systems usually the shell (bash) expands the file
      patterns (fb-doc doesn't see the pattern, but gets the files
      list instead, so option `--recursive` doesn't work -- enclose
      the pattern by single or double quotes to hinder that).


Intermediate Format  {#SecTabInterForm}
===================

The following table contains some examples on how FB source code gets
transformed to the intermediate (C-like) format.

The main trick to make a C parsers work on FB source is to transform
the declarations for variables and functions. FB syntax is full of
keywords for better human readability. Most of them are unknown for the
C parser (fbc-0.90 has more than 400 keyword, in C it's less than 50).

A type specification may have more than one word, the C parsers expect
just a single word. That's why fb-doc packs all FB information in a
single word type name, so that the C tool can handle this fantasy type
and build the documentation output.

Therefor the FB keywords get mangled in to one single word, separated
by underscore characters. This mangling can get suppressed by option
`--cstyle`, to get real C types emitted. There's also some influences
on the emitted TYPEs and file names of include files.

|                                  FB source |            default                 | `--cstyle`            |
| -----------------------------------------: | :--------------------------------: | :-------------------- |
|                       `DIM AS INTEGER Nam` | `INTEGER Nam`                      | `int Nam`             |
|                       `DIM Nam AS INTEGER` | `INTEGER Nam`                      | `int Nam`             |
|                     `CONST Nam AS INTEGER` | `CONST_AS_INTEGER Nam`             | `const int Nam`       |
|                    `Extern Nam AS INTEGER` | `Extern_AS_INTEGER Nam`            | `extern int Nam`      |
| `DECLARE PROPERTY Cu.Tok() AS INTEGER PTR` | `PROPERTY_AS_INTEGER_PTR Cu.Tok()` | `int *Cu.Tok(void)`   |
|                `BYVAL Export_ AS EmitFunc` | `BYVAL_AS_EmitFunc Export_`        | `EmitFunc *Export_`   |
|                          `byref Z as byte` | `byref_as_byte Z`                  | `char *Z`             |
|                          `byval Z as byte` | `byval_as_byte Z`                  | `char Z`              |
|                    `TYPE Udt ... END TYPE` | `class Udt{ ... };`                | `typedef Udt{ ... };` |
|                  \#`INCLUDE ONCE "abc.bi"` | \#`include "abc.bi"`               | \#`include "abc.h"`   |
|                 \#`INCLUDE ONCE "xyz.bas"` | \#`include "xyz.bas"`              | \#`include "xyz.c"`   |


Files  {#SecTabFiles}
=====

The folder *doc* contains configuration files to build this
documentation by executing Doxygen in this folder, check its manual for
details. Those files are not listed in the Files browser, here're the
their functions

|        fb-doc/doc | Function                                                             |
| ----------------: | :------------------------------------------------------------------- |
|          Doxyfile | A configuration file, controlling the Doxygen and fb-doc operations. |
| DoxygenLayout.xml | A configuration file, controlling the index of these *html* pages.   |
|  DoxyExtension.in | A configuration file for CMake, containing global information.       |
|        fb-doc.lfn | A list of function names generated by executing `fb-doc -l`.         |
|        fb-doc.css | A customized style sheet specifying the colors.                      |

To generate caller / callee graphs in the documentation (as in this
html files) you have to install the *dot* tool from the *GraphViz*
package. Executing `fb-doc -l` before doxygen is mandatory to update
the file fb-doc.lfn.

This will generate the documentation with FB source files in
intermediate format. For correct syntax highlighting execute `fb-doc
-s` after the doxygen run. It will replace the Doxygen output files in
the output folders.

\note For this to work, the file Doxyfile must contain the path to all
      FB source files in the first entry (`INPUT =`).