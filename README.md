# xml-prolog

Extensible Markup Language (XML) is a markup language and file format for storing, transmitting, and reconstructing arbitrary data. It defines a set of rules for encoding documents in a format that is both human-readable and machine-readable. The World Wide Web Consortium's XML 1.0 Specification of 1998 and several other related specifications—all of them free open standards—define XML.

The design goals of XML emphasize simplicity, generality, and usability across the Internet. It is a textual data format with strong support via Unicode for different human languages. Although the design of XML focuses on documents, the language is widely used for the representation of arbitrary data structures such as those used in web services.

Several schema systems exist to aid in the definition of XML-based languages, while programmers have developed many application programming interfaces (APIs) to aid the processing of XML data.

## Applications
XML has come into common use for the interchange of data over the Internet. Hundreds of document formats using XML syntax have been developed, including RSS, Atom, Office Open XML, OpenDocument, SVG, and XHTML. XML also provides the base language for communication protocols such as SOAP and XMPP. It is the message exchange format for the Asynchronous JavaScript and XML (AJAX) programming technique.

Many industry data standards, such as Health Level 7, OpenTravel Alliance, FpML, MISMO, and National Information Exchange Model are based on XML and the rich features of the XML schema specification. In publishing, Darwin Information Typing Architecture is an XML industry data standard. XML is used extensively to underpin various publishing formats.

## Key terminology
The material in this section is based on the XML Specification. This is not an exhaustive list of all the constructs that appear in XML; it provides an introduction to the key constructs most often encountered in day-to-day use.

Character
An XML document is a string of characters. Almost every legal Unicode character may appear in an XML document.
Processor and application
The processor analyzes the markup and passes structured information to an application. The specification places requirements on what an XML processor must do and not do, but the application is outside its scope. The processor (as the specification calls it) is often referred to colloquially as an XML parser.
Markup and content
The characters making up an XML document are divided into markup and content, which may be distinguished by the application of simple syntactic rules. Generally, strings that constitute markup either begin with the character < and end with a >, or they begin with the character & and end with a ;. Strings of characters that are not markup are content. However, in a CDATA section, the delimiters <![CDATA[ and ]]> are classified as markup, while the text between them is classified as content. In addition, whitespace before and after the outermost element is classified as markup.
Tag
A tag is a markup construct that begins with < and ends with >. There are three types of tag:
start-tag, such as <section>;
end-tag, such as </section>;
empty-element tag, such as <line-break />.
Element
An element is a logical document component that either begins with a start-tag and ends with a matching end-tag or consists only of an empty-element tag. The characters between the start-tag and end-tag, if any, are the element's content, and may contain markup, including other elements, which are called child elements. An example is <greeting>Hello, world!</greeting>. Another is <line-break />.
Attribute
An attribute is a markup construct consisting of a name–value pair that exists within a start-tag or empty-element tag. An example is <img src="" alt="Madonna" />, where the names of the attributes are "src" and "alt", and their values are "madonna.jpg" and "Madonna" respectively. Another example is <step number="3">Connect A to B.</step>, where the name of the attribute is "number" and its value is "3". An XML attribute can only have a single value and each attribute can appear at most once on each element. In the common situation where a list of multiple values is desired, this must be done by encoding the list into a well-formed XML attribute[i] with some format beyond what XML defines itself. Usually this is either a comma or semi-colon delimited list or, if the individual values are known not to contain spaces,[ii] a space-delimited list can be used. <div class="inner greeting-box">Welcome!</div>, where the attribute "class" has both the value "inner greeting-box" and also indicates the two CSS class names "inner" and "greeting-box".
XML declaration
XML documents may begin with an XML declaration that describes some information about themselves. An example is <?xml version="1.0" encoding="UTF-8"?>.

## Characters and escaping
XML documents consist entirely of characters from the Unicode repertoire. Except for a small number of specifically excluded control characters, any character defined by Unicode may appear within the content of an XML document.

XML includes facilities for identifying the encoding of the Unicode characters that make up the document, and for expressing characters that, for one reason or another, cannot be used directly.

Valid characters
Main article: Valid characters in XML
Unicode code points in the following ranges are valid in XML 1.0 documents:[10]

