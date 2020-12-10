---
title: >-
  Who wants Bangladesh National ID OCR extractor with 100% accuracy? #OCR  #NID
  #bangladesh #Bangla
date: 2020-11-26T21:51:50.337Z
description: >-
  We just finished writing and testing a Bangladesh National ID data extractor
  with 100% accuracy. There are tons of potential use cases for this. As far as
  I know there is no such tool available
image: /img/nid-demo.png
---
We just finished writing and testing a Bangladesh National ID data extractor with 100% accuracy. There are tons of potential use cases for this. As far as I know there is no such tool available. This software is written in python. 

![api demo](/img/api-demo.jpg "API Demo")

Sample API response from uploaded NID image in JSON:

```
{
  "text": "raw [...] text",
  "parsed": [
    "গণপ্রজাতন্ত্রী বাংলাদেশ সরকার",
    "Government of the People's Republic of Bangladesh",
    "NATIONAL ID CARD / জাতীয় পরিচয় পত্র",
    "নাম: মোঃ [...]",
    "Name: [...]",
    "পিতা: মোঃ [...]",
    "জজ মাতা: [...]",
    "Date of Birth: [..] Mar 1990",
    "ID NO: 1990[...]"
  ],
  "id_no": "1990[...]",
  "dob": "[..] Mar 1990",
  "bn_mother": "[...]",
  "bn_father": "মোঃ [...]",
  "en_name": "Md. [...]",
  "bn_name": "মোঃ [...]"
}
```

These are the packages we used to achieve this:

* numpy
* dash
* imutils
* pytesseract
* opencv-python
* xlrd
* pandas
* pdf2image
* dash-canvas

Here is the source image: 

![source image](/img/nid-3.jpg "source image")

**Here is the extracted text:**

```
['নাম: রোমানা আক্তার মৌ', 'Name: Romana Akter Mou', 'মাতা: মোসা: আমেনা', 'Date of Birth: 19 Jan 1992', 'ID NO: 2610413965404']
```

Please [reach us](https://dynamicguy.com/contact/) if you need this.
