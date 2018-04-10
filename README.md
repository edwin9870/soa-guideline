# SOA Guideline

## Index

1. [WSDL](#1-wsdl)
2. XSD
3. XQueries
4. XSLT
5. Database design
6. SOA Composite Applications
7. Oracle Service Bus (OSB)

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

Aditionally, the full version must be especifiqued in the schema's version attribute. Ex: `version="1.0"`

## 2.2 Qualification

All element must be qualified, for this it must be specific as *qualified* element *elementFormDefault*.

Attribues should not be qualified.

## 2.3 XSD Design Pattern

**Garden of Ede** must be used as XSD's design pattern.

>> The **Venetian Blind** approach is similar to the Russian Doll approach in that they both use a single global element.  The Venetian Blind approach describes a modular approach by naming and defining all type definitions globally (as opposed to the Salami Slice approach which declares elements globally and types locally).  Each globally defined type describes an individual "slat" and can be reused by other components.  In addition, all the locally declared elements can be namespace qualified or namespace unqualified (the slats can be "opened" or "closed") depending on the elementFormDefault attribute setting at the top of the schema.  If the namespace is unqualified then the local elements in the instance document must not be qualified with the prefix of the namespace.
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

**xsd** prefix must be used when refering to XSD's elements