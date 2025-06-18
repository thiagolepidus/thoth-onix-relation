# ONIX 3.0 to Thoth Model Mapping Reference

This document provides a comprehensive mapping between ONIX 3.0 XML elements and Thoth model attributes based on the mapper classes in this project.

## Work Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `workStatus` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:PublishingStatus` | - | Maps ONIX codes to Thoth work status constants | 01→CANCELLED, 02→FORTHCOMING, 03→POSTPONED_INDEFINITELY, 04→ACTIVE, 08→SUPERSEDED, 11→WITHDRAWN |
| `title` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:TitleDetail/onix:TitleElement/onix:TitleText` | - | None | Main work title |
| `subtitle` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:TitleDetail/onix:TitleElement/onix:Subtitle` | - | None | Work subtitle |
| `edition` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Edition/onix:EditionNumber` | 1 | None | Edition number, defaults to 1 if not specified |
| `publicationDate` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:PublishingDate[onix:PublishingDateRole="01"]/onix:Date` | - | None | Publication date in YYYYMMDD format |
| `withdrawnDate` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:PublishingDate[onix:PublishingDateRole="13"]/onix:Date` | - | None | Date work was withdrawn |
| `place` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:CityOfPublication` | - | None | Place of publication |
| `coverUrl` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:SupportingResource[onix:ResourceContentType="01"]/onix:ResourceVersion[onix:ResourceForm="02"]/onix:ResourceLink` | - | Validates URL and image extension | Must be valid URL with image extension |
| `coverCaption` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:SupportingResource/onix:ResourceFeature[onix:ResourceFeatureType="02"]/onix:FeatureNote` | - | None | Cover image caption |
| `doi` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="06"]/onix:IDValue` | - | Prepends https://doi.org/ if not present | Digital Object Identifier |
| `lccn` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="13"]/onix:IDValue` | - | None | Library of Congress Control Number |
| `oclc` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="23"]/onix:IDValue` | - | None | OCLC number |
| `pageCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Extent/onix:ExtentValue` | - | None | Total page count |
| `imageCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentType="09"]/onix:Number` | - | None | Number of images |
| `tableCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentType="11"]/onix:Number` | - | None | Number of tables |
| `audioCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentType="19"]/onix:Number` | - | None | Number of audio elements |
| `videoCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentDescription="Videos"]/onix:Number` | - | None | Number of video elements |
| `license` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:EpubLicense/onix:EpubLicenseExpression[onix:EpubLicenseExpressionType="02"]/onix:EpubLicenseExpressionLink` | - | None | License URL |
| `copyrightHolder` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:CopyrightStatement/onix:CopyrightOwner/onix:PersonName` | - | None | Copyright holder name |
| `landingPage` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher/onix:Website[onix:WebsiteRole="02"]/onix:WebsiteLink` | - | None | Work landing page URL |
| `shortAbstract` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="02"]/onix:Text` | - | None | Short description/abstract |
| `longAbstract` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="03"]/onix:Text \| /onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="30"]/onix:Text` | - | None | Long description/abstract |
| `generalNote` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="13"]/onix:Text` | - | None | General notes about the work |
| `bibliographyNote` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:IllustrationsNote` | - | None | Notes about bibliography/illustrations |
| `toc` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="04"]/onix:Text` | - | None | Table of contents |

## Publication Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `publicationType` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:ProductForm` | - | Maps ONIX product form codes to publication types | BC→PAPERBACK, BB→HARDBACK, E107→PDF, E105→HTML, E113→XML, E101→EPUB, E127→MOBI, E116→AZW3, E104→DOCX, E100→FICTION_BOOK, A103→MP3, A104→WAV |
| `isbn` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="15"]/onix:IDValue` | - | Validates and converts to ISBN-13 format | Uses Biblys\Isbn library for validation |
| `heightMm` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="01" and onix:MeasureUnitCode="mm"]/onix:Measurement` | - | None | Height in millimeters |
| `heightIn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="01" and onix:MeasureUnitCode="in"]/onix:Measurement` | - | None | Height in inches |
| `widthMm` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="02" and onix:MeasureUnitCode="mm"]/onix:Measurement` | - | None | Width in millimeters |
| `widthIn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="02" and onix:MeasureUnitCode="in"]/onix:Measurement` | - | None | Width in inches |
| `depthMm` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="03" and onix:MeasureUnitCode="mm"]/onix:Measurement` | - | None | Depth/thickness in millimeters |
| `depthIn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="03" and onix:MeasureUnitCode="in"]/onix:Measurement` | - | None | Depth/thickness in inches |
| `weightG` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="08" and onix:MeasureUnitCode="gr"]/onix:Measurement` | - | None | Weight in grams |
| `weightOz` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="08" and onix:MeasureUnitCode="oz"]/onix:Measurement` | - | None | Weight in ounces |

