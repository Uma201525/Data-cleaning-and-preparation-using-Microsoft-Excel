# Data-cleaning-and-preparation-using-Microsoft-Excel
Missing values, inconsistent formatting, duplicate records, and poorly structured text fields after cleaned

E-Commerce & Retail Product Dataset: Data Cleaning & Transformation Pipeline

Overview Raw 

E-commerce dataset containing inconsistent product listings, missing attributes, incorrect date formats, and formatting errors across global product inventories.

This repository documents the end-to-end data cleaning workflow applied to audit, sanitize, and structure raw product data for reliable downstream analytics and reporting.

Dataset Issues Summary & Solutions



Inconsistent spacing & non-printable characters          PRODUCT NAME  COLUMN                                                =PROPER(TRIM(CLEAN(E2)))   

Missing price values         Affected Column PRICE                         Imputed using overall column average:  IF(ISBLANK(E2),AVERAGE($E$2:$E$35),E2)


Missing category classifications                         CATEGORY                                       Imputed with default label:IF(ISBLANK(F2), "UNKNOWN", F2) 


Inconsistent casing                                      CATEGORY                                              Standardized to uppercase using UPPER(E2)  


Typos in category names                                  CATEGORY                                              Batch corrected using Find & Replace (Ctrl + H) 



Duplicate records across full rows                       All Columns                                 Removed via Data Ribbon > Remove Duplicates > Select All  



Combined manufacturing and country identifiers         PRODUCT ID                                      Parsed using string functions: Date extraction: LEFT(A2,6)
Country code extraction: RIGHT(A2, 2)   


Uncombined brand and product names                     BRAND NAME, PRODUCT NAME                  Merged into single PRODUCT BRAND column: CONCATENATE(D2, " ", E2) 



Currency format inconsistencies                            PRICE                                  Normalized numeric display via Home > Number Group > Currency  



Unstandardized date formats                            MANUFACTURING DATE                    Parsed to standard DD/MM/YYYY using DATEVALUE() or custom formatting  




Data Transformation Pipeline1.

1.String Parsing & Column Splits
 The original PRODUCT ID field concatenated both date strings and country codes (e.g., 28-JAN-US).
 Manufacturing Date Extraction: =LEFT(A2, 6)
 Country Code Extraction: =RIGHT(A2, 2) 

2. Concatenation & Text Standardization
  Brand Merging: BRAND NAME and PRODUCT NAME were joined to create a consolidated PRODUCT BRAND identifier using =CONCATENATE(D2, " ", E2).
  Text Normalization: Removed irregular spaces and hidden characters using =PROPER(TRIM(CLEAN(E2))).

3. Missing Value Imputation & Quality Control
  Price Imputation: Missing price values were replaced with the global average price across all valid rows:
  =IF(ISBLANK(E2),AVERAGE($E$2:$E$35), E2).
  Category Normalization: Unassigned categories were mapped to "UNKNOWN" using  =IF(ISBLANK(F2), "UNKNOWN", F2).

4. Date & Currency Formatting
  Dates were converted to serial values using DATEVALUE() and formatted as DD/MM/YYYY.
  Currency symbols and decimal alignments were standardized across all region rows.

Technical Tools & Skills Demonstrated 

Data Cleaning: Missing value imputation, string trimming, duplicate identification, schema standardization.  
Excel / Spreadsheet Analysis: LEFT(), RIGHT(), CONCATENATE(), TRIM(), CLEAN(), PROPER(), DATEVALUE(), AVERAGE(), IF(), Conditional Logic.   
Data Quality Management: Standardizing regional formatting discrepancies across international datasets (US, UK, IN, CA, DE, AU, ES, BR, CN, RU).


