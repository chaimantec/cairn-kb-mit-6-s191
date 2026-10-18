# Lecture 6 — Language Models and New Frontiers

**MIT 6.S191, 2026 edition. Lecturer: Ava Amini. Delivered 7 January 2026.**
[Video](https://www.youtube.com/watch?v=ev7cLSd-ySE) ·
[Slides (PDF)](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L6.pdf) ·
[Slide-by-slide transcription](../raw/slides/06-language-models-new-frontiers.md) ·
[Transcript](../raw/transcripts/06-language-models-new-frontiers.md) ·
[Verbatim captions](../raw/transcripts/original/06-language-models-new-frontiers.md)

The catalog lists this lecture as "Language Models and New Frontiers"; its title slide reads "Deep
Learning Limitations and New Frontiers", and the class schedule calls it "New Frontiers" (slide 3). It
is the last lecture given by the course's two instructors before the guest lectures, and it looks at
deep learning from two sides (≈0:12). The first half is about **limitations**: the universal
approximation theorem and what it does not promise, networks that fit randomly labelled data perfectly,
what a network does away from its training data, failures caused by the data, uncertainty, adversarial
attacks and algorithmic bias. The second half is about two **new frontiers** that push past some of
those limits: **diffusion models**, which generate data by removing noise step by step, and **large
language models**, trained to predict the next token, whose abilities emerge with scale.

Timestamps such as (≈24:10) point into the [transcript](../raw/transcripts/06-language-models-new-frontiers.md);
"slide N" is page N of the PDF (the deck prints no slide numbers). See also the topic pages
[limitations of deep learning](limitations-of-deep-learning.md), [diffusion models](diffusion-models.md)
and [large language models](large-language-models.md).

## 1. Logistics and the guest lectures (0:12–6:21)

The lecture opens on logistics (slides 2–8). Course T-shirts are handed out the next day, after the
guest lectures (slide 2, ≈0:12–0:57). The class is on day three of five: the next two days are guest
lectures, and Friday ends with the project proposal competition (slide 3, ≈0:57). Each of the three
software labs has a top prize, judged by the rubric at the end of each lab and submitted through a
Dropbox file request linked from the syllabus (slide 4, ≈1:42).

MIT students taking the course for credit have two options (≈1:42–4:47). The first is the project
proposal competition, "kind of like a shark tank style pitch" of a novel deep learning research idea or
application. Amini says the presentation time will be "between three to five minutes", depending on the
number of groups (≈2:27); slide 5 prints "5 minutes (strict)". Groups must be submitted by midnight the
next night, slides by 1 p.m. on Friday, and a winner has the chance to expand the idea into a TEDx talk
(≈2:27–3:14; slide 5). The second option is a one-page written review of a deep learning paper, graded
on clarity and on capturing the technical contribution, also due Friday (slide 6, ≈3:14–4:01).

Slide 7 lists the guest lectures (≈4:01–5:33): Chris Bishop (Microsoft), on AI at the intersection with
the natural sciences (his lecture is [lecture 8](08-ai-for-science.md) in this knowledge base); Mathias Lechner (Liquid AI), on what it takes to train language models today —
Amini mentions the Liquid language models students have been using in Software Lab 3 (his lecture is [lecture 9](09-massively-parallel-training.md) in this knowledge base); Douglas Blank (Comet ML), on deploying AI in the
wild (his lecture is [lecture 7](07-three-laws-of-ai.md) in this knowledge base); and Matt Johnson (Google DeepMind), one of the co-creators of JAX. Slide 8 thanks the course staff
(≈5:33–6:21).

## 2. So far: from data to decision, and back (6:21–8:40)

The course so far has covered deep learning from what it is up to reinforcement learning, as a toolkit
for problems from autonomous vehicles and robotics to biology, medicine, language, finance and
security (slides 9–10, ≈6:21–7:54). Amini frames it as two paradigms (slide 11, ≈7:54). One goes from
**data to decision** — signals, images and sensors in; prediction, detection and action out — in
supervised learning and in reinforcement learning. The other goes back **from desired outcomes to the
data**: generative models, which "help us solve what we call these inverse problems" by modeling the
data distribution itself. Both rest on neural networks learning very complex functions, either from
data to output or over a distribution of data (≈8:40).

## 3. The universal approximation theorem (8:40–10:58)

To understand those functions, Amini goes back to a theorem from 1989, the **universal approximation
theorem** (slide 12, credited "Hornik+ *Neural Networks* 1989."). As printed: "A feedforward network
with a single layer is sufficient to approximate, to an arbitrary precision, any continuous function."
Aloud, it is "a feedforward neural network with a single hidden layer" (≈8:40–9:26). The point Amini
draws out is that the theorem does not even ask for depth: if a problem can be reduced to a mapping from
inputs to outputs, one fully connected layer is enough to approximate it to some precision (≈9:26). (The
unlabelled network drawn on slide 12 has five columns of nodes, more than the single layer of the
statement.)

That sounds very powerful, but slide 13 prints two caveats (≈10:12):

- "The number of hidden units may be infeasibly large." The theorem gives no guarantee or limit on the
  size of the layer.
- "The resulting model may not generalize." This one is "perhaps even more important": the theorem
  places no guarantee on the model's ability to generalize. Recalling lecture 1's discussion of
  overfitting, low training error can come with poor performance on the test set (≈10:12–10:58; see
  [overfitting and regularization](regularization.md)).

These are the two considerations that dominate deep learning today: how large models must be to have
general-purpose capabilities, and whether they can generalize to the new scenarios we care about
(≈10:58).

## 4. AI "hype" in historical perspective (10:58–12:33)

Amini likes the theorem as history because it puts deep learning in context: "like any technology, AI,
deep learning is just that. It's a technology", and it goes through waves of growth and waves of
criticism (≈10:58–11:45). Slide 14 draws AI's popularity over time as one curve: "Birth" in 1956, a peak
of "Inflated Hype" in 1974, "AI winter I" in 1980, "New Hopes" in 1987, "AI winter II" in 1993, then
"Explosive Growth" to the highest point on the chart. We are now in that phase of exponential growth,
with very large, general-purpose AI systems; it was not always so, both because of hardware and because
at times the scientific community heavily doubted these models would lead to real breakthroughs
(≈11:45–12:33).

![Slide 14: AI popularity over time](../raw/images/06-language-models-new-frontiers/slide-14.jpg)

*Slide 14 — AI's popularity over time: two peaks of hype, two AI winters, and the current explosive growth.*

## 5. Rethinking generalization: fitting random labels (12:33–15:40)

The first concrete limitation connects back to the theorem: what generalization means, and what it
means to fit the training data too closely (≈12:33). The paper Amini says contextualizes this "better
than anything else" is "Understanding Deep Neural Networks Requires Rethinking Generalization" (slide 16,
credited "Zhang+ *ICLR* 2017.").

