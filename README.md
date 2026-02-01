# Court Filing Analyzer

A Python program that analyzes court filings to automatically extract key information including parties, court details, procedural history, and litigation impact. The program uses AI-powered analysis (GPT-4.1-mini) to understand legal documents and outputs structured data to professional Excel spreadsheets.

## Features

- **Multi-format Support**: Processes PDF, DOCX, and TXT files
- **AI-Powered Analysis**: Uses GPT-4.1-mini for intelligent information extraction
- **Comprehensive Data Extraction**: Captures 16 key fields from court filings
- **Professional Excel Output**: Generates formatted spreadsheets with conditional formatting
- **Batch Processing**: Analyze multiple documents in a single run
- **Error Handling**: Gracefully handles missing information and processing errors

## Extracted Information

The program extracts the following information from each court filing:

### Basic Case Information
- Case Number
- Case Name
- Court
- Judge(s)

### Filing Details
- Docket ID
- Date Filed
- Document Type
- Filing Party
- Title
- Description

### Procedural Information
- Key Procedural Event (Yes/No)
- Procedural Events Referenced

### Court Order Specifics (if applicable)
- Date Issued
- Order Type
- Impact on Case
- Multidistrict Litigation (MDL) status

## Installation

### Prerequisites
- Python 3.11 or higher
- OpenAI API key (configured in environment as `OPENAI_API_KEY`)

### Install Dependencies

```bash
pip install -r requirements.txt
```

Or install manually:

```bash
pip install python-docx pdfplumber PyPDF2 openai openpyxl
```

## Usage

### Basic Usage

Analyze a single court filing:

```bash
python3 court_analyzer.py path/to/filing.pdf
```

### Batch Processing

Analyze multiple filings at once:

```bash
python3 court_analyzer.py filing1.pdf filing2.docx filing3.txt
```

### Using with Input Directory

Place all your court filings in the `input/` directory and run:

```bash
python3 court_analyzer.py input/*.pdf
```

## Project Structure

```
court_filing_analysis/
├── court_analyzer.py          # Main program
├── requirements.txt           # Python dependencies
├── README.md                  # This file
├── architecture.md            # Technical architecture documentation
├── requirements.md            # Detailed field requirements
├── input/                     # Place court filings here (optional)
└── output/                    # Excel reports saved here
```

## Output

The program generates an Excel spreadsheet with the following features:

- **Professional Formatting**: Clean, readable layout with proper styling
- **Conditional Formatting**: Visual indicators for key fields (e.g., procedural events highlighted)
- **Frozen Headers**: Column headers remain visible when scrolling
- **Wrapped Text**: Long descriptions are properly wrapped for readability
- **Metadata**: Generation timestamp and file count included
- **Optimized Columns**: Column widths adjusted for content

Output files are saved in the `output/` directory with timestamps:
- Format: `court_filing_analysis_YYYYMMDD_HHMMSS.xlsx`

## Example Output

| Source File | Case Number | Case Name | Court | Judge(s) | ... |
|-------------|-------------|-----------|-------|----------|-----|
| filing1.pdf | 2024-CV-1234 | Smith v. Jones | Superior Court | Hon. Jane Doe | ... |
| filing2.docx | 2024-CV-5678 | ABC Corp v. XYZ Inc | District Court | Hon. John Smith | ... |

## Configuration

### API Configuration

The program uses the OpenAI API with the following default settings:
- Model: `gpt-4.1-mini`
- Temperature: 0.1 (for consistent, factual extraction)
- Max Tokens: 2000

To modify these settings, edit the `analyze_filing` method in `court_analyzer.py`.

### Excel Theme

The default theme is "Elegant Black" with professional styling. To change colors, modify the `THEME` dictionary in the `CourtFilingAnalyzer` class:

```python
self.THEME = {
    'primary': '2D2D2D',      # Primary text color
    'light': 'E5E5E5',        # Light background
    'accent': '1F4E79',       # Accent color
    'header_bg': '2D2D2D',    # Header background
    'header_text': 'FFFFFF'   # Header text color
}
```

## Error Handling

The program handles common issues gracefully:

- **Missing Files**: Validates file existence before processing
- **Unsupported Formats**: Provides clear error messages for invalid file types
- **Extraction Failures**: Continues processing other files if one fails
- **Missing Information**: Uses null/N/A for fields that cannot be determined
- **API Errors**: Reports API issues with helpful error messages

## Limitations

- **Accuracy**: Extraction accuracy depends on document quality and structure
- **Handwritten Documents**: Cannot process handwritten or image-based documents without OCR
- **Complex Tables**: May struggle with complex tabular data in PDFs
- **Scanned PDFs**: Requires OCR preprocessing for scanned documents
- **API Rate Limits**: Subject to OpenAI API rate limits for high-volume processing

## Troubleshooting

### No text extracted from PDF
- Ensure the PDF contains selectable text (not a scanned image)
- Try converting the PDF to text format first
- Consider using OCR tools for scanned documents

### API errors
- Verify your OpenAI API key is correctly set in environment variables
- Check your API quota and rate limits
- Ensure internet connectivity

### Missing information in output
- Review the source document to confirm the information exists
- Check if the document format is unusual or non-standard
- Consider providing additional context in the document

## Advanced Usage

### Programmatic Usage

You can also use the analyzer as a Python module:

```python
from court_analyzer import CourtFilingAnalyzer

# Initialize analyzer
analyzer = CourtFilingAnalyzer(output_dir="my_output")

# Process files
file_paths = ["filing1.pdf", "filing2.docx"]
output_path = analyzer.process_files(file_paths)

print(f"Report saved to: {output_path}")
```

### Custom Analysis

To extract additional fields or modify the analysis prompt, edit the `analyze_filing` method in `court_analyzer.py`.

## License

This program is provided as-is for legal document analysis purposes.

## Support

For issues, questions, or feature requests, please refer to the project documentation or contact the development team.