## Contributor Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `firstName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:NamesBeforeKey \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | - | Extracts first name from inverted name format | If comma present, takes part after comma |
| `lastName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:KeyNames \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | - | Extracts last name from inverted name format | If comma present, takes part before comma |
| `fullName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonName \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | - | Reverses inverted name format | If comma present, reverses order and joins with space |
| `orcid` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:NameIdentifier[onix:NameIDType="21"]/onix:IDValue` | - | Prepends https://orcid.org/ if not present | ORCID identifier |
| `website` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:Website[onix:WebsiteRole="06"]/onix:WebsiteLink` | - | None | Contributor's website |

## Contribution Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `contributionType` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ContributorRole` | - | Maps ONIX contributor role codes to contribution types | A01→AUTHOR, B01→EDITOR, B06→TRANSLATOR, A13→PHOTOGRAPHER, A12→ILLUSTRATOR, B25→MUSIC_EDITOR, A23→FOREWORD_BY, A15→PREFACE_BY, A30→SOFTWARE_BY, A51→RESEARCH_BY, A32→CONTRIBUTIONS_BY, A34→INDEXER |
| `mainContribution` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:SequenceNumber` | - | Returns true if sequence number is "1" | Indicates primary contributor |
| `biography` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:BiographicalNote` | - | None | Contributor biography |
| `firstName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:NamesBeforeKey \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | - | Same as Contributor firstName | Inherited from contributor |
| `lastName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:KeyNames \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | - | Same as Contributor lastName | Inherited from contributor |
| `fullName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonName \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | - | Same as Contributor fullName | Inherited from contributor |
| `contributionOrdinal` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:SequenceNumber` | - | None | Order of contribution |

## Affiliation Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `affiliationPosition` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ProfessionalAffiliation/onix:ProfessionalPosition` | - | None | Position/role within institution |
| `institutionName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ProfessionalAffiliation/onix:Affiliation` | - | None | Name of affiliated institution |
| `institutionRor` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ProfessionalAffiliation/onix:AffiliationIdentifier[onix:AffiliationIDType="40"]/onix:IDValue` | - | Prepends https://ror.org/ if not present | ROR (Research Organization Registry) ID |

## Location Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `landingPage` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:Website[onix:WebsiteRole="02"]/onix:WebsiteLink \| /onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher/onix:Website[onix:WebsiteRole="02"]/onix:WebsiteLink \| /onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:Website[onix:WebsiteRole="29"]/onix:WebsiteLink` | - | Complex logic to determine appropriate landing page | Falls back through supplier, publisher, and file URLs |
| `fullTextUrl` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:Website[onix:WebsiteRole="29"]/onix:WebsiteLink` | - | Complex logic to find downloadable content | Validates file URLs and falls back to resource links |
| `locationPlatform` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:SupplierName` | - | Maps supplier names to platform constants | Includes mappings for Project MUSE, OAPEN, DOAB, JSTOR, etc. |

