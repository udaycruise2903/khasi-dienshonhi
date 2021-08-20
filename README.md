# khasi-dienshonhi
Documentation and scripts of khasi-khasi Dictionary Digitalisation project

## Source 

    • author: Kharkongor, Iarington
    • digitalpublicationdate: 2014/11/11
    • date.citation: 1968
    • identifier.barcode: 07019990352114
    • identifier.uri: http://www.new.dli.ernet.in/handle/2015/464423
    • scanningcentre: North Eastern States Libraries
    • totalpages: 493
    • language.iso: Khasi
    • digitalrepublisher: Digital Library Of India
    • publisher: Iarington Kharkongor, Shillong
    • source.library: STATE CENTRAL LIBRARY, SHILLONG, MEGHALAYAA
    
## Tools used 

    • PDF to PNG extraction – ImageMagick convert tool
    • OCR – tesseract 4.1
    • OCR script – Latin
    • text editor – Sublime 
    • custom script language - python 
    • Other softwares – Libre Calc
    • modules - xlsx writer
    • dictionary-platform - Lexonomy

## Process

<ol>
    <li> PDF pages were extracted into PNG images at 600 DPI using imageMagick convert tool.</li>
    <li> All extracted images filenames were inserted into a file.</li>
    <li> Tesseract ocr commands for all the images was written in that file using a text editor.</li>
    <li> Latin script(from tessdata_best) was used for OCR process.</li>
    <li> All tesseract commands for images were run in the terminal to produce output-OCR text.</li>
    <li> The separated OCR textfiles were combined to form a single main file.</li>
    <li> cleantext.py was scripted in python to remove the Guidewords(at the top of a page), page numbers and characters at the begining of a line in the OCR'd textfile.(output-cleaned_textfile.txt)</li>
    <li> ocrtxt2plaintxt.py was scripted in python to remove the newlines in the output of cleaned_textfile.txt</li>
    <li> The Resulting textfile(processed_file.txt) had headword and its meaning line-by-line.</li>
    <li> processed_file.txt was manually reviewed after cloning it for line continuation/broken line errors by comparing it to dictionary PDF.(time taken-4 days)</li>
    <li> OCR process on 11 pages(2.3% of total pages) had to be redone after manual insertion of midline in the corresponding images of input pages.</li>
    <li> The cloned copy was renamed as final_processed_file.txt</li>
    <li> separate file for each letter was created by copy-pasting from final_processed_file.txt in letter_files folder.</li>
    <li> letter_files folder was the input to txt2xlsx.py and wholeline2xlsx.py programs in tx2excel folder.</li>
    <li> txt2xlsx.py program had regex expressions to recognise and capture the headword, part of speech, english meaning, language and additional_information in a line from textfile and output them in the corresponding columns in a excel file(ex: Y.xlsx).</li>
    <li> wholeline2xlsx.py program captured every single line from text file and had output them in corresponding column(khasiMeaning) in the output excel file(ex:Y-lines.xlsx).</li>
    <li> the content of khasiMeaning column was copied to the similar column in the output of txt2xlsx.py(ex: Y.xlsx).</li>
    <li> The above 3 steps were repeated for all letters to create correspoding .xlsx files.</li>
    <li> khasiMeaning column was used as a reference to manually edit the content of all columns in all .xlsx files(time taken- 6 full days). on the other hand, Y-lines.xlsx file and other similar files were deleted.</li>
    <li> a single excel file was created by copy-pasting the contents of all .xlsx files excluding word_number column and empty cells.</li>
    <li> the column names were renamed from (headword, partOfSpeech, khasiMeaning, englishMeaning, language, additionalInfo) to (column_1, column_2,....column_6).</li> 
    <li> This single excel sheet was converted to .xml sheet using online excel-to-xml convertor(https://conversiontools.io/convert/excel-to-xml).</li>
    <li> In the khasi-dict.xml, The column names were edited to previous names using sublime editor and the file was edited to be compatible with external DTD.</li>
    <li> lexonomy was cloned to local computer and was run in the local host.</li>
    <li> A dictionary with title and description was created. under the configure/entry structure tab, a custom schema was chosen and a DTD was scripted.</li>
    <li> khasi-dict.xml file was uploaded to local host and then entry formatting settings were tweaked.</li>
</ol>

## Remaining process

    • Reviewing for character and space errors.
    • Reviewing of khasi and English meanings.

## Issues 

1. severe ink fading ![faded image](https://user-images.githubusercontent.com/56758575/120885078-8ea0be00-c604-11eb-9078-f9d3120702da.png)  

2. unknown ![confusion_1](https://user-images.githubusercontent.com/56758575/120885081-96606280-c604-11eb-869a-4efe575ac856.png)

3. common headwords ![confusion_2](https://user-images.githubusercontent.com/56758575/120885083-98c2bc80-c604-11eb-9c99-6606b80a63a4.png)
    
## observations

<ul>
    <li> using any combination of languages(eng+spa+fra) as option in tesseract OCR leads to lower recognition of characters.</li>
    <li> Midlines in a page indicates the separation of left and right sections of text. A faded midline leads tesseract OCR to read the lines of left and right sections as 1 single line.(i.e., headwords would not have their corresponding meanings).</li>
    <li> less than 3.4 % of 463 pages have been totally misread by OCR which had faded midlines.</li>
    <li> Tesseract OCR takes about 3.5 hours to OCR all 463 pages.</li> 
    <li> Text cleaning using regex results in few headwords missing in every page due to restricted rules occuring simultaneouly in a headword.</li>
    <li> If meaning of  a headword continues in next section of a page or in a new page then a new line is inserted by the OCR. This new lines is to be manually corrected.</li>
    <li> Guide Headwords at the top of the page were removed used a custom text processing program. Although guide headwords reamained for every 2nd or 3rd page due to exception cases from regex conditions.</li>
    <li> Newlines are removed using programs although Meaning of a Headword is found in nextline or few next lines.</li>
    <li> Many headwords occur in a same line. The reason being OCR output have no empty lines after every headword. This error occurs frequently in every page or every 2nd page. This error is to be manually corrected.</li>
    <li>  Whenever a dot/noise has been around a character, OCR has interpreted them for other latin characters with acute markers.(l with strike- ł is occasionally visible in output).</li>  
    <li> After removal of nextlines and making OCR’d text to plain readable text. It is found that some pieces of meaning or part-of-speech of 1 or 2 headwords are jumbled within the page and during manual checking are hard to be traced back to their word and hence are removed.</li>    
    <li> Placing a delimiter after a headword, its part of speech and its meaning is not possible as
        <ol>
            <li> 1 or more headwords exist with same meaning.</li>
            <li> when a headword consists of 2 or more headwords, difficulty arises in plaicing a delimiter aside it.</li>
            <li> part of speech have a dot aside them (v. or n.) but nearly more than a quarter portion of headwords dont have a dot indicating abbreviation of character. Defining any condition would lead selection of all (ex:v or n) characters.</li>
            <li> khasi meaning of a headword varies and is highly inconsistentin matter of number of lines making defining any condition on them hard.</li> 
            <li> although english words can be recognised. Some characters in english words are misinterpreted due to improper characters in input page. (ex: c is misinterpreted for e).</li>
            <li> common brackets only around english meanings would have facilatated any conditions for thier extraction to excel. But a portion of brackets end in flower brackets.</li>
    </ol>
    </li>        
    <li> Manual checking output file after removing nextlines takes 4 days of 8 hours work.</li>
    <li> words with continuation hyphen which is present in dictionary is found in OCR textfile output. Due to no knowledge of khasi language, reviewer would find it difficult to determine continuation hyphen and a phrase.</li>
</ul>
