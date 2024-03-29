=======================================================
    PHP FamilySearch API XML Parser Library

    Version 1.0
    Copyright (C) 2010 Neumont University

=======================================================

CONTENTS
     1.  SUPPORT
     1.  LICENSE
     2.  SYSTEM REQUIREMENTS
     3.  USERS GUIDE

-------------------------------------------------------
SUPPORT

This code was created by students from Neumont University under the 
instruction of faculty member John Finlay. Neumont University is a
revolutionary school which provides a hands-on, project-based 
environment for teaching computer science students.  In addition to
classes in computer science theory, the students work on real projects 
such as this one which truly prepare them to enter the work force.
  
Questions and comments regarding this code may be directed to John at 
john.finlay@neumont.edu.

-------------------------------------------------------
LICENSE

This library works with an XML encoding generated by FamilySearch.  While
this code is under the LGPL license, all use of the XML is governed by a
seperate FamilySearch license. 
 
This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
Lesser General Public License for more details.

See LICENSE.txt for the full license.  If you did not receive a 
copy of the license with this code, you may find a copy online
at http://www.opensource.org/licenses/lgpl-license.php

-------------------------------------------------------
SYSTEM REQUIREMENTS

This library requires PHP 4.3 or higher.  It should work on all standard 
distributions of PHP.  SSL connections are possible, but PHP must be compiled
with OpenSSL support. For more information on how to enable OpenSSL in PHP,
refer to: http://www.php.net/manual/en/ref.openssl.php 

This library uses the PHP-FSAPI client library for communicating with 
FamilySearch.  This library has been included for convenience.  See the 
documentation in the FSAPI folder for more information regarding that 
library.

-------------------------------------------------------
USERS GUIDE

This library provides a library for parsing and working with the data returned
from the FamilySearch API.  The FamilySearch API returns data in an XML format.
This library parses that XML into an object model which client code can work 
with to display and manipulate the data.

Included with this library is a class diagram of the object model generated 
from parsing the XML in both Visio (.vsd) and GIF formats.

This library can also be used to convert the parsed data into a GEDCOM format.
In an attempt to prevent data loss some non-standard extensions were made to 
the GEDCOM format.  If you want to output strict GEDCOM 5.5, then edit the 
FSParse/XMLGEDCOM.php file and set the GEDCOM_COMPLIANCE_LEVEL to 5.5.  Note 
that setting the GEDCOM level to 5.5 will cause data loss and you may not be 
able to tie the data back to its FamilySearch equivalent, but it will allow you
to import it into other genealogy applications. 

The following example shows how to parse XML data assumed to be stored in the
variable $xml and print out the name of every person:
<?php
//-- load the library
include_once("FSParse/XMLGEDCOM.php");
//-- create an instance of the object to work with
$xmlGed = new XmlGedcom();
//-- parse the XML
$xmlGed->parseXML($xml);
//-- get the parsed XG_Person objects and show their names
$persons = $xmlGed->getPersons();
foreach ($persons as $person) {
	print "<i>Name:</i> ".$person->getPrimaryName()->getFullText();
	print "<br />";
}
?>

More complete examples are available in the FSParse library folder. The
file GEDCOMTest.php reads in some person data and converts it to GEDCOM.  The
washington.xml file is a test data file which contains most of the 
XML fields one might encounter when obtaining XML from the API.

The file pedigree.php shows an example of how this library, together with the
FSAPI library can be used to build a full client through the FamilySearch API.  
It will generate a 4 generation pedigree chart.  To run this example, point 
your browser to pedigree.php?rootId=me.  You will be prompted to enter your 
FamilySearch API username and password.  These values can be preset by editing 
the file.

The file FS2Gedcom.php will connect to the FamilySearch API and retrieve the 
person specified by the "id" parameter and show the conversion of that person's
XML data into GEDCOM.

=======================================================