## Price Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `currencyCode` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Price/onix:CurrencyCode` | - | None | ISO currency code |
| `unitPrice` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Price/onix:PriceAmount` | - | None | Price amount |

## Language Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `languageCode` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Language/onix:LanguageCode` | - | Converts to ISO 639-2 format with language name | Returns format: "CODE\|Name" |
| `languageRelation` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Language/onix:LanguageRole` | - | Maps language role codes | 01→ORIGINAL, 02→TRANSLATED_FROM |

## Subject Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `subjectType` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Subject/onix:SubjectSchemeIdentifier` | - | Maps subject scheme codes | 04→LCC, 10→BISAC, 12→BIC, 20→KEYWORD, 93→THEMA, B2→CUSTOM |
| `subjectCode` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Subject/onix:SubjectCode \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Subject/onix:SubjectHeadingText` | - | None | Subject classification code or text |

## Series Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `seriesId` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="01" and onix:IDTypeName="Series ID"]/onix:IDValue` | - | None | Series identifier |
| `seriesName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:TitleDetail/onix:TitleElement/onix:TitleText` | - | None | Series name/title |
| `issn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="02"]/onix:IDValue` | - | Formats ISSN with hyphen if needed | Adds hyphen between 4th and 5th characters |
| `seriesUrl` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="01" and onix:IDTypeName="Series URL"]/onix:IDValue` | - | None | Series website URL |
| `seriesCfpUrl` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="01" and onix:IDTypeName="Series Call for Proposals URL"]/onix:IDValue` | - | None | Series call for proposals URL |
| `issueOrdinal` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionSequence[onix:CollectionSequenceType="03"]/onix:CollectionSequenceNumber` | - | None | Issue number within series |

## Funding Model Mappings

| Thoth Attribute | ONIX XPath | Default Value | Transformation | Notes |
|---|---|---|---|---|
| `institutionName` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:PublisherName` | - | None | Funding institution name |
| `institutionRor` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:PublisherIdentifier[onix:PublisherIDType="40"]/onix:IDValue` | - | Prepends https://ror.org/ if not present | ROR ID of funding institution |
| `program` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="programname"]/onix:IDValue` | - | None | Funding program name |
| `projectName` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="projectname"]/onix:IDValue` | - | None | Project name |
| `projectShortName` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="projectshortname"]/onix:IDValue` | - | None | Project short name/acronym |
| `grantNumber` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="grantnumber"]/onix:IDValue` | - | None | Grant number |
| `jurisdiction` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="jurisdiction"]/onix:IDValue` | - | None | Funding jurisdiction |

## ONIX Code Mappings

### Work Status Codes
- `01` → `WORK_STATUS_CANCELLED`
- `02` → `WORK_STATUS_FORTHCOMING`
- `03` → `WORK_STATUS_POSTPONED_INDEFINITELY`
- `04` → `WORK_STATUS_ACTIVE`
- `08` → `WORK_STATUS_SUPERSEDED`
- `11` → `WORK_STATUS_WITHDRAWN`

### Publication Type Codes
- `BC` → `PUBLICATION_TYPE_PAPERBACK`
- `BB` → `PUBLICATION_TYPE_HARDBACK`
- `E107` → `PUBLICATION_TYPE_PDF`
- `E105` → `PUBLICATION_TYPE_HTML`
- `E113` → `PUBLICATION_TYPE_XML`
- `E101` → `PUBLICATION_TYPE_EPUB`
- `E127` → `PUBLICATION_TYPE_MOBI`
- `E116` → `PUBLICATION_TYPE_AZW3`
- `E104` → `PUBLICATION_TYPE_DOCX`
- `E100` → `PUBLICATION_TYPE_FICTION_BOOK`
- `A103` → `PUBLICATION_TYPE_MP3`
- `A104` → `PUBLICATION_TYPE_WAV`

