# Application Profile

## Namespaces

| Prefix | Namespace |
|-------|----------|
| ebwv | https://w3id.org/ebwv# |
| xsd | http://www.w3.org/2001/XMLSchema# |
| skos | http://www.w3.org/2004/02/skos/core# |

---

## Conventions

- Classes are identified using `ebwv:ClassName`
- Properties are identified using `ebwv:propertyName`
- Requirement Level is derived from multiplicity:
  - `1`, `1..*` → **Mandatory**
  - `0..1`, `0..*` → **Optional**
- Code lists are represented as `skos:Concept`
- The property `code` uses `skos:prefLabel`
- URIs are expressed using CURIE notation only (`prefix:localName`)

---

## Class TradeAgreement

**Description**  
A contractual agreement defining the terms of a trade between economic operators.

**URI**  
`ebwv:TradeAgreement`

**Requirement Level**  
Mandatory

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| identifier | ebwv:identifier | xsd:string | 0..1 | Optional | Identifies the trade agreement |  |  |
| agreementDate | ebwv:agreementDate | xsd:dateTime | 1 | Mandatory | Date and time when the agreement becomes effective |  |  |
| buyer | ebwv:buyer | ebwv:EconomicOperator | 1 | Mandatory | The economic operator acting as the buyer |  |  |
| supplier | ebwv:supplier | ebwv:EconomicOperator | 1 | Mandatory | The economic operator acting as the supplier |  |  |
| hasPaymentTerms | ebwv:hasPaymentTerms | ebwv:PaymentTerms | 1 | Mandatory | Specifies the payment terms applicable to the agreement |  |  |
| hasDeliveryTerms | ebwv:hasDeliveryTerms | ebwv:DeliveryTerms | 1 | Mandatory | Specifies the delivery terms applicable to the agreement |  |  |

---

## Class EconomicOperator

**Description**  
An entity participating in a trade agreement, acting as buyer or supplier.

**URI**  
`ebwv:EconomicOperator`

**Requirement Level**  
Mandatory

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| identifier | ebwv:identifier | ebwv:Identifier | 1 | Mandatory | Identifier of the economic operator |  |  |

---

## Class Identifier

**Description**  
A structured identifier consisting of a value and a type.

**URI**  
`ebwv:Identifier`

**Requirement Level**  
Mandatory

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| value | ebwv:value | xsd:string | 1 | Mandatory | Literal value of the identifier |  |  |
| type | ebwv:type | ebwv:IdentifierType | 1..* | Mandatory | Identifier type or scheme |  |  |

---

## Class PaymentTerms

**Description**  
Terms and conditions describing how and when payment is to be made.

**URI**  
`ebwv:PaymentTerms`

**Requirement Level**  
Mandatory

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| transactionAmount | ebwv:transactionAmount | ebwv:MonetaryAmount | 1 | Mandatory | Amount subject to payment |  |  |
| hasPaymentDueCondition | ebwv:hasPaymentDueCondition | ebwv:PaymentDueCondition | 1 | Mandatory | Defines when payment becomes due |  |  |

---

## Class MonetaryAmount

**Description**  
A monetary amount expressed in a specific currency.

**URI**  
`ebwv:MonetaryAmount`

**Requirement Level**  
Mandatory

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| value | ebwv:value | xsd:decimal | 0..1 | Optional | Numeric value of the amount |  |  |
| currency | ebwv:currency | skos:Concept (CurrencyCode) | 1 | Mandatory | Currency of the amount |  |  |

---

## Class PaymentDueCondition

**Description**  
Defines the trigger and duration for when payment is due.

**URI**  
`ebwv:PaymentDueCondition`

**Requirement Level**  
Mandatory

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| paymentReferenceEvent | ebwv:paymentReferenceEvent | skos:Concept (EventCode) | 1 | Mandatory | Event that triggers the start of the payment due period |  |  |
| paymentDueDuration | ebwv:paymentDueDuration | xsd:duration | 1 | Mandatory | Time interval after the event until payment is due |  |  |

---

## Class DeliveryTerms

**Description**  
Delivery conditions, including incoterms and delivery location.

**URI**  
`ebwv:DeliveryTerms`

