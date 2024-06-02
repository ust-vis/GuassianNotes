# Gaussian Splatting Notes
## This repo serves as a place to put my finding on Gaussian splatting. 
This image was synthesized via Gaussian splatting
![image](https://github.com/ust-vis/GuassianNotes/assets/19912037/2e1cef11-2699-43d2-a27a-3731b4e76f2d)

Compared to CDEP, Gaussian splatting can produce superior visual fidelity with fewer artifacts at a similar performance level. However, the approach’s drawback is the large amount of data required for a good result, the time it takes to optimize the Gaussians, and the increased amount of artifacting that occurs when moving far away from the initial capture positions.

## Creating Gaussian Splats
I attempted to get the [original paper source](https://github.com/graphdeco-inria/gaussian-splatting) without much success. Then I discovered an application called Postshot by Jawset. It encapsulates the functionality of training a Gaussian splat into a user-friendly interface. From this, I was able to start training Gaussian splats.

My system, which includes an RTX3060, a Ryzen5800x, and 32GB of RAM, managed to train/optimize a scene in 45 minutes. This was the quickest I was able to get a result and it wasn't great. There was a lot of artifacting and blurriness.To achieve anything that looked decent, it took around 1.5 to 2 hours. To make matters worse, training often fails halfway through, requiring me to restart and capture new/more camera angles. This makes creating splats a long and time-consuming process.

Additionally, I’ve found that at least 100 images are needed for an acceptable result and 200 for the best quality. Furthermore, these captures need to be from all possible positions that the environment or object would ever be viewed from.

## Viewing Gaussian Splats
There are three file formats that can store Gaussian splats: (.ply), (.splat), and a custom proprietary file format used by Luma AI. The (.splat) format seems a bit more optimized from what I can tell, but more applications support (.ply). To view Gaussians, there are a few options. Luma AI has a library that can easily be integrated into an existing site. However, I found it unfortunately can only load Luma AI file formats after trying to integrate it into this [repo](https://github.com/ust-vis/GaussianViewer). I also found this [library](https://github.com/antimatter15/splat) that looked promising but I encountered some CORS issues and wasn’t able to get it working, though the demo does look very promising. Another one is [Tiny Guassian Splatting viewer](https://github.com/limacv/GaussianSplattingViewer) This is a Python application that can view splats natively instead of through WebGL. It supports CUDA sorting of the splats, though I wasn’t able to get this running on my machine.

The main tool I recommend, however, is [supersplat](https://playcanvas.com/supersplat/editor). It’s an in-browser viewer/editor for Gaussian Splats that works very well. It even supports compressing splat files down which I've done for the attached splats under the release section of this repo. I’ve often seen savings of 10x doing this with very little loss in visual fidelity.

## Further work
One thing Gaussian splatting does exceptionally well, which isn’t talked about much, is its ability to effectively compress a 3D representation of space. With modern techniques outlined in this paper, entire rooms can be rasterized in near photo-realistic quality while only taking up 15 megabytes of RAM. Additionally, Gaussian splats can be rendered extremely quickly and efficiently. I was able to achieve similar or better performance compared to the WebGL implementation of CDEP under WebGL implementations of splat viewers, and I suspect the performance gap would only widen when running native implementations.

An idea I have is to take a CDEP algorithm that only requires a couple of 360 shots to create, then utilize hundreds of planar re-projections of the CDEP algorithm to create a compressed and highly efficient representation of 3D space.

I implemented a proof of concept by adding the ability to take planar screenshots while flying around a CDEP scene. These images were then used to train Gaussian splats:

https://github.com/ust-vis/GuassianNotes/assets/19912037/03ddecb2-d935-41a1-b20b-a62e1d2ebe92

The quality is poor due to suboptimal camera positioning and a lack of enough captures, but theoretically, this could present an opportunity to render CDEP scenes with higher performance and less memory usage. It could also be used in cases where a Gaussian splat is needed for workflow reasons but only a small amount of captures are available.

## Trying the trained Gaussians. 
In the releases section of this repository, I have posted a zip file with both the splats trained on the original model and the CDEP projections. These can be opened in supersplat for easy viewing and editing.