The experiment (slides 16–19, ≈13:20–14:06): take images from **ImageNet**, each with a label describing
what is in it. For every image — "not class, but image" — flip a K-sided die, where K is the number of
classes in the dataset, and reassign the image's label according to the outcome. The mapping from images
to labels becomes arbitrary: two images of the same class can now carry completely different labels,
neither of them the true one. Slides 16–19 show it on four photographs labelled dog, banana, dog and
tree, which after the dice become banana, dog, tree and dog.

![Slide 18: randomizing labels with a die](../raw/images/06-language-models-new-frontiers/slide-18.jpg)

*Slide 18 — each image's label is re-drawn by a die roll, so the same class can end up under different, wrong labels.*

They then trained a deep network on the data at increasing degrees of randomization, from the original
labels to completely random ones (≈14:06). On a held-out test set, as you might expect, accuracy gets
worse and worse as randomization increases. The startling result is on the **training** set: no matter
how much the labels were randomized, a network trained long enough still fit the training examples
(≈14:53). Slide 22 shows it: training accuracy (blue) stays at 100% at every degree of randomization,
while test accuracy (green) falls steadily from "original labels" to "completely random"; a red dashed
line across the tops of the blue bars reads "Modern deep networks can perfectly fit to random data"
(slides 20–22).

![Slide 22: training accuracy stays at 100% while test accuracy falls](../raw/images/06-language-models-new-frontiers/slide-22.jpg)

*Slide 22 — training accuracy (blue) stays at 100% however random the labels; test accuracy (green) falls.*

This is the universal approximation principle in practice, Amini says: granted, this is a deep model and
the theorem is about a single layer, but it shows the capacity of these models to fit training data to
some precision, and that fitting does not bring generalization to the test set with it (≈15:40).

## 6. Neural networks as function approximators (15:40–17:58)

So neural networks are "excellent function approximators" (slide 23). Given a set of data points, a
network can be trained into a very good approximator of the function behind them (slides 23–24,
≈15:40–16:26). In the theory of deep learning, Amini says, we can think of these networks as learning a
maximum-likelihood, most likely estimate of the data within this distribution, so that given a new data
point inside it — the purple point of slides 25–26 — the model produces a reasonable prediction
(≈16:26).

![Slide 26: a prediction inside the range of the training data](../raw/images/06-language-models-new-frontiers/slide-26.jpg)

*Slide 26 — a query inside the range of the data (purple) lands on the fitted curve near the training points.*

Beyond that regime there are no solid theoretical guarantees on how these models behave **out of
distribution** (≈16:26–17:11). Slide 27 extends the fitted curve past the data on both sides, where it
swings to a tall peak on the left and rises steadily on the right with no data to support either, and
slide 28 adds the qualification "…when they have training data" and the question "How do we know when
our network doesn't know?" Amini puts the questions this raises: how do we know when these models do or
do not know, and how do we understand the limits on their capacity to generalize to harder and harder
out-of-distribution scenarios (≈17:11)?

