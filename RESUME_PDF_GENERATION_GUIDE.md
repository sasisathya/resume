# Resume PDF Generation Guide

## Overview
This guide explains how to convert the HTML resume to PDF after making changes.

---

## Files Involved
- **HTML File:** `Sasi_Sathya_Resume.html` (main resume file)
- **PDF File:** `Sasi_Sathya_Resume.pdf` (generated output)
- **Profile Photo:** `profile_photo.jpg` (included in HTML)

---

## How to Generate PDF

### Prerequisites
- Google Chrome installed on your Mac
- Working directory: `/Users/sajja.krishna/Downloads/sasi`

### Command to Generate PDF

Run this command in the terminal:

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu --print-to-pdf="/Users/sajja.krishna/Downloads/sasi/Sasi_Sathya_Resume.pdf" "file:///Users/sajja.krishna/Downloads/sasi/Sasi_Sathya_Resume.html"
```

### One-Line Script

For convenience, you can copy and run this exact command:

```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --print-to-pdf="/Users/sajja.krishna/Downloads/sasi/Sasi_Sathya_Resume.pdf" "file:///Users/sajja.krishna/Downloads/sasi/Sasi_Sathya_Resume.html"
```

---

## Step-by-Step Instructions

1. **Open Terminal**
   ```
   Cmd + Space → Type "Terminal" → Press Enter
   ```

2. **Navigate to the resume folder** (optional, if needed)
   ```bash
   cd /Users/sajja.krishna/Downloads/sasi
   ```

3. **Copy and paste the Chrome command above** into Terminal

4. **Press Enter** to execute

5. **Wait for completion** - You'll see:
   ```
   4228881 bytes written to file /Users/sajja.krishna/Downloads/sasi/Sasi_Sathya_Resume.pdf
   ```

6. **PDF is ready!** - Find it in the same folder with the HTML

---

## What Happens

✅ Chrome opens in headless mode (no visible window)
✅ Loads your HTML file and renders it
✅ Exports as PDF with proper formatting
✅ Saves to: `Sasi_Sathya_Resume.pdf`
✅ Preserves all styling, icons, photos, and formatting

---

## Output Details

- **Format:** A4 (8.5" × 11")
- **No headers/footers:** Date/URL not included
- **No margins:** Uses CSS page margins (0px)
- **File size:** ~4.0 MB
- **Icons:** Embedded SVG icons (location, phone, email, LinkedIn, portfolio)
- **Photo:** Embedded profile_photo.jpg

---

## Making Changes

1. **Edit the HTML file:** `Sasi_Sathya_Resume.html`
   - Edit text content
   - Change colors
   - Modify styling
   - Update links

2. **Run the Chrome command** (from above)

3. **PDF updates automatically** with your changes

---

## Notes

- The HTML file is self-contained with embedded SVG icons
- The profile photo must be in the same folder
- Changes in HTML immediately reflect in the generated PDF
- Font Awesome CDN not used (all icons are embedded SVG)
- CSS @page rules ensure clean PDF output without extra margins

---

## Troubleshooting

**Q: Command not found error?**
- Make sure Google Chrome is installed
- Check the path: `/Applications/Google Chrome.app/Contents/MacOS/Google Chrome`

**Q: PDF has extra header/footer?**
- The Chrome command includes flags to remove headers/footers
- If still appearing, check that the HTML @page CSS rules are intact

**Q: Icons not showing?**
- Icons are embedded as SVG in the HTML
- No external CDN required
- Should always display correctly

**Q: PDF looks different from HTML?**
- Check the CSS print styles in the HTML `<style>` section
- Verify the @page rules are present for clean formatting

---

## Quick Reference

**Save this command for quick access:**
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --print-to-pdf="/Users/sajja.krishna/Downloads/sasi/Sasi_Sathya_Resume.pdf" "file:///Users/sajja.krishna/Downloads/sasi/Sasi_Sathya_Resume.html"
```

---

**Last Updated:** August 13, 2026
**Created by:** Claude Code
