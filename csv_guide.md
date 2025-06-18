# Thoth Template CSV Documentation

## Overview

This repository contains a CSV template file (`thoth_template.csv`) for importing scholarly publication metadata into the Thoth platform. Thoth is an open metadata management and dissemination system for Open Access books.

## File Structure

The template contains **118 columns** covering comprehensive metadata for scholarly publications, including:

- Basic publication information
- Contributors and their affiliations
- Publication formats and pricing
- Subject classifications
- Funding information
- Series information

## Usage Guide

### 1. File Format
- **File Type**: CSV (Comma-Separated Values)
- **Encoding**: UTF-8
- **Delimiter**: Comma (`,`)
- **Text Qualifier**: Double quotes (`"`)

### 2. How to Use This Template

1. **Download the template**: Use the `thoth_template.csv` file as your starting point
2. **Fill in your data**: Replace the example values with your actual publication metadata
3. **Validate data**: Ensure all required fields are completed and data formats are correct
4. **Import to Thoth**: Upload the completed CSV to your Thoth instance

### 3. Column Categories

#### Basic Publication Information
| Column | Description | Required | Example |
|--------|-------------|----------|---------|
| `publisher` | Publisher name | Yes | "My Publisher" |
| `imprint` | Imprint name | No | "My Publisher Imprint" |
| `work_type` | Type of work | Yes | "Edited Book" |
| `work_status` | Publication status | Yes | "Active" |
| `title` | Main title | Yes | "My book title" |
| `subtitle` | Subtitle | No | "My book subtitle" |
| `edition` | Edition number | No | "1" |
| `publication_date` | Publication date | Yes | "2024-01-01" |
| `withdraw_date` | Withdrawal date | No | "2025-01-01" |
| `place_of_publication` | Publication location | No | "Earth, Milky Way" |

#### Identifiers and References
| Column | Description | Format | Example |
|--------|-------------|--------|---------|
| `doi` | Digital Object Identifier | DOI format | "10.12345/11221122" |
| `lccn` | Library of Congress Control Number | LCCN format | "2014123456" |
| `oclc_number` | OCLC number | Numeric | "1000123456" |
| `internal_reference` | Internal reference | Text | "my_internal_reference" |

#### Content Description
| Column | Description | Example |
|--------|-------------|---------|
| `page_count` | Total page count | "302" |
| `page_breakdown` | Page breakdown | "xxiv+278" |
| `first_page` | First page (for chapters) | N/A for books |
| `last_page` | Last page (for chapters) | N/A for books |
| `image_count` | Number of images | "12" |
| `table_count` | Number of tables | "7" |
| `audio_count` | Number of audio files | "2" |
| `video_count` | Number of video files | "5" |

#### Rights and Licensing
| Column | Description | Example |
|--------|-------------|---------|
| `license` | License URL | "https://creativecommons.org/licenses/by-nc/4.0/" |
| `copyright_holder` | Copyright holder | "John Doe" |

#### Contributors (Up to 5 contributors)
For each contributor (1-5), the following fields are available:
- `contributor_X_name`: Full name
- `contributor_X_role`: Role (Author, Editor, Translator, etc.)
- `contribution_X_main_contribution`: Boolean (true/false)
- `contributor_X_biography`: Biography text
- `contributor_X_orcid`: ORCID identifier
- `contributor_X_website`: Personal website
- `contributor_X_affiliation_Y_position`: Position at institution
- `contributor_X_affiliation_Y_institution_name`: Institution name
- `contributor_X_affiliation_Y_institution_ror`: ROR identifier

#### Language Information
| Column | Description | Format | Example |
|--------|-------------|--------|---------|
| `original_language` | Original language(s) | ISO codes | "ENG;FRE" |
| `translated_from_language` | Source language | ISO codes | "" |
| `translated_into_language` | Target language(s) | ISO codes | "SPA;ITA" |

#### Subject Classifications
| Column | Description | Format | Example |
|--------|-------------|--------|---------|
| `thema_subjects` | Thema subject codes | Semicolon-separated | "FYM;QDTK;QDHR5" |
| `bic_subjects` | BIC subject codes | Semicolon-separated | "HPK;HPCF3" |
| `bisac_subjects` | BISAC subject codes | Semicolon-separated | "FIC057000;PHI014000" |
| `keywords` | Keywords | Semicolon-separated | "embodiment;philosophy;media theory" |

#### Publication Formats

The template supports multiple publication formats:

##### Paperback
- ISBN, dimensions (mm/inches), weight (g/oz), pricing

##### Hardback
- ISBN, dimensions (mm/inches), weight (g/oz), pricing

##### PDF
- ISBN, landing pages, full-text URLs, platforms

##### EPUB
- ISBN, landing pages, full-text URLs, platforms, pricing

##### MOBI
- ISBN, landing pages, full-text URLs, platforms

##### AZW3
- ISBN, landing pages, full-text URLs, platforms

#### Series Information
| Column | Description | Example |
|--------|-------------|---------|
| `series_name` | Series name | "My Series Name" |
| `series_issn` | Series ISSN | "1122-1122" |
| `series_issue_number` | Issue number | "3" |

#### Funding Information
| Column | Description | Example |
|--------|-------------|---------|
| `funding_program` | Funding program | "My Funding Program" |
| `funding_project` | Project name | "My Funding Project" |
| `funding_grant_number` | Grant number | "0102-3345" |
| `funding_jurisdiction` | Jurisdiction | "World" |
| `funding_institution_name` | Institution name | "My Funding Institution" |
| `funding_institution_ror` | ROR identifier | "01a23bcd4" |

### 4. Data Format Guidelines

#### Dates
- Format: `YYYY-MM-DD`
- Example: `2024-01-01`

#### Boolean Values
- Use: `true` or `false`
- Leave empty for N/A

#### Multiple Values
- Separate with semicolons (`;`)
- Example: `"ENG;FRE;SPA"`

#### URLs
- Include full URLs with protocol
- Example: `https://example.com/path`

#### Identifiers
- **ORCID**: Format as `0000-0000-0000-0000`
- **DOI**: Include full DOI (e.g., `10.12345/67890`)
- **ISBN**: Use 13-digit format without hyphens

### 5. Required Fields

The following fields are typically required:
- `publisher`
- `work_type`
- `work_status`
- `title`
- `publication_date`
- At least one contributor with role "Author"

### 6. Common Work Types

- `Monograph`
- `Edited Book`
- `Textbook`
- `Journal Issue`
- `Book Chapter`

### 7. Common Contributor Roles

- `Author`
- `Editor`
- `Translator`
- `Introduction By`
- `Preface By`
- `Foreword By`
- `Afterword By`

### 8. Tips for Data Entry

1. **Consistency**: Maintain consistent formatting across all entries
2. **Validation**: Use proper ISBN, DOI, and ORCID validators
3. **Languages**: Use ISO 639-3 language codes
4. **Subject Codes**: Verify codes against official Thema, BIC, and BISAC databases
5. **Pricing**: Include currency codes (USD, EUR, GBP, etc.)

### 9. Troubleshooting

#### Common Issues:
- **Invalid dates**: Ensure YYYY-MM-DD format
- **Missing quotes**: CSV values with commas must be quoted
- **Character encoding**: Save file as UTF-8
- **Empty required fields**: Check for missing mandatory information

## Support

For more information about Thoth and metadata management:
- [Thoth Documentation](https://thoth.pub/)
- [Thoth GitHub Repository](https://github.com/thoth-pub/thoth)

## Version

Template Version: 1.0
Last Updated: June 18, 2025
