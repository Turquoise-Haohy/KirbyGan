# Project Link

Seeing the famous PokemonGan, as a Kirby favor, I intent to create a Gan special for kirby(a nintendo character):

<div align=center><img src="https://github.com/Turquoise-Haohy/KirbyGan/blob/main/Kirby%20Mock-Up.png" width="340"></div>


**Link to github**
[KirbyGan Github](https://github.com/Turquoise-Haohy/KirbyGan.git)


**Link to Colab**
<a href="https://colab.research.google.com/drive/1AE7N2gNOWuvaPkcjz6VAcDoYZ7inxdwC?usp=sharing">
<img src="https://colab.research.google.com/assets/colab-badge.svg"
     alt="Open in Colab"
/>
</a>


**Video of several example**




https://user-images.githubusercontent.com/73295564/175958426-f464f56c-b572-477d-8176-80e634e29413.mp4




---

# Process
### Image Process
First of all, I find that there is no existing dataset for kirby only on kaggle or Huggingface, so I decided to create one by myself.
I decided to use web crawler to scrape images from Google, and I've found this: [AutoCrawler](https://github.com/YoongiKim/AutoCrawler.git), works soundly, 
then I got 703 images of Kirby.

<div align=center><img src="https://github.com/Turquoise-Haohy/KirbyGan/blob/main/kirbyDataset.jpeg" width="720"></div>

After processd by hands😭, also I used python to clip them into size of 256x256， I uploaded this dataset to kaggle: [KirbyDataset](https://www.kaggle.com/datasets/turbihao/nintendo-kirby-dataset)

**or download with kaggle API:**

```
kaggle datasets download -d turbihao/nintendo-kirby-dataset
```
**Clip the images to 256*256**

```
imgs = []
path = "/Users/turqoise/Downloads/AutoCrawler-master/download/kirby"
new_path = "/Users/turqoise/Downloads/kirby"
valid_images = [".jpg",".gif",".png",".tga",".jpeg"]
size = 256

for i,f in enumerate(os.listdir(path)):
    ext = os.path.splitext(f)[1]
    if ext.lower() not in valid_images:
        continue
    
    img = Image.open(os.path.join(path,f))
    w,h = img.size
    filename = str(i) + ".jpg"
    print(filename)
    if w==h:
        img.resize((size,size)).convert('RGB').save(os.path.join(new_path,filename))
    
    elif w>h:
        img.crop(((w-h)/2,0,(w-h)/2+h,h)).resize((size,size)).convert('RGB').save(os.path.join(new_path,filename))
    
    elif h>w:
        img.crop((0,(h-w)/2,w,(h-w)/2+w)).resize((size,size)).convert('RGB').save(os.path.join(new_path,filename))
        

```
---

### Choose StyleGan3

the PokemonGan is based on DCGAN, while I find that the stylegan3 is up to date and may have better performance. 
So I choose the styleGan3 as my main method. 

Here's the official link to it: [nvlabs styleGan3](https://nvlabs.github.io/stylegan3/)，

and also someone has established API on Colab with some pre-trained model as `.pkl` file to play with.

[github link](https://github.com/justinjohn0306/StyleGAN3-CLIP-ColabNB.git)

<a href="https://colab.research.google.com/github/justinjohn0306/StyleGAN3-CLIP-ColabNB/blob/main/StyleGAN3%2BCLIP_v2.ipynb">
<img src="https://colab.research.google.com/assets/colab-badge.svg"
     alt="Open in Colab"
/>
</a>

---

### Pre-trian my own `*.pkl` model

the model has many specific version requirement in terms of downloading the packages, I finnaly find this tutorials by Jeff Heaton suits what I want: 
[video tutorial on youtube](https://youtu.be/R546LYsQk5M)

---

[github Link of the process](https://github.com/jeffheaton/t81_558_deep_learning.git)

---

each 10 ticks, the model would generate a series of fake images, seeing the development:

<div align=center><img src="https://github.com/Turquoise-Haohy/KirbyGan/blob/main/fakes000000.png" width="720"></div>

<div align=center><img src="https://github.com/Turquoise-Haohy/KirbyGan/blob/main/fakes000080.png" width="720"></div>

<div align=center><img src="https://github.com/Turquoise-Haohy/KirbyGan/blob/main/fakes000160.png" width="720"></div>

<div align=center><img src="https://github.com/Turquoise-Haohy/KirbyGan/blob/main/fakes000200.png" width="720"></div>

---

# Relection

As the feature of kirby is becoming various shapes and stuffs, so I am quite comfortable about the final results that the images seem to be like fluid, hahahah..
But my kirby do not have feet...I guess this is due to my dataset is not so clearly as my processing of the images is not enough with various backgrounds in each images. 
Also I might test more epoches in the future. Thanks!
