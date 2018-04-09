# SOA Guideline

## Index

1. [WSDL](wsdl)
2. XSD
3. XQueries
4. XSLT
5. Database design
6. SOA Composite Applications
7. Oracle Service Bus (OSB)

---

# <a name="wsdl"></a> 1. WSDL

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