### Contributor Role Codes
- `A01` → `CONTRIBUTION_TYPE_AUTHOR`
- `B01` → `CONTRIBUTION_TYPE_EDITOR`
- `B06` → `CONTRIBUTION_TYPE_TRANSLATOR`
- `A13` → `CONTRIBUTION_TYPE_PHOTOGRAPHER`
- `A12` → `CONTRIBUTION_TYPE_ILLUSTRATOR`
- `B25` → `CONTRIBUTION_TYPE_MUSIC_EDITOR`
- `A23` → `CONTRIBUTION_TYPE_FOREWORD_BY`
- `A15` → `CONTRIBUTION_TYPE_PREFACE_BY`
- `A30` → `CONTRIBUTION_TYPE_SOFTWARE_BY`
- `A51` → `CONTRIBUTION_TYPE_RESEARCH_BY`
- `A32` → `CONTRIBUTION_TYPE_CONTRIBUTIONS_BY`
- `A34` → `CONTRIBUTION_TYPE_INDEXER`

### Subject Type Codes
- `04` → `SUBJECT_TYPE_LCC`
- `10` → `SUBJECT_TYPE_BISAC`
- `12` → `SUBJECT_TYPE_BIC`
- `20` → `SUBJECT_TYPE_KEYWORD`
- `93` → `SUBJECT_TYPE_THEMA`
- `B2` → `SUBJECT_TYPE_CUSTOM`

### Language Relation Codes
- `01` → `LANGUAGE_RELATION_ORIGINAL`
- `02` → `LANGUAGE_RELATION_TRANSLATED_FROM`

### Platform Mappings
- `Project MUSE` → `LOCATION_PLATFORM_PROJECT_MUSE`
- `OAPEN` → `LOCATION_PLATFORM_OAPEN`
- `DOAB` → `LOCATION_PLATFORM_DOAB`
- `JSTOR` → `LOCATION_PLATFORM_JSTOR`
- `EBSCO Host` → `LOCATION_PLATFORM_EBSCO_HOST`
- `OCLC KB` → `LOCATION_PLATFORM_OCLC_KB`
- `ProQuest KB` → `LOCATION_PLATFORM_PROQUEST_KB`
- `ProQuest ExLibris` → `LOCATION_PLATFORM_PPROQUEST_EXLIBRIS`
- `EBSCO KB` → `LOCATION_PLATFORM_EBSCO_KB`
- `JISC KB` → `LOCATION_PLATFORM_JISC_KB`
- `Google Books` → `LOCATION_PLATFORM_GOOGLE_BOOKS`
- `Internet Archive` → `LOCATION_PLATFORM_INTERNET_ARCHIVE`
- `ScienceOpen` → `LOCATION_PLATFORM_SCIENCE_OPEN`
- `SciELO Books` → `LOCATION_PLATFORM_SCIELO_BOOKS`
- `Zenodo` → `LOCATION_PLATFORM_ZENODO`

## Notes

1. **XPath Context**: All XPaths are absolute paths starting from the ONIX root element and leading to the Product element and beyond.
2. **Namespace**: All ONIX elements use the namespace prefix `onix:` referring to `http://ns.editeur.org/onix/3.0/reference`.
3. **Root Structure**: The complete ONIX XML structure starts with `/onix:ONIXMessage/onix:Product/` for all product-related data.
4. **Fallback Logic**: Some mappings include complex fallback logic to handle missing or alternative data sources.
5. **Validation**: Several fields include validation logic (e.g., URL validation, ISBN validation, file extension checking).
6. **Transformations**: Many fields include callback functions that transform the raw ONIX values into Thoth-compatible formats.
7. **Default Values**: Some fields have default values when no data is present in the ONIX file.
8. **Multiple Elements**: Some elements like Contributors, Languages, Subjects can appear multiple times within a Product.

This mapping is based on the implementation in the mapper classes located in `src/Mapper/Onix30Thoth/` directory.
