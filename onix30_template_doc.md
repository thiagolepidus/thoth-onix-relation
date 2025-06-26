# ONIX 3.0 Template Documentation

This document provides a comprehensive guide for creating ONIX 3.0 XML files compatible with the Thoth ingestion system. The template is based on the mapper classes and sample XML structure used in this project.

## Table of Contents

1. [XML Structure Overview](#xml-structure-overview)
2. [Root Elements](#root-elements)
3. [Product Information](#product-information)
4. [Product Identifiers](#product-identifiers)
5. [Descriptive Details](#descriptive-details)
6. [Series Information](#series-information)
7. [Physical Measurements](#physical-measurements)
8. [License Information](#license-information)
9. [Title and Edition](#title-and-edition)
10. [Contributors](#contributors)
11. [Languages](#languages)
12. [Content Metrics](#content-metrics)
13. [Subject Classifications](#subject-classifications)
14. [Audience Information](#audience-information)
15. [Collateral Detail](#collateral-detail)
16. [Publishing Detail](#publishing-detail)
17. [Product Supply](#product-supply)
18. [Code Reference Tables](#code-reference-tables)
19. [Header](#header)

## XML Structure Overview

The ONIX 3.0 XML file follows a specific structure that maps to the Thoth data model:

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

## ONIXMessage
The root element that contains all ONIX data.

**Attributes:**
- `release="3.0"` - ONIX version
- `xmlns="http://ns.editeur.org/onix/3.0/reference"` - XML namespace

### Header
Contains metadata about the ONIX message sender and transmission.

```xml
<Header>
    <Sender>
        <SenderName>My Publisher</SenderName>
        <EmailAddress>contact@publisher.com</EmailAddress>
    </Sender>
    <SentDateTime>20240101T120000</SentDateTime>
</Header>
```

## Product Information

### Basic Product Elements

```xml
<Product>
    <!-- Unique identifier for this record -->
    <RecordReference>978853330227</RecordReference>
    
    <!-- Notification type: 03 = Notification confirmed on publication -->
    <NotificationType>03</NotificationType>
    
    <!-- Record source: 01 = Publisher -->
    <RecordSourceType>01</RecordSourceType>
    
    <!-- Product identifiers, descriptive details, etc. follow -->
</Product>
```

**Mapped Fields:**
- `RecordReference` - Unique record identifier
- `NotificationType` - Type of notification (typically "03")
- `RecordSourceType` - Source of the record (typically "01" for publisher)

## Product Identifiers

Multiple product identifiers can be specified:

### ISBN (Required)
```xml
<ProductIdentifier>
    <ProductIDType>15</ProductIDType>
    <IDValue>9781800649866</IDValue>
</ProductIdentifier>
```

### DOI
```xml
<ProductIdentifier>
    <ProductIDType>06</ProductIDType>
    <IDValue>10.12345/12345678</IDValue>
</ProductIdentifier>
```

### LCCN (Library of Congress Control Number)
```xml
<ProductIdentifier>
    <ProductIDType>13</ProductIDType>
    <IDValue>2017123456</IDValue>
</ProductIdentifier>
```

### OCLC Number
```xml
<ProductIdentifier>
    <ProductIDType>23</ProductIDType>
    <IDValue>1086123456</IDValue>
</ProductIdentifier>
```

**Mapping:**
- **ISBN** → `Publication.isbn` (converted to ISBN-13 format)
- **DOI** → `Work.doi` (automatically prefixed with https://doi.org/ if needed)
- **LCCN** → `Work.lccn`
- **OCLC** → `Work.oclc`

## Descriptive Details

The `DescriptiveDetail` section contains the main descriptive information about the product.

```xml
<DescriptiveDetail>
    <!-- Product composition: 00 = Single-component retail product -->
    <ProductComposition>00</ProductComposition>
    
    <!-- Product form: BC = Paperback, BB = Hardback -->
    <ProductForm>BC</ProductForm>
    
    <!-- Primary content type: 10 = Text (eye-readable) -->
    <PrimaryContentType>10</PrimaryContentType>
    
    <!-- Series, measurements, license, title, contributors, etc. -->
</DescriptiveDetail>
```

## Series Information

Series information is contained within a `Collection` element:

```xml
<Collection>
    <!-- Collection type: 10 = Issue -->
    <CollectionType>10</CollectionType>
    
    <!-- Series ID -->
    <CollectionIdentifier>
        <CollectionIDType>01</CollectionIDType>
        <IDTypeName>Series ID</IDTypeName>
        <IDValue>574e57ec-c039-4ab2-b8b9-87376c0235fc</IDValue>
    </CollectionIdentifier>
    
    <!-- ISSN -->
    <CollectionIdentifier>
        <CollectionIDType>02</CollectionIDType>
        <IDValue>11112222</IDValue>
    </CollectionIdentifier>
    
    <!-- Series URL -->
    <CollectionIdentifier>
        <CollectionIDType>01</CollectionIDType>
        <IDTypeName>Series URL</IDTypeName>
        <IDValue>https://series.url</IDValue>
    </CollectionIdentifier>
    
    <!-- Series CFP URL -->
    <CollectionIdentifier>
        <CollectionIDType>01</CollectionIDType>
        <IDTypeName>Series Call for Proposals URL</IDTypeName>
        <IDValue>https://series.cfp.url</IDValue>
    </CollectionIdentifier>
    
    <!-- Series Issue Number -->
    <CollectionSequence>
        <CollectionSequenceType>03</CollectionSequenceType>
        <CollectionSequenceNumber>1</CollectionSequenceNumber>
    </CollectionSequence>
    
    <!-- Series Name -->
    <TitleDetail>
        <TitleType>01</TitleType>
        <TitleElement>
            <TitleElementLevel>02</TitleElementLevel>
            <PartNumber>1</PartNumber>
            <TitleText>My Series Name</TitleText>
        </TitleElement>
    </TitleDetail>
</Collection>
```

**Mapping:**
- **Series ID** → `Series.seriesId`
- **Series Name** → `Series.seriesName`
- **ISSN** → `Series.issn` (automatically formatted with hyphen)
- **Series URL** → `Series.seriesUrl`
- **Series CFP URL** → `Series.seriesCfpUrl`
- **Issue Number** → `Series.issueOrdinal`

## Physical Measurements

Physical dimensions and weight can be specified in multiple units:

```xml
<!-- Height in millimeters and inches -->
<Measure>
    <MeasureType>01</MeasureType>
    <Measurement>229</Measurement>
    <MeasureUnitCode>mm</MeasureUnitCode>
</Measure>
<Measure>
    <MeasureType>01</MeasureType>
    <Measurement>9.02</Measurement>
    <MeasureUnitCode>in</MeasureUnitCode>
</Measure>

<!-- Width in millimeters and inches -->
<Measure>
    <MeasureType>02</MeasureType>
    <Measurement>152</Measurement>
    <MeasureUnitCode>mm</MeasureUnitCode>
</Measure>
<Measure>
    <MeasureType>02</MeasureType>
    <Measurement>5.98</Measurement>
    <MeasureUnitCode>in</MeasureUnitCode>
</Measure>

<!-- Depth/Thickness in millimeters and inches -->
<Measure>
    <MeasureType>03</MeasureType>
    <Measurement>20</Measurement>
    <MeasureUnitCode>mm</MeasureUnitCode>
</Measure>
<Measure>
    <MeasureType>03</MeasureType>
    <Measurement>0.79</Measurement>
    <MeasureUnitCode>in</MeasureUnitCode>
</Measure>

<!-- Weight in grams and ounces -->
<Measure>
    <MeasureType>08</MeasureType>
    <Measurement>706</Measurement>
    <MeasureUnitCode>gr</MeasureUnitCode>
</Measure>
<Measure>
    <MeasureType>08</MeasureType>
    <Measurement>24.9034</Measurement>
    <MeasureUnitCode>oz</MeasureUnitCode>
</Measure>
```

**Mapping:**
- **Height** → `Publication.heightMm` / `Publication.heightIn`
- **Width** → `Publication.widthMm` / `Publication.widthIn`
- **Depth** → `Publication.depthMm` / `Publication.depthIn`
- **Weight** → `Publication.weightG` / `Publication.weightOz`

**Measure Types:**
- `01` = Height
- `02` = Width
- `03` = Depth/Thickness
- `08` = Weight

## License Information

License information for open access publications:

```xml
<EpubLicense>
    <EpubLicenseName>Creative Commons Attribution 4.0 International license (CC BY 4.0).</EpubLicenseName>
    <EpubLicenseExpression>
        <EpubLicenseExpressionType>02</EpubLicenseExpressionType>
        <EpubLicenseExpressionLink>https://creativecommons.org/licenses/by/4.0</EpubLicenseExpressionLink>
    </EpubLicenseExpression>
</EpubLicense>
```

**Mapping:**
- **License URL** → `Work.license`

## Title and Edition

Product title and subtitle information:

```xml
<TitleDetail>
    <TitleType>01</TitleType>
    <TitleElement>
        <TitleElementLevel>01</TitleElementLevel>
        <TitleText>My Book Title</TitleText>
        <Subtitle>My Book Subtitle</Subtitle>
    </TitleElement>
</TitleDetail>

<Edition>
    <EditionNumber>2</EditionNumber>
</Edition>
```

**Mapping:**
- **Title** → `Work.title`
- **Subtitle** → `Work.subtitle`
- **Edition** → `Work.edition` (defaults to 1 if not specified)

## Contributors

Contributor information including authors, editors, and other roles:

```xml
<Contributor>
    <SequenceNumber>1</SequenceNumber>
    <ContributorRole>A01</ContributorRole>
    
    <!-- ORCID ID -->
    <NameIdentifier>
        <NameIDType>21</NameIDType>
        <IDValue>0000-0001-2345-678X</IDValue>
    </NameIdentifier>
    
    <PersonName>John Doe</PersonName>
    <NamesBeforeKey>John</NamesBeforeKey>
    <KeyNames>Doe</KeyNames>
    
    <!-- Institutional Affiliation -->
    <ProfessionalAffiliation>
        <ProfessionalPosition>Professor</ProfessionalPosition>
        
        <!-- ROR ID -->
        <AffiliationIdentifier>
            <AffiliationIDType>40</AffiliationIDType>
            <IDValue>03vek6s52</IDValue>
        </AffiliationIdentifier>
        
        <Affiliation>Harvard University</Affiliation>
    </ProfessionalAffiliation>
    
    <BiographicalNote>John Doe is a Professor at the Harvard University.</BiographicalNote>
    
    <!-- Personal Website -->
    <Website>
        <WebsiteRole>06</WebsiteRole>
        <WebsiteDescription>Own website</WebsiteDescription>
        <WebsiteLink>https://john.doe.org/</WebsiteLink>
    </Website>
</Contributor>
```

**Mapping:**
- **Name** → `Contributor.firstName`, `Contributor.lastName`, `Contributor.fullName`
- **ORCID** → `Contributor.orcid` (automatically prefixed with https://orcid.org/)
- **Role** → `Contribution.contributionType`
- **Sequence** → `Contribution.contributionOrdinal`, `Contribution.mainContribution`
- **Biography** → `Contribution.biography`
- **Website** → `Contributor.website`
- **Affiliation** → `Affiliation.institutionName`, `Affiliation.affiliationPosition`
- **ROR ID** → `Affiliation.institutionRor`

**Contributor Role Codes:**
- `A01` = Author
- `B01` = Editor
- `B06` = Translator
- `A12` = Illustrator
- `A13` = Photographer
- `A15` = Preface by
- `A23` = Foreword by
- `A30` = Software by
- `A32` = Contributions by
- `A34` = Indexer
- `A51` = Research by
- `B25` = Music editor

## Languages

Language information for the work:

```xml
<!-- Original Language -->
<Language>
    <LanguageRole>01</LanguageRole>
    <LanguageCode>eng</LanguageCode>
</Language>
```

**Mapping:**
- **Language Code** → `Language.languageCode` (converted to ISO 639-2 format)
- **Language Role** → `Language.languageRelation`

**Language Role Codes:**
- `01` = Language of text (original)
- `02` = Translated from

## Content Metrics

Various content metrics can be specified:

```xml
<!-- Page Count -->
<Extent>
    <ExtentType>00</ExtentType>
    <ExtentValue>284</ExtentValue>
    <ExtentUnit>03</ExtentUnit>
</Extent>

<!-- Bibliography note -->
<IllustrationsNote>Includes bibliographical references and index.</IllustrationsNote>

<!-- Image count -->
<AncillaryContent>
    <AncillaryContentType>09</AncillaryContentType>
    <Number>16</Number>
</AncillaryContent>

<!-- Table count -->
<AncillaryContent>
    <AncillaryContentType>11</AncillaryContentType>
    <Number>5</Number>
</AncillaryContent>

<!-- Audio count -->
<AncillaryContent>
    <AncillaryContentType>19</AncillaryContentType>
    <Number>1</Number>
</AncillaryContent>

<!-- Video count -->
<AncillaryContent>
    <AncillaryContentType>00</AncillaryContentType>
    <AncillaryContentDescription>Videos</AncillaryContentDescription>
    <Number>4</Number>
</AncillaryContent>
```

**Mapping:**
- **Page Count** → `Work.pageCount`
- **Bibliography Note** → `Work.bibliographyNote`
- **Image Count** → `Work.imageCount`
- **Table Count** → `Work.tableCount`
- **Audio Count** → `Work.audioCount`
- **Video Count** → `Work.videoCount`

**AncillaryContent Type Codes:**
- `09` = Images/Illustrations
- `11` = Tables
- `19` = Audio content
- `00` = Other (use with description)

## Subject Classifications

Multiple subject classification schemes can be used:

```xml
<!-- Library of Congress Classification -->
<Subject>
    <MainSubject />
    <SubjectSchemeIdentifier>04</SubjectSchemeIdentifier>
    <SubjectCode>BD183</SubjectCode>
</Subject>

<!-- BISAC Subject Heading -->
<Subject>
    <MainSubject />
    <SubjectSchemeIdentifier>10</SubjectSchemeIdentifier>
    <SubjectCode>1.1.2.2.0.0.0</SubjectCode>
</Subject>

<!-- BIC Subject Category -->
<Subject>
    <MainSubject />
    <SubjectSchemeIdentifier>12</SubjectSchemeIdentifier>
    <SubjectCode>1D</SubjectCode>
</Subject>

<!-- Keywords -->
<Subject>
    <MainSubject />
    <SubjectSchemeIdentifier>20</SubjectSchemeIdentifier>
    <SubjectHeadingText>Interest-Relative Epistemology</SubjectHeadingText>
</Subject>

<!-- Thema Subject Category -->
<Subject>
    <MainSubject />
    <SubjectSchemeIdentifier>93</SubjectSchemeIdentifier>
    <SubjectCode>1A</SubjectCode>
</Subject>

<!-- Custom Subject -->
<Subject>
    <MainSubject />
    <SubjectSchemeIdentifier>B2</SubjectSchemeIdentifier>
    <SubjectHeadingText>Philosophy</SubjectHeadingText>
</Subject>
```

**Mapping:**
- **Subject Type** → `Subject.subjectType`
- **Subject Code/Text** → `Subject.subjectCode`

**Subject Scheme Codes:**
- `04` = Library of Congress Classification
- `10` = BISAC Subject Heading
- `12` = BIC Subject Category
- `20` = Keywords
- `93` = Thema subject category
- `B2` = Custom subject scheme

## Audience Information

Target audience specification:

```xml
<Audience>
    <AudienceCodeType>01</AudienceCodeType>
    <AudienceCodeValue>06</AudienceCodeValue>
</Audience>
```

**Audience Code Types:**
- `01` = ONIX Adult audience rating

**Audience Code Values:**
- `06` = Professional and scholarly

## Collateral Detail

Additional descriptive content including abstracts, table of contents, and cover images:

```xml
<CollateralDetail>
    <!-- Short abstract -->
    <TextContent>
        <TextType>02</TextType>
        <ContentAudience>00</ContentAudience>
        <Text>This is the short abstract of my book.</Text>
    </TextContent>
    
    <!-- Long abstract -->
    <TextContent>
        <TextType>03</TextType>
        <ContentAudience>00</ContentAudience>
        <Text>This is the long abstract of my book.</Text>
    </TextContent>
    
    <!-- Alternative long abstract -->
    <TextContent>
        <TextType>30</TextType>
        <ContentAudience>00</ContentAudience>
        <Text>This is the long abstract of my book.</Text>
    </TextContent>
    
    <!-- Table of Contents -->
    <TextContent>
        <TextType>04</TextType>
        <ContentAudience>00</ContentAudience>
        <Text>1. Introduction;2. List of tables;3. References</Text>
    </TextContent>
    
    <!-- Open Access Notice -->
    <TextContent>
        <TextType>20</TextType>
        <ContentAudience>00</ContentAudience>
        <Text language="eng">Open Access</Text>
    </TextContent>
    
    <!-- General Note -->
    <TextContent>
        <TextType>13</TextType>
        <ContentAudience>00</ContentAudience>
        <Text>Links to additional resources are available from my publisher's website.</Text>
    </TextContent>
    
    <!-- Cover Image -->
    <SupportingResource>
        <ResourceContentType>01</ResourceContentType>
        <ContentAudience>00</ContentAudience>
        <ResourceMode>03</ResourceMode>
        <ResourceVersion>
            <ResourceForm>02</ResourceForm>
            <ResourceLink>https://example.com/cover.jpg</ResourceLink>
        </ResourceVersion>
        <ResourceFeature>
            <ResourceFeatureType>02</ResourceFeatureType>
            <FeatureNote>Cover image caption</FeatureNote>
        </ResourceFeature>
    </SupportingResource>
</CollateralDetail>
```

**Mapping:**
- **Short Abstract** → `Work.shortAbstract`
- **Long Abstract** → `Work.longAbstract`
- **Table of Contents** → `Work.toc`
- **General Note** → `Work.generalNote`
- **Cover URL** → `Work.coverUrl` (validated for image extensions)
- **Cover Caption** → `Work.coverCaption`

**Text Type Codes:**
- `02` = Short description/annotation
- `03` = Description
- `04` = Table of contents
- `13` = General note
- `20` = Open access statement
- `30` = Abstract

## Publishing Detail

Publishing information including dates, publisher, and copyright:

```xml
<PublishingDetail>
    <!-- Publishing status -->
    <PublishingStatus>04</PublishingStatus>
    
    <!-- Publication date -->
    <PublishingDate>
        <PublishingDateRole>01</PublishingDateRole>
        <Date>20240315</Date>
    </PublishingDate>
    
    <!-- Withdrawn date (if applicable) -->
    <PublishingDate>
        <PublishingDateRole>13</PublishingDateRole>
        <Date>20241201</Date>
    </PublishingDate>
    
    <!-- Place of publication -->
    <CityOfPublication>New York</CityOfPublication>
    
    <!-- Publisher -->
    <Publisher>
        <PublishingRole>01</PublishingRole>
        <PublisherName>Academic Press</PublisherName>
        
        <!-- Publisher website -->
        <Website>
            <WebsiteRole>02</WebsiteRole>
            <WebsiteLink>https://academicpress.com/book/123</WebsiteLink>
        </Website>
    </Publisher>
    
    <!-- Funding information -->
    <Publisher>
        <PublishingRole>16</PublishingRole>
        <PublisherName>National Science Foundation</PublisherName>
        
        <!-- Funder ROR ID -->
        <PublisherIdentifier>
            <PublisherIDType>40</PublisherIDType>
            <IDValue>021nxhr62</IDValue>
        </PublisherIdentifier>
        
        <!-- Funding details -->
        <Funding>
            <FundingIdentifier>
                <FundingIDType>01</FundingIDType>
                <IDTypeName>programname</IDTypeName>
                <IDValue>Research Grant Program</IDValue>
            </FundingIdentifier>
            
            <FundingIdentifier>
                <FundingIDType>01</FundingIDType>
                <IDTypeName>projectname</IDTypeName>
                <IDValue>Advanced Research Project</IDValue>
            </FundingIdentifier>
            
            <FundingIdentifier>
                <FundingIDType>01</FundingIDType>
                <IDTypeName>projectshortname</IDTypeName>
                <IDValue>ARP</IDValue>
            </FundingIdentifier>
            
            <FundingIdentifier>
                <FundingIDType>01</FundingIDType>
                <IDTypeName>grantnumber</IDTypeName>
                <IDValue>NSF-2023-001</IDValue>
            </FundingIdentifier>
            
            <FundingIdentifier>
                <FundingIDType>01</FundingIDType>
                <IDTypeName>jurisdiction</IDTypeName>
                <IDValue>United States</IDValue>
            </FundingIdentifier>
        </Funding>
    </Publisher>
    
    <!-- Copyright information -->
    <CopyrightStatement>
        <CopyrightOwner>
            <PersonName>John Doe</PersonName>
        </CopyrightOwner>
    </CopyrightStatement>
</PublishingDetail>
```

**Mapping:**
- **Work Status** → `Work.workStatus`
- **Publication Date** → `Work.publicationDate`
- **Withdrawn Date** → `Work.withdrawnDate`
- **Place** → `Work.place`
- **Landing Page** → `Work.landingPage`
- **Copyright Holder** → `Work.copyrightHolder`
- **Funding Institution** → `Funding.institutionName`
- **Funding ROR** → `Funding.institutionRor`
- **Program** → `Funding.program`
- **Project Name** → `Funding.projectName`
- **Project Short Name** → `Funding.projectShortName`
- **Grant Number** → `Funding.grantNumber`
- **Jurisdiction** → `Funding.jurisdiction`

**Publishing Status Codes:**
- `01` = Cancelled
- `02` = Forthcoming
- `03` = Postponed indefinitely
- `04` = Active
- `08` = Superseded
- `11` = Withdrawn

**Publishing Date Role Codes:**
- `01` = Publication date
- `13` = Withdrawn date

**Publishing Role Codes:**
- `01` = Publisher
- `16` = Funding body

## Product Supply

Information about availability and pricing:

```xml
<ProductSupply>
    <SupplyDetail>
        <!-- Supply availability -->
        <ProductAvailability>20</ProductAvailability>
        
        <!-- Supplier information -->
        <Supplier>
            <SupplierRole>01</SupplierRole>
            <SupplierName>Academic Press</SupplierName>
            
            <!-- Product page -->
            <Website>
                <WebsiteRole>02</WebsiteRole>
                <WebsiteLink>https://academicpress.com/book/123</WebsiteLink>
            </Website>
            
            <!-- Full text URL -->
            <Website>
                <WebsiteRole>29</WebsiteRole>
                <WebsiteLink>https://academicpress.com/book/123.pdf</WebsiteLink>
            </Website>
        </Supplier>
        
        <!-- Pricing information -->
        <Price>
            <PriceType>02</PriceType>
            <CurrencyCode>USD</CurrencyCode>
            <PriceAmount>39.95</PriceAmount>
        </Price>
    </SupplyDetail>
</ProductSupply>
```

**Mapping:**
- **Landing Page** → `Location.landingPage`
- **Full Text URL** → `Location.fullTextUrl`
- **Platform** → `Location.locationPlatform`
- **Currency** → `Price.currencyCode`
- **Price** → `Price.unitPrice`

**Product Availability Codes:**
- `20` = Available

**Website Role Codes:**
- `02` = Publisher's website for specified work
- `29` = Full content package URL

## Code Reference Tables

### Product ID Type Codes
- `06` = DOI
- `13` = LCCN
- `15` = ISBN-13
- `23` = OCLC number

### Collection ID Type Codes
- `01` = Proprietary
- `02` = ISSN

### Name ID Type Codes
- `21` = ORCID

### Affiliation ID Type Codes
- `40` = ROR ID

### Measure Type Codes
- `01` = Height
- `02` = Width
- `03` = Depth/Thickness
- `08` = Weight

### Measure Unit Codes
- `mm` = Millimeters
- `in` = Inches
- `gr` = Grams
- `oz` = Ounces

### Product Form Codes
- `BC` = Paperback
- `BB` = Hardback
- `EA` = Digital download
- `EB` = Digital online
- `EC` = Digital download and online
- `ED` = Digital download, online and print

### Product Form Detail Codes (Digital)
- `E100` = FictionBook
- `E101` = EPUB
- `E104` = Microsoft Word Document
- `E105` = HTML
- `E107` = PDF
- `E113` = OEB
- `E116` = Amazon Kindle
- `E127` = Mobipocket
- `A103` = MP3
- `A104` = WAV

### Text Type Codes
- `02` = Short description/annotation
- `03` = Description
- `04` = Table of contents
- `13` = General note
- `20` = Open access statement
- `30` = Abstract

### Resource Content Type Codes
- `01` = Front cover

### Resource Form Codes
- `02` = Downloadable file

### Extent Type Codes
- `00` = Main content page count

### Extent Unit Codes
- `03` = Pages

### Collection Type Codes
- `10` = Issue

### Collection Sequence Type Codes
- `03` = Issue number

### Title Type Codes
- `01` = Distinctive title

### Title Element Level Codes
- `01` = Product
- `02` = Collection level

### Language Role Codes
- `01` = Language of text
- `02` = Original language

### Audience Code Type Codes
- `01` = ONIX Adult audience rating

### Content Audience Codes
- `00` = General/trade

### Website Role Codes
- `02` = Publisher's website: web page for specified work
- `06` = Author's own website
- `29` = Full content package URL

### Resource Feature Type Codes
- `02` = Caption

### Funding ID Type Codes
- `01` = Proprietary

### Publisher ID Type Codes
- `40` = ROR ID

## Validation Rules

1. **Required Fields:**
   - RecordReference
   - ISBN (ProductIDType 15)
   - Title
   - At least one contributor with role A01 (Author)

2. **URL Validation:**
   - Cover URLs must have valid image extensions (jpg, jpeg, png, gif, webp, svg)
   - DOI URLs are automatically prefixed if not already present
   - ORCID URLs are automatically prefixed if not already present

3. **Format Validation:**
   - ISBN is validated and converted to ISBN-13 format
   - ISSN is formatted with hyphen if needed
   - Dates should be in YYYYMMDD format

4. **Namespace:**
   - All elements must use the correct ONIX 3.0 namespace
   - XPath expressions are relative to the Product element

This template provides a comprehensive structure for creating ONIX 3.0 XML files that will be correctly parsed and mapped to the Thoth data model using the mapper classes in this project.
