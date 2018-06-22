# SOA Guideline

## Index

1. [WSDL](#1-wsdl)
2. [XSD](#2-xsd)
3. [XQuery](#3-xquery)
4. [XSLT](#4-xslt)
5. [SOA Composite Applications](#5-soa-composite-applications)
6. [Oracle Service Bus (OSB)](#6-oracle-service-bus-osb)

---

# 1. WSDL

## 1.1 Namespace structure

`http://www.domain.name/[year]/[DomainName]/Service/[ServiceName]/v1`

> v1 refers to the WSDL's version. It will increments by 1 each time a change break the design of a method.

## 1.2 Prefix

* **wsdl prefix** should be used when declaring wsdl's elements
* **stns prefix** should be used to refer to the primary schema

## 1.3 WSDL's abstract section

* **WSDL's defination name:** Service name

### 1.3.1 WSDL's message element

* **attribute name for input method:** [methodName]Request
* **attribute name for output method:** [methodName]Response
* **WSDL's part name**: payload

### 1.3.2 WSDL's portType element

* **attribute name :** [ServiceName]PortType
* **operation's attribute name:** [methodName]

## 1.4 WSDL's concrate section

### 1.4.1 binding element

* **binding's attribute name:** [portTypeName]Binding
* **soap:binding's style :** document
* **SOAP 1.1 should be used. SOAP 1.1 namespace:** `http://schemas.xmlsoap.org/soap/http`
* **soapAction:** WSDL's namespace/methodName
* **soap body's attribute use:** literal

### 1.4.2 Service element

* **name attribute:** the service name
* **wsdl:port's name attribute:** [ServiceName]Port

# 2. XSD

## 2.1 Namespace structure

`http://www.domain.name/[year]/[DomainName]/Schema/[ServiceName]/v1`

Additionally, the full version must be specified in the schema's version attribute. Ex: `version="1.0"`

## 2.2 Qualification

All element must be qualified, for this, it must be specified as *qualified* element *elementFormDefault*.

Attributes should not be qualified.

## 2.3 XSD Design Pattern

**Garden of Ede** must be used as XSD's design pattern.

>> The Garden of Eden approach implements characteristics of the Venetian Blind and Salami Slice approach.  Like the Salami Slice the Garden of Eden uses a modular approach by defining all elements globally and like the Venetian Blind approach all type definitions are declared globally.  Each element is globally defined as an immediate child of the <schema> node and its type attribute can be set to one of the named complex types.  Since the elements are globally declared, the namespace must be exposed no matter what the settings of the elementFormDefault attribute is.  Therefore, if the elementFormDefault attribute is set to qualified, this does not change the content and structure of the instance document but if the attribute is set to unqualified then the local elements in the instance document must not be qualified with the prefix of the namespace prefix..
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <xs:schema targetNamespace="TargetNamespace" xmlns:TN="TargetNamespace" > xmlns:xs="http://www.w3.org/2001/XMLSchema" 
> elementFormDefault="qualified" attributeFormDefault="unqualified">
>    <xs:element name="BookInformation" type="TN:BookInformation" > maxOccurs="unbounded"/>
>     <xs:complexType name="BookInformation">
>       <xs:sequence>
>            <xs:element name="Title"/>
>            <xs:element name="ISBN"/>
>           <xs:element name="PeopleInvolved" type="TN:PeopleInvolvedType" maxOccurs="unbounded"/>
>        </xs:sequence>
>    </xs:complexType>
>    <xs:complexType name="PeopleInvolvedType">
>        <xs:sequence>
>            <xs:element name="Author"/>
>            <xs:element name="Publisher"/>
>        </xs:sequence>
>    </xs:complexType>
></xs:schema>```

Source: https://blogs.msdn.microsoft.com/skaufman/2005/04/29/schema-design-patterns-venetian-blind/

## 2.4 Prefix

**xsd** prefix must be used when referring to XSD's elements.

# 3. XQuery

* XQuery's file name must be in PascalCase
* XQuery's Method name must be in camelCase.
* XQuery's version must be 1.0
* XQuery's enconding must be utf-8
* Xquery's variables must be in camelCase

# 4. XSLT

TBD

# 5. SOA Composite Applications

## 5.1 Partitions

Partition's name must be in lowercase

# 6. Oracle Service Bus (OSB)

## 6.1 Node, pipeline, routing and stages naming convention

* Node, pipeline, and routing must use the Proxy's name as the prefix and must be in PascalCase.

* Stages should be writing in camelCase.

## 6.2 Variable naming convention

* Variables should be writen in camelCase.

* Service Callout variable name's should use the following patterns: _methodName_**[Request/Response]**

## 6.2 HTTP Proxy Service endpoint naming convention

Proxy service's endpoint must be in lowercase.