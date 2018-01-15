# BaseX-Daffodil

A simple wrapper for using DFDL with Daffodil in XQuery on BaseX.
This is **work in progress** and all comments are welcome.

## Usage examples

Basically it is meant to be used with partial instantiation

```XQuery
import module namespace daffodil = "edu.illinois.ncsa.daffodil"
  at "basex-daffodil/daffodil.xqm";

let $daffodil-bin := "daffodil-2.0.0/bin/daffodil"

let $my-parser := daffodil:daffodil-cmd-use-schema(
  $daffodil-bin, ?, "parse", ?, "-", "utf-8")
  
let $dfdl-tdml := $my-parser("dfdl-schema-file.xsd", "input-file")
```

It is possible to compile and save a DFDL schema with

```XQuery
daffodil:save-parser($daffodil, $schema, $outfile as xs:string?)

(:~
  if no $outfile is specified, a default value of 
  $schema || ".bin"
  will be used
:)
```

and use it with

```XQuery
daffodil:daffodil-cmd-use-saved-parser
  (
    $daffodil, $parser, $action, 
    $infile, $outfile, $sys-encoding as xs:string?
  )
```
