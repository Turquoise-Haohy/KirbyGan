
Seeing the famous PokemonGan, as a Kirby favor, I intent to create a Gan special for kirby(a nintendo character)

First of all, I find that there is no existing dataset for kirby only on kaggle or Huggingface, so I decided to create one by myself.
I decided to use web crawler to scrape images from Google, and I've found this: [AutoCrawler](https://github.com/YoongiKim/AutoCrawler.git), works soundly, 
then I got 703 images of Kirby.



After processd by hands😭, also I used python to clip them into size of 256x256， I uploaded this dataset to kaggle: [KirbyDataset](https://www.kaggle.com/datasets/turbihao/nintendo-kirby-dataset)

**or download with kaggle API:**

> kaggle datasets download -d turbihao/nintendo-kirby-dataset