![Slide 28: the fitted curve away from the data](../raw/images/06-language-models-new-frontiers/slide-28.jpg)

*Slide 28 — away from the training data (the purple arrows) the curve does whatever it likes: "How do we know when our network doesn't know?"*

## 7. Deep learning is not alchemy (17:58–19:29)

There is a myth, Amini says, that a technology like deep learning could be a magic, be-all end-all
solution, compared to the alchemist trying to turn heavy metals into gold: turn the crank and the result
comes out (≈17:58). Slide 29 answers "Deep Learning = Alchemy?" with a red "NO!": beside a painting of an
alchemist, a cartoon machine that takes "Training data" and a "Random network architecture", is cranked
by a "Learning algorithm" and pays out gold coins of "Excellent results", is crossed out with a red X
(credited "U. Muller, 6.S191 2018.").

![Slide 29: Deep Learning = Alchemy? NO!](../raw/images/06-language-models-new-frontiers/slide-29.jpg)

*Slide 29 — the data-in, results-out machine, crossed out.*

The equal and opposite maxim is "garbage in, garbage out" (≈17:58–18:44). Train on a very limited set
of data, on a problem the approach does not suit, or with a model mismatched to the complexity of the
task, and the model may learn the training data but often will not perform on test scenarios. Amini's
advice for final projects and beyond: think about the task at hand and its inputs and outputs, the
quality of data you can curate or generate for it, and whether deep learning makes sense as the approach
in the first place (≈18:44).

## 8. Failure mode I: what the data over-represent (19:29–21:03)

