# NormConf Intro to PDF Text & Table Extraction

Supplemental code/data for NormConf Lightning Talk on PDF Text & Table Extraction presented by Anna Godwin in December 2022.

## Code Snippets in the Lightning Talk Powerpoint

### Search the Text: pymupdf

```
pip install pymupdf
```

```
import fitz

doc = fitz.open(“sample.pdf”)

text_list = list()
for page in doc:
text_list.append(page.get_textpage().extractText())

all_text_str = " ".join(collate_text_list)
```

### Condense PDF: pymupdf

```
pip install pymupdf
```

```
import fitz

doc_orig = fitz.open("sample.pdf")

doc_short = fitz.open()  # initialize an empty pdf
doc_short.insert_pdf(doc_orig, from_page=2, to_page=5)
doc_short.insert_pdf(doc_orig, from_page=10, to_page=11)
doc_short.save("short_pdf.pdf")
doc_short.close()
```


### Collate PDFs: pymupdf

```
pip install pymupdf
```

```
import fitz

doc_collate = fitz.open()  # initialize an empty pdf
for pdf_file in pdf_directory:
	with fitz.open(pdf_file) as f:
	doc_collate.insert_pdf(f)

doc_collate.save("collated_pdf.pdf")
doc_collate.close()
```

### Extract Tables: tabula-py

```
pip install tabula-py
```

```
import tabula

output = tabula.read_pdf(“test.pdf”,
guess=False, 
lattice=False,
stream=True,
pages=1)
```

```
import tabula

column_meas = [0.3, 10.5, 15.6, 20.7]

output = tabula.read_pdf("test.pdf",
                      	   pages=1,
                      	   columns=column_meas)
```



### Attributions

The example PDF in the powerpoint is provided by the open-source **One thousand dot gov PDF dataset**:

Library Of Congress Web Archiving Program. (2019) .gov PDF dataset. [Washington, D.C.: Library of Congress Web Archiving Program] [Software, E-Resource] Retrieved from the Library of Congress, https://www.loc.gov/item/2020445568/.
