# Gaussian Splatting Notes
This image was synthesized via Gaussian splatting
![image](https://github.com/ust-vis/GuassianNotes/assets/19912037/2e1cef11-2699-43d2-a27a-3731b4e76f2d)

## This repo serves as a place to put my finding on Gaussian splatting. 
In comparison to CDEP Gaussian splatting is able to produce much better visual fidelity with less artifacting at similar performance. The drawback of the approach however is the amount of data required to get a good result and the time it takes to optimize the Gaussians. 

## Creating Gaussian Splats
I tried getting the [original paper](https://github.com/graphdeco-inria/gaussian-splatting) running without much luck. Then I stumbled upon an application called [Postshot](https://www.jawset.com/) by Jawset. It wraps the functionality of training a Gaussian splat into a nice ui. From this I was able to start training gaussian splats. 

My system has an RTX3060, a ryzen5800x and 32 gigs of ram, the fastest I ever got a scene to train / optimize was 45 minutes. And these weren't good results. To get anything that looked decent it took around 1.5 to 2 hours. This isn't great but to make matters worse often times training might fail half way through requiring you to restart. This makes creating splats a long time consuming process.

## Viewing Gaussian Splats
There are three file formats that can store Gaussian splats, (.ply) and (.splat) and a custom proprietary file format used by Luma AI. (.splat) is a little more optimized from what I can tell but more applications support (.ply). To view Gaussians there are a couple options. Luma AI has a library that can easily be integrated into an existing site. However, it unfortunately can only load Luma AI file formats. 


## Further work
One thing Gaussian splatting does really well that isn't talked about much is its ability to effectively compress a 3d representation of space. With modern techniques outlined in this [paper](https://dl.acm.org/doi/abs/10.1145/3651282) entire rooms can be rasterized in near photo-realistic quality while only taking up 15 megabytes of ram. Additionally, Gaussian splats are able to be rendered extremely quickly and efficiently. I was able to get similar performance to the webgl implementation of 

## Trying the trained Gaussians. 