**Requirement Level**  
Mandatory

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| incoterm | ebwv:incoterm | skos:Concept (IncotermCode) | 1..* | Mandatory | Applicable incoterm(s) |  |  |
| deliveryLocation | ebwv:deliveryLocation | ebwv:DeliveryLocation | 0..1 | Optional | Location where delivery takes place |  |  |

---

## Class DeliveryLocation

**Description**  
A location associated with delivery, described by an address.

**URI**  
`ebwv:DeliveryLocation`

**Requirement Level**  
Optional

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| address | ebwv:address | ebwv:Address | 1 | Mandatory | Address describing the delivery location |  |  |

---

## Class Address

**Description**  
A structured postal address.

**URI**  
`ebwv:Address`

**Requirement Level**  
Optional

### Properties

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| fullAddress | ebwv:fullAddress | xsd:string | 0..1 | Optional | Full address as a single string |  |  |
| thoroughfare | ebwv:thoroughfare | xsd:string | 0..1 | Optional | Street name |  |  |
| locatorDesignation | ebwv:locatorDesignation | xsd:string | 0..1 | Optional | Street number or other locator designation |  |  |
| addressArea | ebwv:addressArea | xsd:string | 0..1 | Optional | Administrative area within a locality (e.g., district) |  |  |
| postName | ebwv:postName | xsd:string | 1 | Mandatory | Post town / locality name |  |  |
| locatorName | ebwv:locatorName | xsd:string | 0..1 | Optional | Additional locator name (e.g., building name) |  |  |
| adminUnitL2 | ebwv:adminUnitL2 | xsd:string | 1 | Mandatory | Second-level administrative unit (e.g., municipality) |  |  |
| adminUnitL1 | ebwv:adminUnitL1 | xsd:string | 1 | Mandatory | First-level administrative unit (e.g., region/county) |  |  |
| postCode | ebwv:postCode | xsd:string | 1 | Mandatory | Postal code |  |  |

---

## Code lists (as concepts)

### Class CurrencyCode

**Description**  
A currency code represented as a SKOS concept.

**URI**  
`skos:Concept`

**Requirement Level**  
Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Currency code label |  |  |

---

### Class IncotermCode

**Description**  
An incoterm code represented as a SKOS concept.

**URI**  
`skos:Concept`

**Requirement Level**  
Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Incoterm code label |  |  |

---

### Class EventCode

**Description**  
An event code represented as a SKOS concept.

**URI**  
`skos:Concept`

**Requirement Level**  
Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Event code label |  |  |

---

### Class IdentifierType

**Description**  
A controlled value indicating the scheme or type of an identifier.

**URI**  
`ebwv:IdentifierType`

**Requirement Level**  
Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note | Usage note |
|--------|-----|-------|-------|------|-------------|------|------------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Identifier type label |  |  |

---

# Mermaid Model

```mermaid
classDiagram
    class TradeAgreement {
        +identifier : xsd:string [0..1]
        +agreementDate : xsd:dateTime [1]
        +buyer : EconomicOperator [1]
        +supplier : EconomicOperator [1]
        +hasPaymentTerms : PaymentTerms [1]
        +hasDeliveryTerms : DeliveryTerms [1]
    }

    class EconomicOperator {
        +identifier : Identifier [1]
    }

    class Identifier {
        +value : xsd:string [1]
        +type : IdentifierType [1..*]
    }

    class PaymentTerms {
        +transactionAmount : MonetaryAmount [1]
        +hasPaymentDueCondition : PaymentDueCondition [1]
    }

    class MonetaryAmount {
        +value : xsd:decimal [0..1]
        +currency : CurrencyCode [1]
    }

    class PaymentDueCondition {
        +paymentReferenceEvent : EventCode [1]
        +paymentDueDuration : xsd:duration [1]
    }

    class DeliveryTerms {
        +incoterm : IncotermCode [1..*]
        +deliveryLocation : DeliveryLocation [0..1]
    }

    class DeliveryLocation {
        +address : Address [1]
    }

    class Address {
        +fullAddress : xsd:string [0..1]
        +thoroughfare : xsd:string [0..1]
        +locatorDesignation : xsd:string [0..1]
        +addressArea : xsd:string [0..1]
        +postName : xsd:string [1]
        +locatorName : xsd:string [0..1]
        +adminUnitL2 : xsd:string [1]
        +adminUnitL1 : xsd:string [1]
        +postCode : xsd:string [1]
    }

    class CurrencyCode<<skos:Concept>> {