U+0009 (Horizontal Tab), U+000A (Line Feed), U+000D (Carriage Return): these are the only C0 controls accepted in XML 1.0;
U+0020–U+D7FF, U+E000–U+FFFD: this excludes some non-characters in the BMP (all surrogates, U+FFFE and U+FFFF are forbidden);
U+10000–U+10FFFF: this includes all code points in supplementary planes, including non-characters.
XML 1.1 extends the set of allowed characters to include all the above, plus the remaining characters in the range U+0001–U+001F.[11] At the same time, however, it restricts the use of C0 and C1 control characters other than U+0009 (Horizontal Tab), U+000A (Line Feed), U+000D (Carriage Return), and U+0085 (Next Line) by requiring them to be written in escaped form (for example U+0001 must be written as &#x01; or its equivalent). In the case of C1 characters, this restriction is a backwards incompatibility; it was introduced to allow common encoding errors to be detected.

The code point U+0000 (Null) is the only character that is not permitted in any XML 1.0 or 1.1 document.

Encoding detection
The Unicode character set can be encoded into bytes for storage or transmission in a variety of different ways, called "encodings". Unicode itself defines encodings that cover the entire repertoire; well-known ones include UTF-8 and UTF-16.[12] There are many other text encodings that predate Unicode, such as ASCII and ISO/IEC 8859; their character repertoires in almost every case are subsets of the Unicode character set.

XML allows the use of any of the Unicode-defined encodings and any other encodings whose characters also appear in Unicode. XML also provides a mechanism whereby an XML processor can reliably, without any prior knowledge, determine which encoding is being used.[13] Encodings other than UTF-8 and UTF-16 are not necessarily recognized by every XML parser.

Escaping
XML provides escape facilities for including characters that are problematic to include directly. For example:

The characters "<" and "&" are key syntax markers and may never appear in content outside a CDATA section. It is allowed, but not recommended, to use "<" in XML entity values.[14]
Some character encodings support only a subset of Unicode. For example, it is legal to encode an XML document in ASCII, but ASCII lacks code points for Unicode characters such as "é".
It might not be possible to type the character on the author's machine.
Some characters have glyphs that cannot be visually distinguished from other characters, such as the non-breaking space (&#xa0;) " " and the space (&#x20;) " ", and the Cyrillic capital letter A (&#x410;) "А" and the Latin capital letter A (&#x41;) "A".
There are five predefined entities:

&lt; represents "<";
&gt; represents ">";
&amp; represents "&";
&apos; represents "'";
&quot; represents '"'.
All permitted Unicode characters may be represented with a numeric character reference. Consider the Chinese character "中", whose numeric code in Unicode is hexadecimal 4E2D, or decimal 20,013. A user whose keyboard offers no method for entering this character could still insert it in an XML document encoded either as &#20013; or &#x4e2d;. Similarly, the string "I <3 Jörg" could be encoded for inclusion in an XML document as I &lt;3 J&#xF6;rg.

&#0; is not permitted because the null character is one of the control characters excluded from XML, even when using a numeric character reference.[15] An alternative encoding mechanism such as Base64 is needed to represent such characters.

Comments
Comments may appear anywhere in a document outside other markup. Comments cannot appear before the XML declaration. Comments begin with <!-- and end with -->. For compatibility with SGML, the string "--" (double-hyphen) is not allowed inside comments;[16] this means comments cannot be nested. The ampersand has no special significance within comments, so entity and character references are not recognized as such, and there is no way to represent characters outside the character set of the document encoding.

An example of a valid comment: <!--no need to escape <code> & such in comments-->
### International use
XML 1.0 (Fifth Edition) and XML 1.1 support the direct use of almost any Unicode character in element names, attributes, comments, character data, and processing instructions (other than the ones that have special symbolic meaning in XML itself, such as the less-than sign, "<"). The following is a well-formed XML document including Chinese, Armenian and Cyrillic characters:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<俄语 լեզու="ռուսերեն">данные</俄语>
```

## Syntactical correctness and error-handling
Main article: Well-formed document
The XML specification defines an XML document as a well-formed text, meaning that it satisfies a list of syntax rules provided in the specification. Some key points in the fairly lengthy list include:

The document contains only properly encoded legal Unicode characters.
None of the special syntax characters such as < and & appear except when performing their markup-delineation roles.
The start-tag, end-tag, and empty-element tag that delimit elements are correctly nested, with none missing and none overlapping.
Tag names are case-sensitive; the start-tag and end-tag must match exactly.
Tag names cannot contain any of the characters `!"#$%&'()*+,/;<=>?@[\]^`{|}~`, nor a space character, and cannot begin with "-", "."`, or a numeric digit.
A single root element contains all the other elements.
The definition of an XML document excludes texts that contain violations of well-formedness rules; they are simply not XML. An XML processor that encounters such a violation is required to report such errors and to cease normal processing. This policy, occasionally referred to as "draconian error handling," stands in notable contrast to the behavior of programs that process HTML, which are designed to produce a reasonable result even in the presence of severe markup errors. XML's policy in this area has been criticized as a violation of Postel's law ("Be conservative in what you send; be liberal in what you accept").

The XML specification defines a valid XML document as a well-formed XML document which also conforms to the rules of a Document Type Definition (DTD).

## Schemas and validation
In addition to being well-formed, an XML document may be valid. This means that it contains a reference to a Document Type Definition (DTD), and that its elements and attributes are declared in that DTD and follow the grammatical rules for them that the DTD specifies.

XML processors are classified as validating or non-validating depending on whether or not they check XML documents for validity. A processor that discovers a validity error must be able to report it, but may continue normal processing.

A DTD is an example of a schema or grammar. Since the initial publication of XML 1.0, there has been substantial work in the area of schema languages for XML. Such schema languages typically constrain the set of elements that may be used in a document, which attributes may be applied to them, the order in which they may appear, and the allowable parent/child relationships.

### Document type definition
Main article: Document type definition
The oldest schema language for XML is the document type definition (DTD), inherited from SGML.

DTDs have the following benefits:

- DTD support is ubiquitous due to its inclusion in the XML 1.0 standard.
- DTDs are terse compared to element-based schema languages and consequently present more information in a single screen.
- DTDs allow the declaration of standard public entity sets for publishing characters.
- DTDs define a document type rather than the types used by a namespace, thus grouping all constraints for a document in a single collection.

DTDs have the following limitations:

- They have no explicit support for newer features of XML, most importantly namespaces.
- They lack expressiveness. XML DTDs are simpler than SGML DTDs and there are certain structures that cannot be expressed with regular grammars. DTDs only support rudimentary datatypes.
- They lack readability. DTD designers typically make heavy use of parameter entities (which behave essentially as textual macros), which make it easier to define complex grammars, but at the expense of clarity.
- They use a syntax based on regular expression syntax, inherited from SGML, to describe the schema. Typical XML APIs such as SAX do not attempt to offer applications a structured representation of the syntax, so it is less accessible to programmers than an element-based syntax may be.

Two peculiar features that distinguish DTDs from other schema types are the syntactic support for embedding a DTD within XML documents and for defining entities, which are arbitrary fragments of text or markup that the XML processor inserts in the DTD itself and in the XML document wherever they are referenced, like character escapes.

DTD technology is still used in many applications because of its ubiquity.

### Schema
Main article: [XML Schema (W3C)](https://en.wikipedia.org/wiki/XML_Schema_(W3C))
A newer schema language, described by the W3C as the successor of DTDs, is XML Schema, often referred to by the initialism for XML Schema instances, XSD (XML Schema Definition). XSDs are far more powerful than DTDs in describing XML languages. They use a rich datatyping system and allow for more detailed constraints on an XML document's logical structure. XSDs also use an XML-based format, which makes it possible to use ordinary XML tools to help process them.

xs:schema element that defines a schema:
```xml
<?xml version="1.0" encoding="ISO-8859-1" ?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"></xs:schema>
```
### RELAX NG
RELAX NG (Regular Language for XML Next Generation) was initially specified by OASIS and is now a standard (Part 2: Regular-grammar-based validation of ISO/IEC 19757 – DSDL). RELAX NG schemas may be written in either an XML based syntax or a more compact non-XML syntax; the two syntaxes are isomorphic and James Clark's conversion tool—Trang—can convert between them without loss of information. RELAX NG has a simpler definition and validation framework than XML Schema, making it easier to use and implement. It also has the ability to use datatype framework plug-ins; a RELAX NG schema author, for example, can require values in an XML document to conform to definitions in XML Schema Datatypes.

### Schematron
Schematron is a language for making assertions about the presence or absence of patterns in an XML document. It typically uses XPath expressions. Schematron is now a standard (Part 3: Rule-based validation of ISO/IEC 19757 – DSDL).

### DSDL and other schema languages
DSDL (Document Schema Definition Languages) is a multi-part ISO/IEC standard (ISO/IEC 19757) that brings together a comprehensive set of small schema languages, each targeted at specific problems. DSDL includes RELAX NG full and compact syntax, Schematron assertion language, and languages for defining datatypes, character repertoire constraints, renaming and entity expansion, and namespace-based routing of document fragments to different validators. DSDL schema languages do not have the vendor support of XML Schemas yet, and are to some extent a grassroots reaction of industrial publishers to the lack of utility of XML Schemas for publishing.

Some schema languages not only describe the structure of a particular XML format but also offer limited facilities to influence processing of individual XML files that conform to this format. DTDs and XSDs both have this ability; they can for instance provide the infoset augmentation facility and attribute defaults. RELAX NG and Schematron intentionally do not provide these.
