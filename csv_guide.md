
| Column | Required | Description | Example |
|--------|-----------|-------------|---------|
| `publisher`| Mandatory | Publisher Name. | My Publisher |
| `imprint` | Mandatory | Imprint Name. | My Publisher Imprint |
| `work_type` | Mandatory | Type of the work. Accepted values: `BOOK_CHAPTER`; `MONOGRAPH`; `EDITED_BOOK`; `TEXTBOOK`; `JOURNAL_ISSUE`; `BOOK_SET` | TEXTBOOK |
| `work_status` | Mandatory | Status of the work. Accepted values: `FORTHCOMING`; `ACTIVE`; `WITHDRAWN`; `SUPERSEDED`; `POSTPONED_INDEFINITELY`; `CANCELLED` | ACTIVE |
| `title` | Mandatory | The title of the Work. | My Work Title |
| `subtitle`| Optional | The subtitle of the Work. | My Work itle |
| `edition` | Optional | Edition number of the Work. Use "1" for the initial edition of a Work, even if subsequent editions are not planned. | 1 |
| `publication_date` | Optional | Date the work was published in the format `yyyy-mm-dd`. | 2024-01-01 |
| `withdraw_date` | Optional | Date the work was withdrawn from publication in the format `yyyy-mm-dd`. Only applies to out of print and withdrawn works. | 2024-12-01 |
| `place_of_publication` | Optional | Place of publication of the work | Vancouver,CA |
| `cover_url` | Optional | URL of the work's cover image | https://my.publisher.website/book/my-book/cover.jpg |
| `cover_caption` | Optional | Caption describing the work's cover image | Cover of my book |
| `doi` | Optional | Digital Object Identifier of the work | 10.11647/obp.0001 |
| `lccn` | Optional | Library of Congress Control Number of the work (not applicable to chapters) | 2023513485 |
| `oclc_number` | Optional | OCLC (WorldCat) Control Number of the work (not applicable to chapters) | 1463605613 |
| `internal_reference` | Optional | A reference to the Work used by the Publisher internally. | 0100 |
| `page_count` | Optional | Total number of pages. In most cases, unnumbered pages (e.g., endpapers) should be omitted from this count. | 350 |
| `page_breakdown` | Optional | Breakdown of work's page count into front matter, main content, and/or back matter | xi + 140 |
| `first_page` | Optional | Page number on which the work begins (only applicable to chapters) | 155 |
| `last_page` | Optional | Page number on which the work ends (only applicable to chapters) | 172 |
| `image_count` | Optional | Total number of images in the work | 12 |
| `table_count"` | Optional | Total number of tables in the work | 4 |
| `audio_count` | Optional | Total number of audio fragments in the work | 2 |
| `video_count` | Optional | Total number of video fragments in the work | 1 |
| `license` | Optional | URL of the license which applies to this work | https://creativecommons.org/licenses/by-nc/4.0 |
| `copyright_holder` | Optional | Copyright holder of the work | John Doe |
| `landing_page` | Optional | URL of the web page of the work. This should be a valid URL where users can access the work, e.g. the book's landing page on a publisher's website. This URL should not be a DOI. | https://my.publisher.website/book/my-book |
| `short_abstract` | Optional | Short abstract of the work. Where a work has two different versions of the abstract, the truncated version should be entered here. | This is the long abstract of my book |
| `long_abstract` | Optional | Abstract of the work. Where a work has only one abstract, it should be entered here, and Short Abstract can be left blank. | This is the short abstract of my book |
| `general_note` | Optional | A general-purpose field used to include information that does not have a specific designated field | Additional links to further material on publisher's website. |
| `bibliography_note` | Optional | Indicates that the work contains a bibliography or other similar information | Includes bibliography (pages 289-321) and index. |
| `table_of_content` | Optional | Table of contents of the work (not applicable to chapters) | 1. Prologue\n2. Chapter 1\n3. Chapter 2\n4. Chapter 3\n5. Epilogue |
| `contributor_n_name` | Mandatory for each occurrence of contributor | Full name of contributor. Repeatable for each occurrence of contributor (contributor_1_name, contributor_2_name, contributor_3_name, ...) | John Doe |
| `contributor_n_type` | Mandatory for each occurrence of contributor | Role describing the type of contribution to the work. Accepted values: `AUTHOR`; `EDITOR`; `TRANSLATOR`; `PHOTOGRAPHER`; `ILLUSTRATOR`; `MUSIC_EDITOR`; `FOREWORD_BY`; `INTRODUCTION_BY`; `AFTERWORD_BY`; `PREFACE_BY`; `SOFTWARE_BY`; `RESEARCH_BY`; `CONTRIBUTIONS_BY`; `INDEXER`. Repeatable for each occurrence of contributor (contributor_1_type, contributor_2_type, contributor_3_type, ...) | AUTHOR |
| `contributor_n_main_contribution` | Mandatory for each occurrence of contributor | Use `true` or `false` to indicate whether the contribution is a main contribution to the work. Repeatable for each occurrence of contributor (contributor_1_main_contribution, contributor_2_main_contribution, contributor_3_main_contribution, ...) | true |
| `contributor_n_biography` | Optional | The biography of the contributor at the time of contribution. Repeatable for each occurrence of contributor (contributor_1_biography, contributor_2_biography, contributor_3_biography, ...) | This is the bibliography of the author of my book. |
| `contributor_n_orcid` | Optional | ORCID (Open Researcher and Contributor ID) of the contributor. Repeatable for each occurrence of contributor (contributor_1_orcid, contributor_2_orcid, contributor_3_orcid, ...) |  |
| `contributor_n_website` | Optional | URL of the contributor's website. Repeatable for each occurrence of contributor (contributor_1_website, contributor_2_website, contributor_3_website, ...) | https://www.johndoe.org |
| `contributor_n_affiliation_n_position` |  |  |  |
| `contributor_n_affiliation_n_institution_name` |  |  |  |
| `contributor_n_affiliation_n_institution_ror` |  |  |  |
| `contributor_n_affiliation_n_position` |  |  |  |
| `contributor_n_affiliation_n_institution_name` |  |  |  |
| `contributor_n_affiliation_n_institution_ror` |  |  |  |
| `original_language` |  |  |  |
| `translated_from_language` |  |  |  |
| `translated_into_language` |  |  |  |
| `thema_subjects` |  |  |  |
| `bic_subjects` |  |  |  |
| `bisac_subjects` |  |  |  |
| `keywords` |  |  |  |
| `publication_paperback_isbn` |  |  |  |
| `publication_paperback_width_mm` |  |  |  |
| `publication_paperback_width_in` |  |  |  |
| `publication_paperback_height_mm` |  |  |  |
| `publication_paperback_height_in` |  |  |  |
| `publication_paperback_depth_mm` |  |  |  |
| `publication_paperback_depth_in` |  |  |  |
| `publication_paperback_weight_g` |  |  |  |
| `publication_paperback_weight_oz` |  |  |  |
| `publication_paperback_price_1_currency_code` |  |  |  |
| `publication_paperback_price_1_unit_price` |  |  |  |
| `publication_paperback_price_2_currency_code` |  |  |  |
| `publication_paperback_price_2_unit_price` |  |  |  |
| `publication_hardback_isbn` |  |  |  |
| `publication_hardback_width_mm` |  |  |  |
| `publication_hardback_width_in` |  |  |  |
| `publication_hardback_height_mm` |  |  |  |
| `publication_hardback_height_in` |  |  |  |
| `publication_hardback_depth_mm` |  |  |  |
| `publication_hardback_depth_in` |  |  |  |
| `publication_hardback_weight_g` |  |  |  |
| `publication_hardback_weight_oz` |  |  |  |
| `publication_hardback_price_1_currency_code` |  |  |  |
| `publication_hardback_price_1_unit_price` |  |  |  |
| `publication_pdf_isbn` |  |  |  |
| `publication_pdf_location_1_landing_page` |  |  |  |
| `publication_pdf_location_1_full_text_url` |  |  |  |
| `publication_pdf_location_1_platform` |  |  |  |
| `publication_pdf_location_2_landing_page` |  |  |  |
| `publication_pdf_location_2_full_text_url` |  |  |  |
| `publication_pdf_location_2_platform` |  |  |  |
| `publication_epub_isbn` |  |  |  |
| `publication_epub_location_1_landing_page` |  |  |  |
| `publication_epub_location_1_full_text_url` |  |  |  |
| `publication_epub_location_1_platform` |  |  |  |
| `publication_epub_price_1_currency_code` |  |  |  |
| `publication_epub_price_1_unit_price` |  |  |  |
| `publication_mobi_isbn` |  |  |  |
| `publication_mobi_location_1_landing_page` |  |  |  |
| `publication_mobi_location_1_full_text_url` |  |  |  |
| `publication_mobi_location_1_platform` |  |  |  |
| `publication_azw3_isbn` |  |  |  |
| `publication_azw3_location_1_landing_page` |  |  |  |
| `publication_azw3_location_1_full_text_url` |  |  |  |
| `publication_azw3_location_1_platform` |  |  |  |
| `series_name` |  |  |  |
| `series_issn` |  |  |  |
| `series_issue_number` |  |  |  |
| `funding_program` |  |  |  |
| `funding_project` |  |  |  |
| `funding_grant_number` |  |  |  |
| `funding_jurisdiction` |  |  |  |
| `funding_institution_name` |  |  |  |
| `funding_institution_ror` |  |  |  |
| `book_id` |  |  |  |
