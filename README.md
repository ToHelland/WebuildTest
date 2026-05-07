# Application Profile

## Innholdsfortegnelse
- #application-profile
  - #namespaces
  - #conceptual-model
  - #class-tradeagreement
  - #class-economicoperator
  - #class-identifier
  - #class-identifiertype
  - #class-paymentterms
  - #class-monetaryamount
  - #class-paymentduecondition
  - #class-deliveryterms
  - #class-deliverylocation
  - #class-address
  - #class-currencycode
  - #class-incotermcode
  - #class-eventcode

---

## Namespaces

| Prefix | Namespace |
|-------|----------|
| ebwv | https://w3id.org/ebwv# |
| xsd | http://www.w3.org/2001/XMLSchema# |
| skos | http://www.w3.org/2004/02/skos/core# |

---

## Conceptual Model

```mermaid
classDiagram
    class TradeAgreement {
        identifier : xsd:string [0..1]
        agreementDate : xsd:dateTime [1]
        buyer : EconomicOperator [1]
        supplier : EconomicOperator [1]
        hasPaymentTerms : PaymentTerms [1]
        hasDeliveryTerms : DeliveryTerms [1]
    }

    class EconomicOperator {
        identifier : Identifier [1]
    }

    class Identifier {
        value : xsd:string [1]
        type : IdentifierType [1..*]
    }

    class IdentifierType {
        code : skos:prefLabel [1]
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
        (skos:Concept)
        code : skos:prefLabel [1]
    }

    class IncotermCode {
        (skos:Concept)
        code : skos:prefLabel [1]
    }

    class EventCode {
        (skos:Concept)
        code : skos:prefLabel [1]
    }

    TradeAgreement --> EconomicOperator : buyer
    TradeAgreement --> EconomicOperator : supplier
    TradeAgreement --> PaymentTerms : hasPaymentTerms
    TradeAgreement --> DeliveryTerms : hasDeliveryTerms
    PaymentTerms --> MonetaryAmount : transactionAmount
    PaymentTerms --> PaymentDueCondition : hasPaymentDueCondition
    DeliveryTerms --> DeliveryLocation : deliveryLocation
    DeliveryLocation --> Address : address
