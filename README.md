# Application Profile (Normative)

## Klasser
TradeAgreement, EconomicOperator, Identifier, IdentifierType, PaymentTerms, MonetaryAmount, PaymentDueCondition, DeliveryTerms, DeliveryLocation, Address, CurrencyCode, IncotermCode, EventCode

---

## Namespaces

| Prefix | Namespace |
|-------|----------|
| ebwv | https://w3id.org/ebwv# |
| xsd | http://www.w3.org/2001/XMLSchema# |
| skos | http://www.w3.org/2004/02/skos/core# |

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

  %% Associations
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

## Class IdentifierType
URI: ebwv:IdentifierType
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---|---|---|---|---|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |

---

## Class CurrencyCode
URI: skos:Concept
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---|---|---|---|---|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |

---

## Class IncotermCode
URI: skos:Concept
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---|---|---|---|---|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |

---

## Class EventCode
URI: skos:Concept
Requirement Level: Mandatory

| Property | URI | Range | Mult. | Req. |
|---|---|---|---|---|
| code | skos:prefLabel | xsd:string | 1 | Mandatory |
