---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
---

_By [Matthew Lincoln](https://matthewlincoln.net)_

Playing on George Kubler's anthropology of visual style, _The Shape of Time_[^kubler], this app finds a path of similar images through the Rijksmuseum collections, at times moving forwards in time, and at times moving backwards.

Sometimes the results are uncanny. Other times they are laughably misguided. But they each offer an alternative pathway into a large art collection bound together by more formal similarities than we usually chart in our textbooks and exhibitions.

[^kubler]: George Kubler, _The Shape of Time: Remarks on the History of Things_ (New Haven: Yale University Press, 1962).

It produces both animated GIFs that are tweeted under [@MechaKubler](https://twitter.com/MechaKubler).
This companion site hosts pages for each tweet with links to all the artworks.

<figure><a href="/pathways/88735e8915ee1900340d62ec278018bf.html"><img src="/assets/images/88735e8915ee1900340d62ec278018bf.gif" /></a></figure>

**[See pathways found so far.](/pathways)**

## Why?

Inspired by Google Cultural Institute's ["X Degrees of Separation"](https://artsexperiments.withgoogle.com/xdegrees/), I was curious to see if it was possible to recreate that app by hand using a smaller collection of works, and constraining the kinds of paths that would get drawn between two given artworks.
Was it possible to make this path move only forward in time? Or only backwards? To only consider a certain set of objects by type or nationality?
[The idea had been gnawing at me for some time.](https://twitter.com/matthewdlincoln/status/959253318160744448)

## How?

To find a "visual path" between two artworks, I used the penultimate max pooling layer of the pre-trained VGG 16 convolutional neural network[^vgg] to produce multidimensional embeddings for over 120,000 images of artworks in the [Rijksmuseum collections](https://www.rijksmuseum.nl/).
Artworks close to each other in this vector space tend to share visual features (although fine-tuning the network that produced these embeddings would go a long way to fostering similarities more familiar to art historians in this domain.[^seguin])
By drawing an ideal path between two points in this space, we can find real points (i.e. artworks) close to this path, effectively producing a list of images evenly-spaced in visual similarity - at least, the similarity recognized by VGG 16.
The R package [pathway](https://github.com/mdlincoln/pathway) powers this search, and offers some functions for constraining the search to move in one direction - in our case, either forward or backwards through the "time" represented by the creation dates given to these objects by Rijksmuseum curators.

<figure><a href="/pathways/88735e8915ee1900340d62ec278018bf.html"><img src="/assets/images/88735e8915ee1900340d62ec278018bf.png" /></a><figcaption>A representation of the visual fingerprints of ~120k images, the multidimensional space returned by VGG-18 here boiled down to just two principal components, with the start, end, and intermediate images highlighted.</figcaption></figure>

[^seguin]: This avenue is already being explored by Benoit Seguin et al., “Visual Link Retrieval in a Database of Paintings,” in _Computer Vision – ECCV 2016 Workshops_, ed. Gang Hua and Hervé Jégou, vol. 9913 (Cham: Springer International Publishing, 2016), 753–67, <https://doi.org/10.1007/978-3-319-46604-0_52>.

[^vgg]: Karen Simonyan and Andrew Zisserman, “Very Deep Convolutional Networks for Large-Scale Image Recognition,” ArXiv:1409.1556 [Cs], September 4, 2014, <http://arxiv.org/abs/1409.1556>.

Mechanical Kubler does not producing real causal chains of visual influence. What it does do is deliberately remove some of the magic from GCI's "X Degrees of Separation" app, more closely binding it to the idea of historical process. Hopefully this can encourage us to revisit Kubler's ideas about how to write histories of visual morphologies even in the absence of social context - ideas all the more important in an age where more images are being looked at by machines than by humans.
