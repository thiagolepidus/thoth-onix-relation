# ONIX 3.0 to Thoth Model Mapping Reference

This document provides a comprehensive mapping between ONIX 3.0 XML elements and Thoth model attributes based on the mapper classes in this project.

## Notes

1. **XPath Context**: All XPaths are absolute paths starting from the ONIX root element and leading to the Product element and beyond.
2. **Namespace**: All ONIX elements use the namespace prefix `onix:` referring to `http://ns.editeur.org/onix/3.0/reference`.
3. **Root Structure**: The complete ONIX XML structure starts with `/onix:ONIXMessage/onix:Product/` for all product-related data.
8. **Multiple Elements**: Some elements like Contributors, Languages, Subjects can appear multiple times within a Product.

## Work Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `workStatus` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:PublishingStatus` | 01→CANCELLED, 02→FORTHCOMING, 03→POSTPONED_INDEFINITELY, 04→ACTIVE, 08→SUPERSEDED, 11→WITHDRAWN |
| `title` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:TitleDetail/onix:TitleElement/onix:TitleText` | Main work title |
| `subtitle` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:TitleDetail/onix:TitleElement/onix:Subtitle` | Work subtitle |
| `edition` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Edition/onix:EditionNumber` | Edition number, defaults to 1 if not specified |
| `publicationDate` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:PublishingDate[onix:PublishingDateRole="01"]/onix:Date` | Publication date in YYYYMMDD format |
| `withdrawnDate` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:PublishingDate[onix:PublishingDateRole="13"]/onix:Date` | Date work was withdrawn |
| `place` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:CityOfPublication` | Place of publication |
| `coverUrl` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:SupportingResource[onix:ResourceContentType="01"]/onix:ResourceVersion[onix:ResourceForm="02"]/onix:ResourceLink` | Must be valid URL with image extension |
| `coverCaption` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:SupportingResource/onix:ResourceFeature[onix:ResourceFeatureType="02"]/onix:FeatureNote` | Cover image caption |
| `doi` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="06"]/onix:IDValue` | Digital Object Identifier, prepends https://doi.org/ if not present |
| `lccn` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="13"]/onix:IDValue` | Library of Congress Control Number |
| `oclc` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="23"]/onix:IDValue` | OCLC number |
| `pageCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Extent/onix:ExtentValue` | Total page count |
| `imageCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentType="09"]/onix:Number` | Number of images |
| `tableCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentType="11"]/onix:Number` | Number of tables |
| `audioCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentType="19"]/onix:Number` | Number of audio elements |
| `videoCount` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:AncillaryContent[onix:AncillaryContentDescription="Videos"]/onix:Number` | Number of video elements |
| `license` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:EpubLicense/onix:EpubLicenseExpression[onix:EpubLicenseExpressionType="02"]/onix:EpubLicenseExpressionLink` | License URL |
| `copyrightHolder` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:CopyrightStatement/onix:CopyrightOwner/onix:PersonName` | Copyright holder name |
| `landingPage` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher/onix:Website[onix:WebsiteRole="02"]/onix:WebsiteLink` | Work landing page URL |
| `shortAbstract` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="02"]/onix:Text` | Short description/abstract |
| `longAbstract` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="03"]/onix:Text \| /onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="30"]/onix:Text` | Long description/abstract |
| `generalNote` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="13"]/onix:Text` | General notes about the work |
| `bibliographyNote` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:IllustrationsNote` | Notes about bibliography/illustrations |
| `toc` | `/onix:ONIXMessage/onix:Product/onix:CollateralDetail/onix:TextContent[onix:TextType="04"]/onix:Text` | Table of contents |

## Publication Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `publicationType` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:ProductForm` | BC→PAPERBACK, BB→HARDBACK, E107→PDF, E105→HTML, E113→XML, E101→EPUB, E127→MOBI, E116→AZW3, E104→DOCX, E100→FICTION_BOOK, A103→MP3, A104→WAV |
| `isbn` | `/onix:ONIXMessage/onix:Product/onix:ProductIdentifier[onix:ProductIDType="15"]/onix:IDValue` | Uses Biblys\Isbn library for validation and converts to ISBN-13 format |
| `heightMm` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="01" and onix:MeasureUnitCode="mm"]/onix:Measurement` | Height in millimeters |
| `heightIn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="01" and onix:MeasureUnitCode="in"]/onix:Measurement` | Height in inches |
| `widthMm` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="02" and onix:MeasureUnitCode="mm"]/onix:Measurement` | Width in millimeters |
| `widthIn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="02" and onix:MeasureUnitCode="in"]/onix:Measurement` | Width in inches |
| `depthMm` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="03" and onix:MeasureUnitCode="mm"]/onix:Measurement` | Depth/thickness in millimeters |
| `depthIn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="03" and onix:MeasureUnitCode="in"]/onix:Measurement` | Depth/thickness in inches |
| `weightG` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="08" and onix:MeasureUnitCode="gr"]/onix:Measurement` | Weight in grams |
| `weightOz` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Measure[onix:MeasureType="08" and onix:MeasureUnitCode="oz"]/onix:Measurement` | Weight in ounces |

## Contributor Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `firstName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:NamesBeforeKey \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | If comma present in inverted name, takes part after comma |
| `lastName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:KeyNames \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | If comma present in inverted name, takes part before comma |
| `fullName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonName \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | If comma present in inverted name, reverses order and joins with space |
| `orcid` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:NameIdentifier[onix:NameIDType="21"]/onix:IDValue` | ORCID identifier, prepends https://orcid.org/ if not present |
| `website` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:Website[onix:WebsiteRole="06"]/onix:WebsiteLink` | Contributor's website |

