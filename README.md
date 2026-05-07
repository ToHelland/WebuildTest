# Application Profile (Normative)

## Klasser
TradeAgreement, EconomicOperator, Identifier, IdentifierType, PaymentTerms, MonetaryAmount, PaymentDueCondition, DeliveryTerms, DeliveryLocation, Address, CurrencyCode, IncotermCode, EventCode

---

## Namespaces

| Prefix | Namespace |
|--------|-----------|
| ebwv   | https://w3id.org/ebwv# |
| xsd    | http://www.w3.org/2001/XMLSchema# |
| skos   | http://www.w3.org/2004/02/skos/core# |

---

## Conceptual Model (UML view)

```mermaid
classDiagram
  direction LR

  class TradeAgreement {
    identifier : xsd:string [0..1]
    agreementDate : xsd:dateTime [1]
  }

  class EconomicOperator {
    identifier : Identifier [1]
  }

  class Identifier {
    value : xsd:string [1]
    type : IdentifierType [1..*]
  }

  class IdentifierType {
    code : xsd:string [1]
  }

  class PaymentTerms {
    transactionAmount : MonetaryAmount [1]
    hasPaymentDueCondition : PaymentDueCondition [1]
  }

  class MonetaryAmount {
    value : xsd:decimal [0..1]
    currency : CurrencyCode [1]
  }

  class PaymentDueCondition {
    paymentReferenceEvent : EventCode [1]
    paymentDueDuration : xsd:duration [1]
  }

  class DeliveryTerms {
    incoterm : IncotermCode [1..*]
    deliveryLocation : DeliveryLocation [0..1]
  }

  class DeliveryLocation {
    address : Address [1]
  }

  class Address {
    fullAddress : xsd:string [0..1]
    thoroughfare : xsd:string [0..1]
    locatorDesignation : xsd:string [0..1]
    addressArea : xsd:string [0..1]
    postName : xsd:string [1]
    locatorName : xsd:string [0..1]
    adminUnitL2 : xsd:string [1]
    adminUnitL1 : xsd:string [1]
    postCode : xsd:string [1]
  }

  class CurrencyCode {
    <<skos:Concept>>
    code : xsd:string [1]
  }

  class IncotermCode {
    <<skos:Concept>>
    code : xsd:string [1]
  }

  class EventCode {
    <<skos:Concept>>
    code : xsd:string [1]
  }

  TradeAgreement "1" --> "1" EconomicOperator : buyer
  TradeAgreement "1" --> "1" EconomicOperator : supplier
  TradeAgreement "1" --> "1" PaymentTerms : hasPaymentTerms
  TradeAgreement "1" --> "1" DeliveryTerms : hasDeliveryTerms

  EconomicOperator "1" --> "1" Identifier : identifier
  Identifier "1" --> "1..*" IdentifierType : type

  PaymentTerms "1" --> "1" MonetaryAmount : transactionAmount
  PaymentTerms "1" --> "1" PaymentDueCondition : hasPaymentDueCondition

  MonetaryAmount "1" --> "1" CurrencyCode : currency
  PaymentDueCondition "1" --> "1" EventCode : paymentReferenceEvent

  DeliveryTerms "1" --> "1..*" IncotermCode : incoterm
  DeliveryTerms "1" --> "0..1" DeliveryLocation : deliveryLocation
  DeliveryLocation "1" --> "1" Address : address
```

---

## Class TradeAgreement
URI: ebwv:TradeAgreement  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| identifier | ebwv:identifier | xsd:string | 0..1 | Optional | Identifier of the trade agreement. | External identifier if available. |
| agreementDate | ebwv:agreementDate | xsd:dateTime | 1 | Mandatory | Date and time when the agreement becomes effective. | Legally binding start date. |
| buyer | ebwv:buyer | ebwv:EconomicOperator | 1 | Mandatory | Economic operator acting as the buyer. | |
| supplier | ebwv:supplier | ebwv:EconomicOperator | 1 | Mandatory | Economic operator acting as the supplier. | |
| hasPaymentTerms | ebwv:hasPaymentTerms | ebwv:PaymentTerms | 1 | Mandatory | Payment conditions applicable to the agreement. | |
| hasDeliveryTerms | ebwv:hasDeliveryTerms | ebwv:DeliveryTerms | 1 | Mandatory | Delivery conditions applicable to the agreement. | |

