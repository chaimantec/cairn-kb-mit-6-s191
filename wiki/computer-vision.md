# Computer vision

Computer vision is getting a machine to see: "to know what is where by looking". MIT 6.S191 covers it
in [lecture 3](03-convolutional-neural-networks.md), where Alexander Amini builds up from what an image
is to a computer, through why features must be learned rather than hand-engineered, to the tasks one
convolutional architecture can do: classification, object detection, semantic segmentation and control.
How the networks themselves work is on the [convolutional neural networks](convolutional-neural-networks.md)
page.

## More than recognition

Vision is more than recognizing what is in an image; it is understanding the dynamics of a scene
(lecture 3, ≈0:53–1:39). In slide 3's street scene, two cars look alike but behave differently: one has
probably stopped because pedestrians are about to cross and will move again soon, while the other is
probably parked. Slide 3 puts the goal as "To discover from images what is present in the world, where
things are, what actions are taking place, to predict and anticipate events in the world". Deep learning
has spread into robotics, mobile computing, biology and medicine, autonomous driving and accessibility
(slide 4, ≈2:24). Its early applications were mostly recognition: facial **detection**, which finds a
face, and then facial **recognition**, which relates the face to a particular person (slide 5,
≈2:24–3:10).

![Slide 3: To discover from images what is present in the world](../raw/images/03-convolutional-neural-networks/slide-3.jpg)

*Lecture 3, slide 3 — objects, their locations and their likely motion in one street scene.*

## Images are numbers

Computers "don't see in color space, they see in numbers" (≈3:56). A grayscale image is a 2D matrix with
one brightness value per pixel; a colour image is three such matrices, for red, green and blue, so it is
a three-dimensional matrix whose third dimension has size three (slides 10–12, ≈4:43–5:28). Amini
describes brightness as ranging from zero to one; slide 12 prints the values as whole numbers in
[0, 255] and gives "1080x1080x3 for an RGB image" as an example size.

![Slide 12: Images are Numbers](../raw/images/03-convolutional-neural-networks/slide-12.jpg)

*Lecture 3, slide 12 — a portrait, the portrait with its pixel values printed on it, and the matrix alone.*

Vision tasks are regression, with a continuous output, or classification, with a class label or a
probability for each class (slide 13, ≈5:28–6:14). Lecture 3's example classifies a portrait as Lincoln,
Washington, Jefferson or Obama: a two-dimensional input mapped to a fixed-size one-dimensional vector,
on the slide Lincoln 0.8, Washington 0.1, Jefferson 0.05 and Obama 0.05.

## Features: engineered or learned

Classification works by detecting lower-level features and composing them into higher-level ones: eyes,
noses and ears for a face; wheels, license plates and headlights for a car; doors and windows for a house
(slide 14, ≈7:00–7:46). The traditional pipeline uses domain knowledge to define such features by hand,
then detects them to classify (slide 15, ≈8:32). It breaks down because images vary so much, both within
a class and between classes. Slide 16 shows seven sources of variation: viewpoint, illumination
conditions, scale, deformation, background clutter, occlusion and intra-class variation. And humans "are
just not very good at clearly defining what those lower-level features should be" (≈10:05).

![Slide 16: Manual Feature Extraction](../raw/images/03-convolutional-neural-networks/slide-16.jpg)

*Lecture 3, slide 16 — the variation that defeats hand-defined features.*

Deep learning instead learns the features, and what the good features are, directly from data, as a
hierarchy through the depth of the network (slide 18, ≈10:05–11:39). Feeding images to a fully connected
network would throw away their spatial structure, so vision uses convolutional networks; see
[convolutional neural networks](convolutional-neural-networks.md) and
[what is deep learning?](what-is-deep-learning.md).

## One architecture, many tasks

A CNN splits into a feature-learning part and a task-specific head. The feature-learning part produces
general-purpose features, so it can stay the same while only the head changes (slide 56, ≈44:02–44:47).

**Classification.** One label for the image. Lecture 3's example is healthcare: a CNN-based system
outperformed expert radiologists at detecting breast cancer from mammograms (slide 57, McKinney+
*Nature* 2020), which Amini describes as a paper "from some time ago" — "we've gone much farther than
this" (≈45:34).

**Object detection.** A bounding box for every object in the image — its x and y coordinates, width and
height — and a class for each box, so the output must hold a variable number of boxes (slides 58–59,
≈45:34–47:10). Trying random boxes is far too expensive (slide 60). Proposing boxes with a heuristic
first, the approach slide 61 names R-CNN (Girshick+ *CVPR* 2014), is better but slow and brittle,
because the proposals are not learned (≈47:55–48:43). The widely used fix, which slide 62 names Faster
R-CNN (Ren+ 2016), runs the whole image once through the convolutional feature extractor, proposes
candidate boxes from the features, and classifies each. The whole model is end-to-end differentiable,
so bad boxes teach it to propose better ones (≈49:29–51:00). Aloud, Amini says the proposals around
blobs in the features can come from heuristics such as thresholding (≈50:15); slide 62 calls the step a
learned "Region proposal network".

![Slide 59: Object Detection](../raw/images/03-convolutional-neural-networks/slide-59.jpg)

*Lecture 3, slide 59 — detection outputs a class and a box for every object, however many there are.*

**Semantic segmentation.** A class for every pixel, an image-to-image task (≈51:00–52:32). The
convolutional, downsampling front is unchanged; the back upsamples to produce an output image of per-pixel
classes, and the model is trained as a classifier. Slide 63 names this a fully convolutional network
(FCN, Long+ *CVPR* 2015), with upsampling layers `tf.keras.layers.Conv2DTranspose` and
`torch.nn.ConvTranspose2d`.

![Slide 63: Semantic Segmentation: Fully Convolutional Networks](../raw/images/03-convolutional-neural-networks/slide-63.jpg)

*Lecture 3, slide 63 — downsampling then upsampling, from a photograph to a class for every pixel.*

**Continuous control.** Lecture 3's self-driving car, built at MIT, steers from camera images and a
coarse street map, with no HD map (≈3:10–3:56). Each input goes through its own convolutional layers,
the features are concatenated, and the network outputs a probability distribution over control
commands, because the right action can be multimodal, such as turning left or right (slides 64–65,
≈52:32–54:49, Amini+ *ICRA* 2019). The model is trained end-to-end without human labels (slide 65).

![Slide 65: End-to-End Framework for Autonomous Navigation](../raw/images/03-convolutional-neural-networks/slide-65.jpg)

*Lecture 3, slide 65 — convolutional branches for cameras and map, concatenated, giving a mixture over steering commands.*

## Where this comes up

- [Lecture 3 — Convolutional Neural Networks](03-convolutional-neural-networks.md), sections 1–3 and
  17–21.
- [Lecture 1 — Introduction to Deep Learning](01-introduction.md) previews lab 2, on computer vision and
  facial detection.