## Contribution Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `contributionType` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ContributorRole` | A01→AUTHOR, B01→EDITOR, B06→TRANSLATOR, A13→PHOTOGRAPHER, A12→ILLUSTRATOR, B25→MUSIC_EDITOR, A23→FOREWORD_BY, A15→PREFACE_BY, A30→SOFTWARE_BY, A51→RESEARCH_BY, A32→CONTRIBUTIONS_BY, A34→INDEXER |
| `mainContribution` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:SequenceNumber` | Returns true if sequence number is "1", indicates primary contributor |
| `biography` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:BiographicalNote` | Contributor biography |
| `firstName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:NamesBeforeKey \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | Inherited from contributor |
| `lastName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:KeyNames \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | Inherited from contributor |
| `fullName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonName \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:PersonNameInverted` | Inherited from contributor |
| `contributionOrdinal` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:SequenceNumber` | Order of contribution |

## Affiliation Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `affiliationPosition` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ProfessionalAffiliation/onix:ProfessionalPosition` | Position/role within institution |
| `institutionName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ProfessionalAffiliation/onix:Affiliation` | Name of affiliated institution |
| `institutionRor` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Contributor/onix:ProfessionalAffiliation/onix:AffiliationIdentifier[onix:AffiliationIDType="40"]/onix:IDValue` | ROR (Research Organization Registry) ID, prepends https://ror.org/ if not present |

## Location Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `landingPage` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:Website[onix:WebsiteRole="02"]/onix:WebsiteLink \| /onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher/onix:Website[onix:WebsiteRole="02"]/onix:WebsiteLink \| /onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:Website[onix:WebsiteRole="29"]/onix:WebsiteLink` | Falls back through supplier, publisher, and file URLs with complex logic |
| `fullTextUrl` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:Website[onix:WebsiteRole="29"]/onix:WebsiteLink` | Validates file URLs and falls back to resource links with complex logic |
| `locationPlatform` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Supplier/onix:SupplierName` | Maps supplier names to platform constants (Project MUSE, OAPEN, DOAB, JSTOR, etc.) |

## Price Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `currencyCode` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Price/onix:CurrencyCode` | ISO currency code |
| `unitPrice` | `/onix:ONIXMessage/onix:Product/onix:ProductSupply/onix:SupplyDetail/onix:Price/onix:PriceAmount` | Price amount |

## Language Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `languageCode` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Language/onix:LanguageCode` | Converts to ISO 639-2 format with language name, returns format: "CODE\|Name" |
| `languageRelation` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Language/onix:LanguageRole` | Maps language role codes: 01→ORIGINAL, 02→TRANSLATED_FROM |

## Subject Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `subjectType` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Subject/onix:SubjectSchemeIdentifier` | Maps subject scheme codes: 04→LCC, 10→BISAC, 12→BIC, 20→KEYWORD, 93→THEMA, B2→CUSTOM |
| `subjectCode` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Subject/onix:SubjectCode \| /onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Subject/onix:SubjectHeadingText` | Subject classification code or text |

## Series Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `seriesId` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="01" and onix:IDTypeName="Series ID"]/onix:IDValue` | Series identifier |
| `seriesName` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:TitleDetail/onix:TitleElement/onix:TitleText` | Series name/title |
| `issn` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="02"]/onix:IDValue` | Formats ISSN with hyphen if needed, adds hyphen between 4th and 5th characters |
| `seriesUrl` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="01" and onix:IDTypeName="Series URL"]/onix:IDValue` | Series website URL |
| `seriesCfpUrl` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionIdentifier[onix:CollectionIDType="01" and onix:IDTypeName="Series Call for Proposals URL"]/onix:IDValue` | Series call for proposals URL |
| `issueOrdinal` | `/onix:ONIXMessage/onix:Product/onix:DescriptiveDetail/onix:Collection/onix:CollectionSequence[onix:CollectionSequenceType="03"]/onix:CollectionSequenceNumber` | Issue number within series |

## Funding Model Mappings

| Thoth Attribute | ONIX XPath | Notes |
|---|---|---|
| `institutionName` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:PublisherName` | Funding institution name |
| `institutionRor` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:PublisherIdentifier[onix:PublisherIDType="40"]/onix:IDValue` | ROR ID of funding institution, prepends https://ror.org/ if not present |
| `program` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="programname"]/onix:IDValue` | Funding program name |
| `projectName` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="projectname"]/onix:IDValue` | Project name |
| `projectShortName` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="projectshortname"]/onix:IDValue` | Project short name/acronym |
| `grantNumber` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="grantnumber"]/onix:IDValue` | Grant number |
| `jurisdiction` | `/onix:ONIXMessage/onix:Product/onix:PublishingDetail/onix:Publisher[onix:PublishingRole="16"]/onix:Funding/onix:FundingIdentifier[onix:FundingIDType="01" and onix:IDTypeName="jurisdiction"]/onix:IDValue` | Funding jurisdiction |