---

## Class EconomicOperator
URI: ebwv:EconomicOperator  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| identifier | ebwv:identifier | ebwv:Identifier | 1 | Mandatory | Identifier of the economic operator. | At least one identifier MUST be provided. |

---

## Class Identifier
URI: ebwv:Identifier  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| value | ebwv:value | xsd:string | 1 | Mandatory | Literal value of the identifier. | |
| type | ebwv:type | ebwv:IdentifierType | 1..* | Mandatory | Type or scheme of the identifier. | Controlled vocabulary. |

---

## Class IdentifierType
URI: ebwv:IdentifierType  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Code identifying the identifier type. | From Identifier Type Code List. |

---

## Class PaymentTerms
URI: ebwv:PaymentTerms  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| transactionAmount | ebwv:transactionAmount | ebwv:MonetaryAmount | 1 | Mandatory | Amount subject to payment. | |
| hasPaymentDueCondition | ebwv:hasPaymentDueCondition | ebwv:PaymentDueCondition | 1 | Mandatory | Condition defining when payment is due. | |

---

## Class MonetaryAmount
URI: ebwv:MonetaryAmount  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| value | ebwv:value | xsd:decimal | 0..1 | Optional | Numeric value of the amount. | |
| currency | ebwv:currency | ebwv:CurrencyCode | 1 | Mandatory | Currency of the amount. | ISO 4217 alphabetic code. |

---

## Class PaymentDueCondition
URI: ebwv:PaymentDueCondition  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| paymentReferenceEvent | ebwv:paymentReferenceEvent | ebwv:EventCode | 1 | Mandatory | Event triggering the payment due period. | Controlled vocabulary. |
| paymentDueDuration | ebwv:paymentDueDuration | xsd:duration | 1 | Mandatory | Duration after the event until payment is due. | ISO 8601 duration. |

---

## Class DeliveryTerms
URI: ebwv:DeliveryTerms  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| incoterm | ebwv:incoterm | ebwv:IncotermCode | 1..* | Mandatory | Applicable INCOTERM(s). | INCOTERMS® 2020. |
| deliveryLocation | ebwv:deliveryLocation | ebwv:DeliveryLocation | 0..1 | Optional | Location where delivery takes place. | |

---

## Class DeliveryLocation
URI: ebwv:DeliveryLocation  
Requirement Level: Optional

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| address | ebwv:address | ebwv:Address | 1 | Mandatory | Address of the delivery location. | |

---

## Class Address
URI: ebwv:Address  
Requirement Level: Optional

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| fullAddress | ebwv:fullAddress | xsd:string | 0..1 | Optional | Full address as a single string. | |
| thoroughfare | ebwv:thoroughfare | xsd:string | 0..1 | Optional | Street name. | |
| locatorDesignation | ebwv:locatorDesignation | xsd:string | 0..1 | Optional | Street number or similar locator. | |
| addressArea | ebwv:addressArea | xsd:string | 0..1 | Optional | Administrative area within locality. | |
| postName | ebwv:postName | xsd:string | 1 | Mandatory | Post town. | |
| locatorName | ebwv:locatorName | xsd:string | 0..1 | Optional | Building name. | |
| adminUnitL2 | ebwv:adminUnitL2 | xsd:string | 1 | Mandatory | Municipality. | |
| adminUnitL1 | ebwv:adminUnitL1 | xsd:string | 1 | Mandatory | Region. | |
| postCode | ebwv:postCode | xsd:string | 1 | Mandatory | Postal code. | |

---

## Class CurrencyCode
URI: skos:Concept  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Currency code. | ISO 4217. |

---

## Class IncotermCode
URI: skos:Concept  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Incoterm code. | INCOTERMS® 2020. |

---

## Class EventCode
URI: skos:Concept  
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. | Description | Note |
|---------|-----|-------|-------|------|-------------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory | Payment reference event code. | EBWV code list. |

