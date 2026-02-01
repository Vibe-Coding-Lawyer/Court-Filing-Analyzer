# Court Filing Analysis Program - Architecture Design

## Overview
The program will analyze court filing documents (PDF, DOCX, TXT) using an LLM to extract structured information and output results to a professional Excel spreadsheet.

## Architecture Components

### 1. Document Processing Module
- **Input**: Court filing documents in various formats (PDF, DOCX, TXT)
- **Function**: Extract text content from documents
- **Libraries**: `python-docx` for DOCX, `PyPDF2` or `pdfplumber` for PDF

### 2. LLM Analysis Module
- **Input**: Extracted text from documents
- **Function**: Use GPT-4.1-mini to analyze text and extract structured information
- **API**: OpenAI API (pre-configured in environment)
- **Extraction Fields**:
  - Case Number
  - Case Name
  - Court
  - Judge(s)
  - Docket ID
  - Date Filed
  - Document Type
  - Filing Party
  - Title
  - Description
  - Key Procedural Event (Yes/No)
  - Procedural Events Referenced
  - Date Issued (if court order)
  - Order Type (if court order)
  - Impact on Case (if court order)
  - Multidistrict Litigation (Yes/No/N/A)

### 3. Excel Generation Module
- **Input**: Structured data from LLM analysis
- **Function**: Create professional Excel spreadsheet with formatting
- **Library**: `openpyxl`
- **Features**:
  - Professional styling following excel-generator skill guidelines
  - Proper column widths and formatting
  - Date formatting
  - Conditional formatting for classification fields
  - Freeze panes for headers
  - Data source attribution

## Program Flow

1. **Initialize**: Set up directories and check dependencies
2. **Load Documents**: Read one or more court filing documents
3. **Extract Text**: Convert documents to text format
4. **Analyze with LLM**: Send text to GPT-4.1-mini with structured prompt
5. **Parse Response**: Extract structured data from LLM response (JSON format)
6. **Generate Excel**: Create formatted Excel file with results
7. **Save Output**: Write Excel file to disk

## Technical Decisions

- **LLM Model**: GPT-4.1-mini (good balance of capability and speed)
- **Prompt Strategy**: Single-shot extraction with structured JSON output
- **Error Handling**: Graceful degradation if fields cannot be extracted
- **Batch Processing**: Support multiple documents in one run
- **Output Format**: One row per document, all fields as columns

## File Structure

```
court_filing_analysis/
├── court_analyzer.py          # Main program
├── requirements.txt           # Python dependencies
├── README.md                  # Usage instructions
├── input/                     # Place court filings here
└── output/                    # Excel outputs saved here
```
