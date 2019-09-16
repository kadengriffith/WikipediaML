# WikipediaML

---

This is an adapted version of [TFDS wikipedia dataset code](https://github.com/tensorflow/datasets/blob/master/tensorflow_datasets/text/wikipedia.py).

To ensure you have all of the required packages installed run:

```
pip install apache-beam mwparserfromhell urllib3 tensorflow-datasets tensorflow
```

This file will work with Python 2. Once the data is downloaded, the script works with Python 3 or Python 2. When Python 2 dies in January, I will update this to solely run with Python 3.

The downloads are very large, but once completed this will save the TF dataset in the download directory you specify under a folder named **custom_wikipedia**. Once you download, you will re-use the existing dataset by default. You can change the version if you wish to re-download a newer version using the same directory.

To find specific scrapes first visit: [Wikimedia](https://dumps.wikimedia.org/backup-index.html), then find the language code you want (e.g., "en" for English, or "fr" for French), and finally find the date of the dump you wish to download. Keep in mind that these dumps are rolling, so if a few months pass and you wish to re-use this class as a downloader you will need to find a date that exists on the Wikimedia server. For example at the time of me writing this, my most current date is: 20190901.

Just drop the WikipediaML.py file into your project and use as if you are using the tfds.load(). Not all of the tfds.load() API is present so check out the API section below.

If the binary exists, you will not re-download the dump unless you change the force_download flag in the load function to True. Expect the process to take >12hrs.

##### NOTE: Make sure your download directory is changed if you want to download more than one version, the files may be overwritten unintentionally since this generator acts as a universal gateway.

#### API

**WikipediaML**

- **Type**: Class
- **Description**: A universal wrapper for downloading Wikipedia dumps and converting them into TensorFlow Datasets.

- **Methods**:

  - **load**(download, download_mode)
    - **Arguments**:
      - **download**: _boolean_; Default is False. If True, the download will be forced.
      - **download_mode**: _tfds.GenerateMode_; Default is tfds.GenerateMode.REUSE_DATASET_IF_EXISTS. Options include { FORCE_REDOWNLOAD, REUSE_DATASET_IF_EXISTS, and REUSE_CACHE_IF_EXISTS }.

- **Arguments**:

  - **language**: _string_; Default is None. This is a language code specified by Wikimedia.
  - **date**: _int_; Default is None. This is a YYYYMMDD time stamp specified by Wikimedia.
  - **data_dir**: _string_; Default is None. This is a relative filepath (from WikipediaML.py) for the data you wish to download. This allows for your data to be independent from the current directory you are working in.
  - **split**: _tfds.Split_; Default is tfds.Split.TRAIN. This is the split you wish to specify for the TFDS. Options include { tfds.Split.TRAIN, tfds.Split.TEST, None }.
  - **as_supervised**: _boolean_; Default is False.
  - **batch_size**: _int_; Default is None,
  - **shuffle_files**: _boolean_; Default is False.
  - **code_messages**: _boolean_; Default is False. Toggles my print statements that get annoying after the data has been downloaded and processed successfully. I recommend turning this to true when you download so you can identify what process is in progress.

#### Example Usage

```
# Get the English dataset
tfds = WikipediaML(language="en",
                   date=20190601,
                   data_dir="data/en_wikipedia").load()
```
