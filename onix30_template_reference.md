# ONIX 3.0 Template Reference

- [ONIXMessage](#onixmessage)
  - [Header](#header)
    - [Sender](#sender)
    - [SentDateTime](#sentdatetime)
  - [Product](#product)
    - [RecordReference](#recordreference)
    - [NotificationType](#notificationtype)
    - [RecordSourceType](#recordsourcetype)
    - [ProductIdentifier](#productidentifier)
    - [DescriptiveDetail](#descriptivedetail)
      - [ProductComposition](#productcomposition)
      - [ProductForm](#productform)
      - [ProductFormDetail](#productformdetail)
      - [PrimaryContentType](#primarycontenttype)
      - [Collection](#collection)
        - [CollectionType](#collectiontype)
        - [CollectionIdentifier](#collectionidentifier)
        - [CollectionSequence](#collectionsequence)
        - [TitleDetail](#titledetail)
          - [TitleType](#titletype)
          - [TitleElement](#titleelement)
      - [Measure](#measure)
      - [EpubLicense](#epublicense)
        - [EpubLicenseName](#epublicensename)
        - [EpubLicenseExpression](#epublicenseexpression)
      - [TitleDetail](#titledetail-1)
        - [TitleType](#titletype-1)
        - [TitleElement](#titleelement-1)
      - [Contributor](#contributor)
        - [SequenceNumber](#sequencenumber)
        - [ContributorRole](#contributorrole)
        - [NameIdentifier](#nameidentifier)
        - [PersonName](#personname)
        - [NamesBeforeKey](#namesbeforekey)
        - [KeyNames](#keynames)
        - [ProfessionalAffiliation](#professionalaffiliation)
          - [ProfessionalPosition](#professionalposition)
          - [Affiliation](#affiliation)
        - [BiographicalNote](#biographicalnote)
        - [Website](#website)
      - [EditionNumber](#editionnumber)
      - [Language](#language)
      - [Extent](#extent)
      - [IllustrationsNote](#illustrationsnote)
      - [AncillaryContent](#ancillarycontent)
      - [Subject](#subject)
      - [Audience](#audience)
    - [CollateralDetail](#collateraldetail)
      - [TextContent](#textcontent)
      - [SupportingResource](#supportingresource)
        - [ResourceContentType](#resourcecontenttype)
        - [ContentAudience](#contentaudience)
        - [ResourceMode](#resourcemode)
        - [ResourceFeature](#resourcefeature)
        - [ResourceVersion](#resourceversion)
    - [ContentDetail](#contentdetail)
      - [ContentItem](#contentitem)
        - [LevelSequenceNumber](#levelsequencenumber)
        - [TextItem](#textitem)
          - [TextItemType](#textitemtype)
          - [TextItemIdentifier](#textitemidentifier)
          - [PageRun](#pagerun)
          - [NumberOfPages](#numberofpages)
        - [ComponentTypeName](#componenttypename)
    - [PublishingDetail](#publishingdetail)
      - [Imprint](#imprint)
        - [ImprintIdentifier](#imprintidentifier)
        - [ImprintName](#imprintname)
      - [Publisher](#publisher)
        - [PublishingRole](#publishingrole)
        - [PublisherIdentifier](#publisheridentifier)
        - [PublisherName](#publishername)
        - [Funding](#funding)
          - [FundingIdentifier](#fundingidentifier)
        - [Website](#website-1)
      - [CityOfPublication](#cityofpublication)
      - [PublishingStatus](#publishingstatus)
      - [PublishingDate](#publishingdate)
      - [CopyrightStatement](#copyrightstatement)
      - [SalesRights](#salesrights)
    - [RelatedMaterial](#relatedmaterial)
      - [RelatedWork](#relatedwork)
        - [ProductRelationCode](#productrelationcode)
        - [ProductIdentifier](#productidentifier-1)
      - [RelatedProduct](#relatedproduct)
        - [ProductRelationCode](#productrelationcode-1)
        - [ProductIdentifier](#productidentifier-2)
    - [ProductSupply](#productsupply)
      - [Market](#market)
      - [SupplyDetail](#supplydetail)
        - [Supplier](#supplier)
          - [SupplierRole](#supplierrole)
          - [SupplierName](#suppliername)
          - [Website](#website-2)
        - [ProductAvailability](#productavailability)
        - [SupplyDate](#supplydate)
        - [Price](#price)
          - [PriceType](#pricetype)
          - [PriceAmount](#priceamount)
          - [CurrencyCode](#currencycode)
          - [Territory](#territory)

## ONIXMessage
`Mandatory`

The root element that contains all ONIX data.

The ONIX 3.0 XML file follows a specific structure:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ONIXMessage release="3.0" xmlns="http://ns.editeur.org/onix/3.0/reference">
  <Header>
    <!-- Header information -->
  </Header>
  <Product>
    <!-- Product information -->
  </Product>
</ONIXMessage>
```

**Attributes:**
- `release="3.0"` - ONIX version
- `xmlns="http://ns.editeur.org/onix/3.0/reference"` - XML namespace

## Header
`Mandatory`

Contains information about the file.

```xml
<Header>
  <Sender>
    <!-- Sender information -->
  </Sender>
  <SentDateTime>...</SentDateTime>
</Header>
```

### Sender
`Mandatory`

Information about the entity sending the file.

```xml
<Sender>
  <SenderName>My Publisher</SenderName>
  <EmailAddress>contact@publisher.com</EmailAddress>
</Sender>
```

**Sub-elements:**
- `SenderName` - Sender entity name
- `EmailAddress` - Sender entity contact e-mail

### SentDateTime

Specifies the date and time when the file is being sent.

```xml
<SentDateTime>20240101T120000</SentDateTime>
```

## Product
`Mandatory, Repeatable`

Information about each publication.

### RecordReference
`Mandatory`

Unique identifier for the record. ISBN recommended.

```xml
<RecordReference>9789800000001</RecordReference>
```

### NotificationType
`Mandatory`

Indicates the type of notification or update which you are sending. Default 03 (Notification confirmed on publication).

```xml
<NotificationType>03</NotificationType>
```

### RecordSourceType
`Mandatory`

Indicates the type of source which has issued the record. Default 01 (Publisher).

```xml
<RecordSourceType>01</RecordSourceType>
```

### ProductIdentifier
`Optional, Repeatable`

Define an identifier of the organization which is the source of the record.

**ISBN-13**
```xml
<ProductIdentifier>
    <ProductIDType>15</ProductIDType>
    <IDValue>9781800649866</IDValue>
</ProductIdentifier>
```

**DOI**
```xml
<ProductIdentifier>
    <ProductIDType>06</ProductIDType>
    <IDValue>10.12345/12345678</IDValue>
</ProductIdentifier>
```

**LCCN (Library of Congress Control Number)**
```xml
<ProductIdentifier>
    <ProductIDType>13</ProductIDType>
    <IDValue>2017123456</IDValue>
</ProductIdentifier>
```

**OCLC Number**
```xml
<ProductIdentifier>
    <ProductIDType>23</ProductIDType>
    <IDValue>1086123456</IDValue>
</ProductIdentifier>
```

**Sub-elements**:
- `ProductIDType` - ONIX code specifying the Product Identifier type provided.
  - `05`: DOI
  - `13`: LCCN
  - `15`: ISBN-13
  - `23`: OCLC
- `IDValue` - The identifier value of the type specified in the `ProductIDType` element.

### DescriptiveDetail
`Mandatory`

Describes the product form and metadata such as title, content description, and authorship.

#### ProductComposition

#### ProductForm

#### ProductFormDetail

#### PrimaryContentType

#### Collection

##### CollectionType

##### CollectionIdentifier

##### CollectionSequence

##### TitleDetail

###### TitleType

###### TitleElement

#### Measure

#### EpubLicense

##### EpubLicenseName

##### EpubLicenseExpression

#### TitleDetail

##### TitleType

##### TitleElement

#### Contributor

##### SequenceNumber

##### ContributorRole

##### NameIdentifier

##### PersonName

##### NamesBeforeKey

##### KeyNames

##### ProfessionalAffiliation

###### ProfessionalPosition

###### Affiliation

##### BiographicalNote

##### Website

#### EditionNumber

#### Language

#### Extent

#### IllustrationsNote

#### AncillaryContent

#### Subject

#### Audience

### CollateralDetail

#### TextContent

#### SupportingResource

##### ResourceContentType

##### ContentAudience

##### ResourceMode

##### ResourceFeature

##### ResourceVersion

### ContentDetail

#### ContentItem

##### LevelSequenceNumber

##### TextItem

###### TextItemType

###### TextItemIdentifier

###### PageRun

###### NumberOfPages

##### ComponentTypeName

### PublishingDetail

#### Imprint

##### ImprintIdentifier

##### ImprintName

#### Publisher

##### PublishingRole

##### PublisherIdentifier

##### PublisherName

##### Funding

###### FundingIdentifier

##### Website

#### CityOfPublication

#### PublishingStatus

#### PublishingDate

#### CopyrightStatement

#### SalesRights

### RelatedMaterial

#### RelatedWork

##### ProductRelationCode

##### ProductIdentifier

#### RelatedProduct

##### ProductRelationCode

##### ProductIdentifier

### ProductSupply

#### Market

#### SupplyDetail

##### Supplier

###### SupplierRole

###### SupplierName

###### Website

##### ProductAvailability

##### SupplyDate

##### Price

###### PriceType

###### PriceAmount

###### CurrencyCode

###### Territory
