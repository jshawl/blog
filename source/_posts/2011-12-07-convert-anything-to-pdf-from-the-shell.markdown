---
date: '2011-12-07 13:51:17'
layout: post
slug: convert-anything-to-pdf-from-the-shell
status: publish
title: Convert anything to PDF from the shell
wordpress_id: '1191'
categories:
- tech
tags:
- bash
- mac
- openoffice
---

A month or two ago my brother showed me this [great article](http://www.togaware.com/linux/survivor/Convert_MS_Word.html) on how to convert .doc files to PDF from the command line. Well, I think that's a little misleading because OpenOffice can do so much more than just convert .doc files. It can open pretty much any type of file and convert it to PDF. So, I modified the macro a bit and created a script with some additional options. First, fire up OpenOffice and go to Tools→Macros→Organize Macros→OpenOffice.org Basic. Click on Module1 and hit Edit. Then paste this macro into the window:

```
REM  *****  BASIC  *****
Sub ConvertToPDF(cFile)
   cURL = ConvertToURL(cFile)
   ' Open the document.
   ' Just blindly assume that the document is of a type that OOo will
   '  correctly recognize and open -- without specifying an import filter.
   oDoc = StarDesktop.loadComponentFromURL(cURL, "_blank", 0, Array(MakePropertyValue("Hidden", True), ))

   Dim comps
   comps = split (cFile, ".")
   If UBound(comps) > 0 Then
       comps(UBound(comps)) = "pdf"
       cfile = join (comps, ".")
   Else
       cfile = cFile + ".pdf"
   Endif

   cURL = ConvertToURL(cFile)
   ' Save the document using a filter.
   oDoc.storeToURL(cURL, Array(MakePropertyValue("FilterName", "writer_pdf_Export"), ))
   oDoc.close(True)
End Sub

Function MakePropertyValue( Optional cName As String, Optional uValue ) As com.sun.star.beans.PropertyValue
   Dim oPropertyValue As New com.sun.star.beans.PropertyValue
   If Not IsMissing( cName ) Then
      oPropertyValue.Name = cName
   EndIf
   If Not IsMissing( uValue ) Then
      oPropertyValue.Value = uValue
   EndIf
   MakePropertyValue() = oPropertyValue
End Function
```

Then you can use [this script](http://connermcd.com/files/any2pdf.txt) to convert anything into a PDF! If you're not using a mac or have an older version of OpenOffice you may need to modify the script to point towards your soffice binary. I created the following alias in my ~/.profile: `alias pdf="/path/to/any2pdf.sh"` You can see the help menu using the -h flag for more instructions.
