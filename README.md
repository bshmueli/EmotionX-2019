# Social EmotionX 2019 Data

## Paper and Citation

The SocialNLP EmotionX 2019 paper is available at [SocialNLP EmotionX 2019 Challenge Overview: Predicting Emotions in Spoken Dialogues and Chats](https://arxiv.org/abs/1909.07734]).

Kindly cite the paper using the following BibTex entry:

```
@misc{shmueli2019socialnlpemotionx2019challenge,
      title={SocialNLP EmotionX 2019 Challenge Overview: Predicting Emotions in Spoken Dialogues and Chats}, 
      author={Boaz Shmueli and Lun-Wei Ku},
      year={2019},
      eprint={1909.07734},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/1909.07734}, 
}
```

## Data description
Each of the two datasets contains 1000 English-language dialogues, duplicated in two files: original and augmented. Note that the Friends dialogues are speech-based, while the EmotionPush dialogues are chat-based.

The datasets files are in JSON format.

## Original Data
Each of the original data files (`friends.json`, `emotionpush.json`) contain an array of dialogues objects, and each dialogue object is an array of line objects. Here is an example line object:

        {
            "speaker": "Chandler",
            "utterance": "My duties?  All right.",
            "emotion": "surprise",
            "annotation": "2000030"
        },
Each line object includes `speaker`, `utterance`, `emotion`, and `annotation` strings. 

Each `utterance` was annotated by five people. The `annotation` string contains the raw count of votes for each emotion by the annotators. The order of the emotions in the string is [neutral, joy, sadness, fear, anger,  surprise, disgust]. For example, in the above line, `"2000030"` denotes that two annotators voted for `"neutral"`, and three voted for `"surprise"`. Note that the sum of the votes is always five, since the dialogues were annotated by five annotators.

The `emotion` string is the `utterance`'s label. It is calculated from the annotation as follows. If a certain emotion has an absolute majority of votes (i.e., three or more votes), then that `utterance` is labeled with the majority emotion. Otherwise, `the utterance` is labeled with the `"non-neutral"` label. In the above example, the emotion is labeled `"surprise"` because  surprise got three votes.

## New in 2019: Augmented data
This year we added **augmented** datasets. The augmented datasets files are `friends.augmented.json` and `emotionpush.augmented.json`. They are similar to the original data files, but include multiple utterances for each spoken or typed line. We used Google Translate to translate each utterance from English into three target languages (German, French, and Italian), then used Google Translate to translate from the target language back into English. The resulting utterances (`utterance_de`, `utterance_fr` and `utterance_it`) are included together in the same object with the original utterance.

Here is an example line object from the augmented Friends file (`friends.augmented.json`):

        {
            "speaker": "Ross",
            "utterance": "It was. It was an amazing night.",
            "emotion": "joy",
            "annotation": "0500000",
            "utterance_de": "It was. It was a great night.",
            "utterance_fr": "It was. It was an incredible night.",
            "utterance_it": "Was. It was a fantastic night."
        },
While some of the double-translated utterances are identical to the original ones, sometimes they are not. The double-translated utterances thus have the potential to serve as additional labeled data points for training, and can be used at your discretion. 

A small difference between the **original** and **augmented** files is that the utterances in the augmented data files have also been normalized to use ASCII characters, while the original files use some non-ASCII characters.

Please specify the dataset used when writing your report.

## Sample annotations
Here are some more examples of how the labels are calculated:

`"annotation": "2003000" ⟶  "emotion": "fear"`

`"annotation": "0500000" ⟶ "emotion": "joy"`

`"annotation": "2011010" ⟶ "emotion": "non-neutral"`
