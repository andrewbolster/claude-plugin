---
description: Convert Office/PDF/binary files to markdown using markitdown via uvx
disable-model-invocation: false
---

# markitdown — File-to-Markdown Conversion

Use `markitdown` (via `uvx`) to convert binary documents to readable markdown before analysis or ingestion.

## Standard Invocation

```bash
uvx --from 'markitdown[pdf,docx,pptx,xlsx,outlook]' markitdown <input-file> --output /tmp/<basename>.md
```

Then read the output file:
```bash
# or use the Read tool on /tmp/<basename>.md
```

## Supported Formats

| Extension | Format |
|-----------|--------|
| `.pdf` | PDF documents |
| `.docx` | Word documents |
| `.pptx` | PowerPoint presentations |
| `.xlsx` | Excel spreadsheets |
| `.msg`, `.eml` | Outlook/email messages |

## When to Use

- User provides a binary document for analysis (PDF report, Word doc, PowerPoint)
- Need to extract text content from Office files for summarisation
- Preprocessing documents before feeding to further analysis

## Pattern

1. User shares a file path (e.g., `/Users/bolster/Downloads/report.pdf`)
2. Run: `uvx --from 'markitdown[pdf,docx,pptx,xlsx,outlook]' markitdown /Users/bolster/Downloads/report.pdf --output /tmp/report.md`
3. Read `/tmp/report.md` with the Read tool
4. Proceed with analysis on the extracted text

**Note**: Always write to `/tmp/` to avoid cluttering the user's directories.