Garbage in, garbage out shows up as the limits of the training distribution, not necessarily as garbage
(≈19:29). Slide 30 trains a CNN to colorize black-and-white images, and puts a grayscale photo of a dog
through it. Asked what is odd about the result, a student points to green on the ear, and Amini adds that
the tongue "is also kind of reddish" (≈20:17). Why? Probably because the dataset holds many images of
dogs with their tongues out, so that is the over-represented example, and the model reproduces it
(≈20:17; slide 31's collages of dogs with their tongues out, both credited "P. Isola 6.869.").

![Slide 30: colorizing a black-and-white dog](../raw/images/06-language-models-new-frontiers/slide-30.jpg)

*Slide 30 — a CNN trained to colorize black-and-white images tints this dog's left ear green and the patch below its nose pink.*

![Slide 31: the training data are full of dogs with their tongues out](../raw/images/06-language-models-new-frontiers/slide-31.jpg)

*Slide 31 — "What Happens During Training…": the dog photos the network learns from mostly have their tongues out.*

## 9. Failure mode II: out of distribution on the road, and uncertainty (21:03–23:24)

The same problem has much more serious consequences in the real world (≈21:03). Slide 32 reproduces ABC
News coverage of a fatal crash of a Tesla on autopilot near Mountain View, California, in March 2018.
Amini's account: the driver, who did not survive, had reported multiple times over several weeks that
the car in autonomous mode would swivel towards the construction barrier where the accident later
happened (the broadcast caption on the slide: "7-10 TIMES THE CAR WOULD SWIVEL TOWARD THAT SAME
EXACT BARRIER"). Investigations found that in past street-view images of the location the barrier was not
present; it had been erected more recently, so it was an out-of-distribution outlier that had not been in
the training set (≈21:03–21:49). Slide 32 sets a photograph of the spot labelled "GOOGLE STREET VIEW" beside
one labelled "THURSDAY, MARCH 22, 2018".

This leads to **uncertainty** in AI models: how do we know when a model is confident in its predictions,
and when it lacks information and needs human intervention (≈21:49–22:37)? It is critical in
safety-critical applications — autonomous vehicles, biology, medicine and health care, security, public
surveillance and facial detection — and imbalance or noise in the data can produce regions of greater
uncertainty in the network's outputs (slide 33, ≈22:37). Slide 33 groups the cases as "Safety-critical
applications" and "Sparse and/or noisy datasets" (imbalance, data noise). Lab 2 dealt with these issues,
which have both algorithmic and data-side countermeasures (≈23:24).

## 10. Failure mode III: adversarial attacks (23:24–26:31)

Another famous failure mode is the **adversarial attack** or **jailbreak**: take an example, or create a
synthetic one, that fools the network (≈23:24). It started with attacks on vision models, CNNs in
particular. Take a natural image, add a noise-based perturbation imperceptible to the human eye, and feed
the result to the model: it now misclassifies it, with very high probability (≈24:11). Slide 34 (credited
"Despois 'Adversarial examples' 2017.") shows an "Original image" classified "Temple (97%)", plus
"Perturbations", equals an "Adversarial example" that looks the same and is classified "Ostrich (98%)".

![Slide 34: temple plus perturbation equals ostrich](../raw/images/06-language-models-new-frontiers/slide-34.jpg)

*Slide 34 — an imperceptible perturbation turns "Temple (97%)" into "Ostrich (98%)".*

How does the perturbation trip the network so severely? Recall from lecture 1 how networks are trained
(slide 36, ≈24:58): gradient descent changes the weights $W$ to decrease a loss $J$, with the image $x$ and
its true label $y$ held fixed (slides 37–38):

$$W \leftarrow W - \eta \frac{\partial J(W, x, y)}{\partial W}$$

where $\eta$ is the learning rate — "How does a small change in weights decrease our loss". An
adversarial image asks the inverse question (slide 39, credited "Goodfellow+ *NIPS* 2014.", ≈25:45): with
the weights and the true label fixed, how can we modify the **input** to produce a large **increase** in
the loss? So the update runs on $x$, and with a plus sign:

$$x \leftarrow x + \eta \frac{\partial J(W, x, y)}{\partial x}$$

— "How does a small change in the input increase our loss" (slides 39–41). Slide 39's heading is
"Adversarial Image: Modify image to increase error". (Slide 41's callout reads "Fix your weights
$\boldsymbol{\theta}$, and true label $\boldsymbol{y}$", although its formula writes the weights $W$.)

It goes beyond 2D images: a group at MIT CSAIL synthesized **3D objects** in the real world, constructed
adversarially so that photographs of them fool a CNN classifier (≈25:45–26:31). Slide 42, "Synthesizing
Robust Adversarial Examples" (credited "Athalye+ *ICML* 2018."), shows 24 photographs of a 3D-printed
turtle from different viewpoints, bordered by how each was classified: only one as "turtle", most as
"rifle", the rest as "other". A very simple idea — perturb the input instead of updating the weights —
yields measurable differences in the outputs (≈26:31).

![Slide 42: a 3D-printed adversarial turtle classified as a rifle](../raw/images/06-language-models-new-frontiers/slide-42.jpg)

*Slide 42 — a 3D-printed turtle photographed from 24 viewpoints: red borders "classified as rifle", green "turtle", black "other".*

## 11. Algorithmic bias, and the list of limitations (26:31–28:04)

A very real and severe limitation for safety, fairness and ethics is **algorithmic bias** (slide 43, a
wall of news headlines about racial and gender bias in AI systems; ≈26:31–27:18), which the course's labs
explore hands-on. Slide 44 lists the limitations of neural networks: very data hungry (often millions of
examples); computationally intensive to train and deploy; easily fooled by adversarial examples; subject
to algorithmic bias; poor at representing uncertainty ("how do you know what the model knows?");
uninterpretable black boxes, difficult to trust; often requiring expert knowledge to design and fine-tune
architectures; difficult to encode structure and prior knowledge during learning; and poor at
extrapolation, struggling "to go beyond the data". The list is "not comprehensive at all" (≈27:18), and
Amini presents limitations as opportunities: places where new technologies and solutions can counteract
them, whether for algorithmic bias, interpretability, uncertainty or the others. Slides 45–46 highlight
bias, uncertainty and black boxes (marked "6.S191 Lab"), then encoding structure and extrapolation.

## 12. New frontiers: generalization through scale (28:04–28:50)

The rest of the lecture takes a couple of these limitations and looks at advances that overcome them,
especially in generalization: going beyond the training distribution to models with very general-purpose
capabilities (≈28:04). Networks depend heavily on data, but scaling the data and scaling the models
themselves has led to **emerging capabilities** that improve generalization very significantly, as with
today's language models (≈28:04–28:50). The two frontiers are diffusion models and large language
models.

## 13. The landscape of generative modeling (28:50–31:08)

The first frontier, teased the day before, is generative modeling and in particular **diffusion models**
(slide 47, "New Frontiers I: Generative AI & Diffusion Models"; ≈28:50). Lecture 4 laid the foundations:
autoencoding, compression into latent variables, and the beginnings of sample generation with GANs (slide
48's "Lecture 4: VAEs and GANs" panel; see [generative modeling](generative-modeling.md)). Those approaches
have notable limitations (slide 48, ≈29:37): they can collapse to generating average instances (slide 48
prints "Mode collapse"; aloud, "what we call model collapse"), so it is hard to generate instances that
stretch the data distribution ("Generating OOD"), and GANs especially are tricky to train, with two
networks set against each other ("Hard to train"). Those translate into challenges of training stability,
training efficiency, and the quality and novelty of the samples (slide 48's "Challenges", ≈30:22).

Diffusion modeling has become one of the dominant paradigms in generative modeling, and it is very often
the backbone of the text-to-image systems where a text prompt conditions the generated image (slide 49,
≈30:22–31:08).

![Slide 49: the landscape of generative modeling](../raw/images/06-language-models-new-frontiers/slide-49.jpg)

*Slide 49 — lecture 4's VAEs and GANs, diffusion models (a photograph to noise and back), and text-to-image ("Two cats doing research").*

## 14. Diffusion: generating iteratively (31:08–32:40)

VAEs and GANs generate a sample **in one shot**, directly from noise or a low-dimensional set of latent
variables back to the data space $x$ (slide 50, ≈31:08). Diffusion is fundamentally different: rather than
generating in a single shot, decompose the problem into iterative generations that make the task easier
(≈31:08–31:53). Diffusion models generate new samples iteratively by learning to remove noise, step by
step, refining the generation as they go. Slide 50 draws the contrast: on the left, a noisy latent vector
$z$ goes through one network to a generated sample $x$; on the right, a noisy sample $x_T$ passes through
a chain of denoising blocks to a less noisy $x_i$, an even less noisy $x_j$ and finally the generated
sample $x_0$.

![Slide 50: one-shot generation versus iterative denoising](../raw/images/06-language-models-new-frontiers/slide-50.jpg)

*Slide 50 — VAEs and GANs map a latent vector to a sample in one step; diffusion refines a noisy sample through repeated denoising.*

So a diffusion model has two processes (slide 51, credited "Sohl-Dickstein+ *ICML* 2015; Ho+ *NeurIPS*
2020.", ≈31:53–32:40). **Forward noising** (data to noise) starts with training data, say images, and adds
noise iteratively, step by step, slowly wiping out the details until the instance is pure random noise.
These iterates constitute the samples used to train the model: one image, noised step by step. **Reverse
denoising** (noise to data) is what the neural network learns. Amini calls the forward process "the
deterministic forward noising process" (≈31:53); only the reverse process is learned.

![Slide 51: forward noising and reverse denoising](../raw/images/06-language-models-new-frontiers/slide-51.jpg)

*Slide 51 — forward noising turns an image into noise; the network learns the reverse, noise back to data.*

## 15. Forward noising (32:40–34:12)

Step by step (slides 52–53, ≈32:40–33:26): **Step 1**, given an image, sample a random noise pattern.
**Step 2**, progressively add more and more of that noise to the image. Slide 53 shows five time steps,
$T = 0$ to $T = 4$, each differing from the last by a step-wise addition of random noise: 100% image and
0% noise at $T = 0$, then 75/25, 50/50 and 25/75, to 0% image and 100% noise at $T = 4$.

![Slide 53: forward noising from T = 0 to T = 4](../raw/images/06-language-models-new-frontiers/slide-53.jpg)

*Slide 53 — the clean image is noised in four steps until it is all noise.*

## 16. Reverse denoising: what to train the network on (33:26–36:28)

The question is how to define the reverse process (slide 54, credited "Ho+ *NeurIPS* 2020.",
≈33:26–34:12). Goal: "Given image at **T**, can we **learn** to estimate image at **T-1**?" — the image one
step less noisy. Training the network means teaching it this denoising estimation, and slide 54 asks "How
can we train this network?", with a network block that takes the image at $T = 3$ to the image at $T = 2$.

![Slide 54: learn to estimate the image at T-1 from the image at T](../raw/images/06-language-models-new-frontiers/slide-54.jpg)

*Slide 54 — the denoising network's task: from the image at step T, estimate the image at step T-1.*

Amini asks the room for a loss (≈34:12–35:43). A student suggests removing one colour or one shade;
Amini points out that the noise is random Gaussian noise, sampled from a Gaussian distribution and
applied, but that the two images side by side differ by exactly that addition. Another student proposes
calculating how far one noised image is from another, and Amini restates it: look at the difference in
pixel values between the images at $T = 2$ and $T = 3$ — "That's exactly right" (≈34:58–35:43). The model
can be trained with "a mean squared error style loss" comparing the image at $T = 3$ with the image at
$T = 2$, where the difference is in the pixel values; since the pairs differ by added random noise, the
model learns to remove the noise from these stepwise pairs. It turns out that **predicting the
difference, which is the noise**, is a very effective way to train diffusion models (≈35:43). The deck
prints no loss formula; for mean squared error itself see [loss functions](loss-functions.md).

## 17. Sampling brand new generations (36:28–38:01)

With a forward process and a loss for the reverse process, the recipe is complete (≈36:28). To generate
at inference time, start from a pattern of noise, use the trained network to predict the residual
difference, and use it to define a new instance at the next time step with less noise; repeat, time step
by time step, and the image "come[s] to life" until at the last step it is back in image space as a
newly generated sample (slides 55–61, ≈36:28–37:14). Slide 61 shows the whole chain, from pure noise at T
through T-1, T-2, T-3 and T-4 to a clean photograph of a dog at "T-5 (end)" (slide 60 labels the same
final image "T0 (end)").

![Slide 61: sampling a new image by repeated denoising](../raw/images/06-language-models-new-frontiers/slide-61.jpg)

*Slide 61 — from pure noise to a generated dog, one denoising step at a time.*

Putting it together (≈37:14): in **training**, the network learns to predict the additions of noise, which
defines the reverse denoising process; at **inference**, it starts from noise and denoises iteratively to
construct new samples. Starting from random noise while decomposing the objective into iterative steps
simplifies the task the model has to learn, yet keeps a very high information capacity at the start, so
diffusion models can produce very diverse, high-quality samples: a different instance of starting noise
can yield a strikingly different image (≈37:14–38:01).

## 18. A question: is the noise really noise? (38:01–39:34)

A student asks whether this suggests that what is being called noise is not noise at all — that there is
some order in the noise that turns one image into the other (≈38:01–38:47). Amini's answer: the
difference is subtle. The model gets its signal from the comparison of step T with step T minus 1, which
gives enough supervisory signal to bring semantic structure to the problem even though the noise applied
is still a noise function. The noise itself is not structured meaningfully in any way; it is the
difference between two time steps created by the forward process that lends signal and semantic structure
(≈38:47–39:34).

## 19. Text-to-image generation (39:34–42:36)

Another student asks how text-to-image generation works: is a description of the image being captured in
the latent space through the noise (≈39:34)? The examples so far, Amini explains, are **unconditional
generation**: images generated with no text injected. To condition on a prompt, the signal from the text
guides the generation (≈39:34–41:06). In practice the text is tokenized into a numerical representation,
and a language-based encoder or embedding model produces a vector representing it; signal from that vector
is mixed with signal from the corresponding image, so the model learns patterns between the text and image
representations. Text-conditioned diffusion models can be trained some percent of the time with the text
prompts and some percent of the time on images alone, which pushes the model to produce high-quality
generations that follow the semantic content of the prompt while still training on images by themselves,
so the generations stay high-quality (≈41:06–41:51). Asked whether the embedding is trained separately:
often in practice it is, and used as a prior, though the embedding model can also be refined on the image
training so signal flows back to it (≈41:51).

Slide 64 shows the prompt "A photo of an astronaut riding a horse." going into a network and the
generated image (credited "Ramesh+ *arXiv* 2022"); slide 65 shows three more, credited "OpenAI. Ramesh+
*arXiv* 2022": "a painting of a fox sitting in a field at sunrise in the style of Claude Monet", "an ibis in
the wild, painted in the style of John Audubon", and "close-up of a snow leopard in the snow hunting, rack
focus, nature photography". Neither is discussed aloud.

![Slide 64: a photo of an astronaut riding a horse](../raw/images/06-language-models-new-frontiers/slide-64.jpg)

*Slide 64 — the prompt "A photo of an astronaut riding a horse." and the image generated from it.*

![Slide 65: three prompts and their generated images](../raw/images/06-language-models-new-frontiers/slide-65.jpg)

*Slide 65 — three prompts and their images: a Monet-style fox, an Audubon-style ibis and a photograph-style snow leopard.*

## 20. Beyond images: molecular design (42:36–43:21)

Diffusion goes beyond images and text to other modalities (≈41:51–42:36). In recent years it has shown
strong capabilities in **molecular design**: the input can be the 3D coordinates of the atoms in a molecule
or a protein, and diffusion runs over them in continuous space, because like the pixels of an image these
are continuous values (≈42:36). Slide 66 shows "Chemistry: Generating Molecules in 3D", a sequence from
"Noise" to "Molecule" (credited "Hoogeboom+ *ICML* 2022, Jing+ *NeurIPS* 2022, and more…", with a "6.S191
Guest Lecture!" star), and "Biology: Generating Novel Proteins", four generated protein structures
(credited "Anand+ *arXiv* 2022, Watson+ *Nature* 2023, Ingraham+ *Nature* 2023, Wu+ *Nature Comm.* 2024,
Alamdari+ *bioRxiv* 2024, and more …"). These capabilities are being translated into many real-world
applications (≈43:21).

![Slide 66: diffusion for molecules and proteins](../raw/images/06-language-models-new-frontiers/slide-66.jpg)

*Slide 66 — diffusion beyond images: a 3D molecule emerging from noise, and generated protein structures.*

## 21. What are large language models? (43:21–44:52)

The final part of the lecture is a foundation in **large language models** (slide 67, "New Frontiers II:
Large Language Models"; ≈43:21): the core principles of what they are and how they operate, and how that
has produced the capabilities seen in practice. GPT, Gemini, Copilot and the rest have revolutionized our
world (slide 68, ≈43:21–44:07). Fundamentally, LLMs are a special class of deep learning models: for
simplicity, very large neural networks trained on very large sets of text, with different tasks or
objectives that train them in general-purpose ways (≈44:07). Slide 69 nests them inside the course's
opening definitions: "Artificial Intelligence" ("Any technique that enables computers to mimic human
behavior") contains "Deep Learning" ("Extract patterns from data using neural networks"), which contains
"Large Language Models" ("Very, very large neural networks trained on very, very large sets of text").
See [what is deep learning?](what-is-deep-learning.md)

![Slide 69: LLMs inside deep learning inside AI](../raw/images/06-language-models-new-frontiers/slide-69.jpg)

*Slide 69 — large language models as a class of deep learning, itself a part of artificial intelligence.*

## 22. How LLMs like GPT are trained (44:52–46:22)

The pipeline behind models like GPT (slide 70, ≈44:07–45:37): a general-purpose, really unannotated
dataset, scraped from the web — Common Crawl, Wikipedia, WebText, code and other sources of text. As in the
sequence modeling lecture, the first step is to split the text into chunks, called **tokens**; that
chunking is what "tokenization" refers to (≈44:52; see [sequence modeling](sequence-modeling.md)). The
tokens have numerical IDs, which are the input to training (≈45:37). For scale: GPT-3 was reported to have
175 billion parameters (slide 70: "175B parameters (GPT3)"); GPT-4, 5 and later models have often scaled
beyond that, while small language models such as Liquid AI's are scaled back by orders of magnitude and
still show strong capabilities (≈45:37).

The dominant task in modern language modeling is **next-token prediction** (≈46:22). Slide 70 states the
task and objective: "Given a sequence of tokens, predict the next token. Update model parameters given how
good next-token prediction is." It is very similar to what the sequence modeling lecture set out (see
[lecture 2](02-rnns-transformers-attention.md)).

## 23. Next-token prediction and the cross-entropy loss (46:22–49:25)

What is the loss behind that objective (slide 71, ≈46:22–47:08)? Take the raw text "MIT deep learning is
so awesome" and break it into tokens — shown as words for simplicity — convert them to IDs and embed them
into a numerical representation, which is the input to the LLM (≈47:08). Given a series of tokens, the
model predicts the next one, and what it outputs is a **probability** for every possible token in the
vocabulary (≈47:08–47:54). Because the vocabulary is a discrete set of tokens, this is a **classification**
problem, just like lecture 1's: compare the true next token with the predicted probabilities and compute a
**cross-entropy loss** (≈47:54; see [loss functions](loss-functions.md)). In slide 71, the model reading
"MIT deep learning is so" predicts each next token, and for the position after "so" the bar chart of token
probabilities and the true token both feed the "Cross entropy loss" box.

![Slide 71: next-token prediction and the cross-entropy loss](../raw/images/06-language-models-new-frontiers/slide-71.jpg)

*Slide 71 — raw text is tokenized and embedded; the LLM predicts a probability for each next token, scored against the true token by a cross-entropy loss.*

Why this is so powerful (≈48:40): the data are their own signal. No external labels are needed beyond the
structure of the text itself, and the same classification cross-entropy loss, comparing the predicted
probabilities over the vocabulary with the true next token, learns structure in very complex text data —
"so beautiful in its simplicity" (≈48:40–49:25).

## 24. From a base model to a chatbot, and what LLMs can do (49:25–50:57)

A base language model does next-token prediction; deployed models have been tuned and refined after that to
follow structured prompts and act as chatbots and interactive agents, with a clear division between the
user's prompt and the LLM's generated response (slide 72, ≈49:25–50:10). Slide 72's deployment example:
"I'm giving a talk on AI at MIT. Can you outline it?" goes in, and an outline comes out — "Introduction",
"What is AI?", "How does AI work?", "How can we use AI?".

![Slide 72: training, then deployment on a prompt](../raw/images/06-language-models-new-frontiers/slide-72.jpg)

*Slide 72 — the training pipeline of slide 70, and a deployed model answering a prompt with a talk outline.*

What makes it powerful is the combination of a very simple objective — next-token prediction with a
cross-entropy loss — with the scale of the available data, the models and the compute, which together let
the model learn patterns in very large datasets (≈50:10). Today's language models are extremely capable at
assisting with writing and planning and at knowledge retrieval, and have shown mastery over natural
language (slide 73: "Knowledge Retrieval", "Writing Co-Pilot", "Planning Co-Pilot"; "LLMs like GPT have
shown mastery over natural language."; ≈50:10).

## 25. Limitations of LLMs (50:57–52:30)

LLMs still face the same principles the lecture started with (slide 74, ≈50:10–51:43):

- **Robustness and confidence.** How do we know a generation is confident? Being very likely or very
  probable is not the same as being high-confidence, and quantifying the uncertainty of LLMs is still an
  open research direction (≈50:57). Slide 74 heads this column "Robustness: How confident?" over a
  deliberately garbled prompt, "Cn @uN66rN you translate ths from Spanish to English?" (credited "Wang+
  *arXiv* 2023.").
- **Hallucination.** Work with these models long enough and you will see generated text that seems
  feasible, consistent and logical, but that someone who knows the field can tell is "not really like all
  the way there" (≈50:57). Slide 74: "'Hallucinations': Confidently wrong". Amini adds that very recent
  work has shown that language models that are well calibrated will necessarily produce hallucinations
  (≈51:43).
- **Jailbreaks.** As with adversarial attacks, there are still ways to jailbreak these models and probe
  them to expose adversarial failure modes (≈51:43; slide 74, "Guardrails and Jailbreaks", around
  "Model-level guardrails").
- **Planning and logic.** Long-term planning and logic remain limited; recent advances in reasoning have
  enabled tremendous new capabilities, but there is still a long way to go (≈51:43; slide 74, "Logic and
  Numerics", and its closing line, "Key challenges motivated by the high-level thinking process:
  robustness + confidence; long-term planning; logic and discovery").

## 26. Emergent abilities with scale (52:30–54:02)

What has struck a chord over the past couple of years is that modern language models can **generalize**,
performing tasks in domains that stretch their capabilities, and much of this is due to **emergent
abilities** (≈52:30). Work that systematically evaluated these models as a function of the amount of
training data and of model capacity found that past a particular threshold of model scale there are new
inflection points, step changes in capability, that seem to come only with scaling the data, the compute
and the parameters (≈52:30–53:15). Slide 75 (credited "Wei+ TMLR 2022.") defines it: "An ability is
**emergent** if it is not present in smaller models but is present in larger models." Its three charts —
"Structuring Language", "Understanding Phonetics" and "Performing Arithmetic" — plot accuracy or BLEU
against model scale on a log axis: each curve stays flat near its dashed baseline for the smaller models
and rises sharply only at the largest scales.

![Slide 75: emergent abilities with scale](../raw/images/06-language-models-new-frontiers/slide-75.jpg)

*Slide 75 — three tasks on which performance stays at the baseline as models grow, then jumps at the largest scales.*

The idea is a hierarchy of abilities, unlocked as models scale to larger and larger sizes (≈53:15). Slide
76 (credited "Google AI blog.") draws it as a tree whose branches — question answering, arithmetic and
language understanding — grow with model size, shown at "8 billion parameters".

![Slide 76: emergent abilities as a growing tree](../raw/images/06-language-models-new-frontiers/slide-76.jpg)

*Slide 76 — abilities as branches of a tree that grows with model size, here at 8 billion parameters.*

## 27. Closing: foundation models and human capabilities (54:02–end)

Emergence, and language models effectively modeling our world through natural language, inspire the idea
Amini leaves the class with: how do we think about reasoning, and about augmenting and accelerating our own
capabilities with AI (≈53:15–54:02)? For someone who works closely with these models, the goal is that they
stay a technology that humans use to accelerate their own creative process and capabilities in ways the
models cannot, while the models' capabilities, still far out of reach for humans, augment our own
limitations (≈54:02–54:49). Slide 77, "Foundation Models Spawn a Powerful Idea", puts it as "Towards a
central reasoning system for general-purpose AI" and closes on "Relationships and connections between
artificial and human intelligence".

The lecture ends with encouragement to get hands-on — not everyone has the chance to sit in this class —
and with **Lab 3**, on fine-tuning language models (slide 78, "Lab 3: Fine-Tune an LLM, You Must!"), and
the guest lectures and T-shirts of the next day (slide 79, ≈54:49–55:36).

## Spoken versus printed

- **Pitch length**: aloud, "between three to five minutes" depending on the number of groups (≈2:27);
  slide 5 prints "5 minutes (strict)".
- **The universal approximation theorem**: aloud, a network "with a single hidden layer" (≈8:40); slide 12
  prints "a single layer", and its unlabelled diagram has five columns of nodes.
- **Mode collapse**: aloud, "what we call model collapse" (≈29:37); slide 48 prints "Mode collapse".
- **The weights' symbol**: slide 41's callout says "Fix your weights $\boldsymbol{\theta}$", while every
  formula on slides 36–41 writes the weights as $W$.
- **Time-step labels**: slide 53 numbers the forward process from $T = 0$ (the clean image) to $T = 4$ (pure
  noise); the sampling slides count down from T (noise) and label the final image "T0 (end)" on slide 60
  and "T-5 (end)" on slide 61.
- **Not discussed aloud**: slide 12's network drawing, slide 44's full list beyond what section 11 quotes,
  the text-to-image examples of slides 64–65, slide 68's ChatGPT screenshot, slide 73's three capabilities,
  and slide 76's "8 billion parameters".
