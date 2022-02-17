## Automatic morpheme splitting program in English and Hungarian
By: Pfeifer Dániel<br>
N65V6V

This is a program that, given an input word, is capable of slpitting the word into morphemes (word stem and particles). I will first try to accomplish this in English, since there aren't nearly as many morphemes as in Hungarian, then if all goes well, I'll continie the project on Hungarian words. If the latter doesn't work out, I'll still have something to show.

Here are some examples for input and outputs:

- English: interestingly = interesting (adjective) + ly (adverb marker)
- Hungarian: kutyátokhoz = kutya (noun) + tok (possession particle Plural/2) + hoz (relation marker particle)

Short English and Hungarian data is available here: https://github.com/sigmorphon/2019/tree/master/task1<br>
Long Hungarian data is available here: ftp://ftp.mokk.bme.hu/Language/Hungarian/Corp/Webcorp/ana/<br>
And this is an online tool that's capable of splitting any Hungarian word into its morphemes: https://e-magyar.hu/hu/

## Solution

My work can be found in my `WORKSPACE` subfolder. The order of which I've created my Jupyter Notebooks can be read from their name. Most of these are just to show my work, and only the last one (**07 Runnable_Morpheme_Decomposer.ipynb**) is truely runnable, using presaved files from the rest of the Notebooks. (The others might run for multiple days, especially number **04**.):

- **01 Baseline_MorphemeDecomposer.ipynb**: The Morpheme Decomposition accomplished for the English language. A simple grammatical model, no Data Science / Neural Networks have been used.
- **02 Plans_And_UniversalDependencies_Data.ipynb**: My first attempt using the `hu_szeged-ud-train.conllu` data to train the Neural Networks. However, this has proved to be insufficient, only contaning ~20,000 entries. (This is what I call "Short Hungarian data".)
- **03 More_Data.ipynb**: Using the "Long Hungarian Data", containing about ~5,000,000 entries. This Notebook breaks up the data and creates conveniant dataframes out of it.
- **04 Neural_Networks.ipynb**: Using the previous data, I have created Neural Network models to decompose nouns, verbs, adjectives, determiners and numbers. This Notebook ran by far the longest. The Keras Neural Network models have been saved separately into H5 files.
- **05 Word_Type_Neural_Network.ipynb**: This Notebook only contains one Neural Network model: one that distinguishes between nouns, verbs, adjectives, determiners and numbers. For the rest of the word types, I have used a Set-Similarity model.
- **06 Set_Similarity.ipynb**: Using <a href="https://en.wikipedia.org/wiki/Levenshtein_distance">Levenshtein distance</a> between words and averaging it through sets of words, this Notebook is capable of predicting the word types of simpler words (with some error, of course).
- **07 Runnable_Morpheme_Decomposer.ipynb**: The final combined model. This Notebook is entirely runnnable, granted all files from the `WORKSPACE` folder are in the user's directory. It uses the pretrained Keras models for nouns, verbs, adjectives, determiners and numbers; and some smaller dataframes for adverbs, articles, conjugations, determiners, numbers, onomatopeias, postpositions, prepositions, and utterences / interjections. (Determiners and Numbers appear in both lists - a combined model has been used for those.)

(**Note:** If you wish to run all the Notebooks regardless, please go into the `DATA` folder, read `all_morphtable_used_data.txt`, and follow the instructions to create a file called `all_morphtable.txt` right next to the file you just read.)
