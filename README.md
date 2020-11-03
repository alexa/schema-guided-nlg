
The Schema-Guided Natural Language Generation (SG-NLG) Dataset
==============================================================


Overview
--------

The SG-NLG dataset is a pre-processed version of the [DSTC8 Schema-Guided Dialogue SGD dataset](https://github.com/google-research-datasets/dstc8-schema-guided-dialogue), designed specifically for data-to-text NLG. The original DSTC8 SGD contains ~20,000 dialogues spanning across ~20 domains.

This SG-NLG dataset is designed to make it easier to conduct NLG experiments on the SGD data. We pre-process SGD by pairing the schema for each system turn with the corresponding set of natural language strings that realize it. We also “delexicalize” the prompts (replace related values with fixed names) to convert them into templates that make them more generic for use within a dialog system.

The final SG-NLG dataset is composed of nearly 4K MRs and over 140K templates. Full details on the pre-processing step are given in the paper (see [Citation](#citation) section). Note that we only use the train and dev splits of the original DSTC8 SGD dataset, since at the time of creation the SGD test set did not yet include user intents (which are a necessary part of our pre-processing). Thus, we use SGD train to create our train+dev sets (split into 90% train and 10% dev), and use SGD dev as our test set.


Sample Instance
---------------

The excerpt below shows a sample data instance:
```
  {
    "MR": [
      {
        "confirm": {
          "hotel_name": "$hotel_name1"
        }
      },
      {
        "confirm": {
          "destination": "$destination1"
        }
      }
    ],
    "Templates": [
      "confirm these details if you would: the name of the hotel is $hotel_name1 located in the city of $destination1.",
      "please verify the following information: the hotel is $hotel_name1 at $destination1.",
      "so to double-check: the hotel is $hotel_name1 in $destination1..",
      "the hotel is $hotel_name1 and it is in $destination1. is this correct?"
    ],
    "SlotDescription": [
      "name of the hotel",
      "location of the hotel"
    ],
    "Domain": "hotels_1",
    "DomainDescription": "a popular service for searching and reserving rooms in hotels",
    "Intent": "reservehotel",
    "IntentDescription": "reserve a selected hotel for given dates",
    "MRNaturalLanguage": "please confirm that the hotel name is $hotel_name1. please confirm that the destination is $destination1.",
    "ID": "001669"
  },
```


Description of Fields
---------------------

 - *MR:* The meaning representation, i.e., a list of dictionaries of `{dialog_act: {slot: value}}` describing the content to be expressed in the corresponding templates.
 - *Templates*: The templates that realize the content in the MR. These are delexicalized to include the value placeholders from the MR instead of the original values in the natural language string for template-based NLG.
 - *SlotDescription:* Descriptions of the slots from the MR (pulled from the SGD schema files).
 - *Domain:* Domain of the MR (specifically, the SGD "service").
 - *DomainDescription:* Description of the domain (service).
 - *Intent:* The intent of the user turn preceding the current system turn.
 - *IntentDescription:* Description of the user intent (pulled from the SGD schema files).
 - *MRNaturalLanguage:* Rule-based natural language version of the MR (see paper for more details).
 - *ID:* Numeric ID for the sample.


Data Files
----------

The dataset consists of the JSON data files along with meta files containing additional information to enable the mapping of each prompt to the original, lexicalized version from the SGD dataset.

```
├── data
│   ├── train.json
│   ├── dev.json
│   └── test.json
└── meta
    ├── train_meta.json
    ├── dev_meta.json
    └── test_meta.json
```

License
-------

CC BY-SA 4.0 (see LICENSE).


Citation
-------
If using this dataset, please cite the following paper in any relevant work:
~~~
@article{du2020schema,
  title={Schema-Guided  Natural  Language  Generation},
  author={Du,  Yuheng  and  Oraby,  Shereen  and  Perera,  Vittorio  and  Shen,  Minmin  and  Narayan-Chen,  Anjali  and  Chung,  Tagyoung  and  Venkatesh,  Anu  and  Hakkani-Tur,  Dilek},
  journal={arXiv  preprint  arXiv:2005.05480},
  year={2020}
}
