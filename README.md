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

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| identifier | ebwv:identifier | xsd:string | 0..1 | Optional |
| agreementDate | ebwv:agreementDate | xsd:dateTime | 1 | Mandatory |
| buyer | ebwv:buyer | ebwv:EconomicOperator | 1 | Mandatory |
| supplier | ebwv:supplier | ebwv:EconomicOperator | 1 | Mandatory |
| hasPaymentTerms | ebwv:hasPaymentTerms | ebwv:PaymentTerms | 1 | Mandatory |
| hasDeliveryTerms | ebwv:hasDeliveryTerms | ebwv:DeliveryTerms | 1 | Mandatory |

---

## Class EconomicOperator
URI: ebwv:EconomicOperator
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| identifier | ebwv:identifier | ebwv:Identifier | 1 | Mandatory |

---

## Class Identifier
URI: ebwv:Identifier
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| value | ebwv:value | xsd:string | 1 | Mandatory |
| type | ebwv:type | ebwv:IdentifierType | 1..* | Mandatory |

---

## Class IdentifierType
URI: ebwv:IdentifierType
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |

---

## Class PaymentTerms
URI: ebwv:PaymentTerms
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| transactionAmount | ebwv:transactionAmount | ebwv:MonetaryAmount | 1 | Mandatory |
| hasPaymentDueCondition | ebwv:hasPaymentDueCondition | ebwv:PaymentDueCondition | 1 | Mandatory |

---

## Class MonetaryAmount
URI: ebwv:MonetaryAmount
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| value | ebwv:value | xsd:decimal | 0..1 | Optional |
| currency | ebwv:currency | ebwv:CurrencyCode | 1 | Mandatory |

---

## Class PaymentDueCondition
URI: ebwv:PaymentDueCondition
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| paymentReferenceEvent | ebwv:paymentReferenceEvent | ebwv:EventCode | 1 | Mandatory |
| paymentDueDuration | ebwv:paymentDueDuration | xsd:duration | 1 | Mandatory |

---

## Class DeliveryTerms
URI: ebwv:DeliveryTerms
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| incoterm | ebwv:incoterm | ebwv:IncotermCode | 1..* | Mandatory |
| deliveryLocation | ebwv:deliveryLocation | ebwv:DeliveryLocation | 0..1 | Optional |

---

## Class DeliveryLocation
URI: ebwv:DeliveryLocation
Requirement Level: Optional

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| address | ebwv:address | ebwv:Address | 1 | Mandatory |

---

## Class Address
URI: ebwv:Address
Requirement Level: Optional

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| fullAddress | ebwv:fullAddress | xsd:string | 0..1 | Optional |
| thoroughfare | ebwv:thoroughfare | xsd:string | 0..1 | Optional |
| locatorDesignation | ebwv:locatorDesignation | xsd:string | 0..1 | Optional |
| addressArea | ebwv:addressArea | xsd:string | 0..1 | Optional |
| postName | ebwv:postName | xsd:string | 1 | Mandatory |
| locatorName | ebwv:locatorName | xsd:string | 0..1 | Optional |
| adminUnitL2 | ebwv:adminUnitL2 | xsd:string | 1 | Mandatory |
| adminUnitL1 | ebwv:adminUnitL1 | xsd:string | 1 | Mandatory |
| postCode | ebwv:postCode | xsd:string | 1 | Mandatory |

---

## Class CurrencyCode
URI: skos:Concept
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |

---

## Class IncotermCode
URI: skos:Concept
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |

---

## Class EventCode
URI: skos:Concept
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---------|-----|-------|-------|------|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |
