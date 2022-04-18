# Optical Character Recognition (OCR)


## How to Run

1. Fork or clone OCR repo (OR locate directory on Midway by typing `cd /project2/adukia/miie/text_analysis/code/OCR`)
2. (Optional) If you have access to a compute node that has internet access, you can connect to it now. Otherwise, skip this step.
3. Load in Python (`module load python`) and download the dependencies in one of two ways:
    - In the OCR folder, type:
    ```
    $ pip install --user -r requirements.txt
    ```
    - OR Activate the virtual environment if you have access to the adukia project space on Midway
    ```
    $ source /project2/adukia/miie/text_analysis/dependencies/OCR/OCR/bin/activate
    ```
3. Edit and save `OCR/src/input.yaml` file, see details of possible customizations below
4. If using Google Vision, type:
   ```
   export GOOGLE_APPLICATION_CREDENTIALS=src/google_auth_key/TextAnalysis-8fc4fa534750.json
   ```
   **Note:** If you have forked/cloned this repository you need to specify the path to your own google credentials above to replace ours (`src/google_auth_key/TextAnalysis-8fc4fa534750.json`)

5. Run the pipeline:
  ```
  $ python src/main.py
  ```

## Default input.yaml file

```
---
raw_data_directory: /path/to/raw_data_dir # only required input
...
```

## Example input.yaml file with all features
```
---
raw_data_directory: /path/to/raw_data_dir # only required input
combination_type: both 
output_combined: /path/to/output/combined_dir
output_uncombined: /path/to/output/uncombined_dir/
ocr_method: Google Vision
confidence_threshold: 0.5
image_ordering: underscore_numerical
language: []
project_id: ocr_google_vision
model_id: 1234
remove_cover_ends: True
preprocess_images: True
...
```

**The data directory containing images of text is the only required input. Custom and default options are detailed below.**


| Input | Description |
| --- | --- |
| Raw Data Directory ***(required)*** | User filepath to raw scan data directory|
| Output Combined | User filepath for OCR output for combined files ***(default is /path/to/raw_data_dir/../ocr_output)*** |
| Output Uncombined | User filepath for OCR output for uncombined files (each OCR'd file is stored as a separate file) ***(default is /path/to/raw_data_dir/../ocr_output)*** |
| OCR Method | Tesseract or Google Vision ***(default is Tesseract)*** |
| Confidence Threshold | Value from 0-1 indicating confidence threshold per scan ***(default is 0.5)*** |
| Image Ordering | Ordering for images in a directory: alphabetical *(a.jpg, b.jpg, c.jpg)*,numerical *(1.jpg, 2.jpg, 3.jpg)*, dash_numerical *(book-1.jpg, book-2.jpg, book-3.jpg)*, or underscore_numerical *(book_1.jpg, book_2.jpg, book_3.jpg)* ***(default is underscore_numerical)*** |
| Language | List of languages present in the scans. If unknown, provide an empty list and allow auto-language-detection. Possible languages currently include English, Spanish, Chinese, and Hindi. Example input could be ["English", "Spanish"]. ***(default is empty list)***|
| Project ID | If using google vision, project ID for classifying main text vs cover/end text ***(default is None)***|
| Model ID | If using google vision, model ID for the trained model to classify main text vs cover/end text ***(default is None)*** |
| Remove Cover & Ends | Whether or not to use text model to identify and remove cover and end pages from text ***(default is False)*** |
| Preprocess Images | Whether or not to preprocess (compress, deskew) images before running OCR ***(default is False)*** | 


## Data Structure Details

The suggested image type is JPEG, but this platform supports [eleven image types](https://docs.opencv.org/3.4/d4/da8/group__imgcodecs.html#ga288b8b3da0892bd651fce07b3bbd3a56).


If your input folder is "data", and structured as follows:

```
data
|
|-------> group1
|           |
|           |-------> book1
|                           |
|                           |-------> page_1.jpg
|                           |-------> page_2.jpg
|                           |-------> page_3.jpg
|                                              .
|                                              .
|                                              .
|-------> group2
            |
            |-------> book2
                            |
                            |-------> page_1.jpg
                            |-------> page_2.jpg
                            |-------> page_3.jpg
                                               .
                                               .
                                               .

```

Your output will be structured as shown below, where the order that images are combined and the location of the output are based on user inputs. The structure of the output will mirror that of the input, combining all images in the same directory into a single text file.
```
output
|
|-------> group1
|           |
|           |-------> book1.txt                                                                     
|                                              
|-------> group2
            |
            |-------> book2.txt

```



