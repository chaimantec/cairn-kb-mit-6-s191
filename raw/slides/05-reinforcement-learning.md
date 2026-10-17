---
title: Lecture 5 — Reinforcement Learning (slide deck)
lecture: 5
slides: 58
source_pdf: https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L5.pdf
note: Slide N = PDF page N (N = 1..58). The deck prints no slide numbers; the "1/7/26" in each footer is the lecture date (7 January 2026).
---

# Lecture 5 — Reinforcement Learning: slide-by-slide

Text and figures of all 58 slides of
[`6S191_MIT_DeepLearning_L5.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L5.pdf)
(MIT 6.S191 Introduction to Deep Learning, 2026 edition; lecturer Alexander Amini), transcribed from the
deck. The catalog lists this lecture as "Reinforcement Learning"; the title slide reads "Deep
Reinforcement Learning". Cite these as "slide N", where N is the PDF page number. Diagrams,
photographs, plots and equations are described in prose or reproduced, since the KB is read as text.

Many slides are **build steps**: the same slide re-shown with one more element revealed. They are
transcribed individually, so that a citation to any one of them resolves, with a note of what each
adds to the one before.

## Numbering: slide numbers vs PDF pages

The PDF is a flattened export: every page is a single 1280×720 image with no text layer, and no
page prints a slide number. Headings therefore use the PDF page number, and a reader who opens page
N of the PDF sees slide N. The standard footer on content slides (MIT logo, "MIT Introduction to
Deep Learning", introtodeeplearning.com, @MITDeepLearning, "1/7/26") is not repeated below; citations
printed beside it are, as "Footer credit" lines.

## Images

19 slides carry their page image under the heading: 6, 10, 17, 22, 26, 30–33, 37–40, 42–45, 48 and
56 — every slide with a distinct figure. The rest are the title, the decorative and application
pictures of slides 2, 3 and 51, build steps contained in an included slide (4–5, 8–9, 11–16, 25,
27–29, 53–55), slide 7 (a frame caught mid-animation), slides of text and equations transcribed
exactly (18–21, 34, 35, 46, 50), video stills (23, 24, 47, 49), repeats of an included figure (36
repeats 31; 41 repeats 17's loop beside text), the Go table of slide 52 (transcribed cell by cell),
the summary (57) and the announcements (58). Use only an image path that appears below; slides
without one have no image.

## Contents

| Slides | Section |
| ------ | ------- |
| 1 | Title: "Deep Reinforcement Learning" |
| 2–3 | Learning in dynamic environments; reinforcement learning in robotics, game play and strategy, and language modeling |
| 4–7 | Classes of learning problems: supervised, unsupervised and reinforcement learning, each with an apple example |
| 8–17 | Key concepts: agent, environment, actions and the action space, observations, state, reward, the return and the discounted return |
| 18–19 | Defining the Q-function; taking actions given a Q-function: the policy $\pi^{\ast}(s) = \operatorname{argmax}_ {a} Q(s, a)$ |
| 20–21 | Deep reinforcement learning algorithms: value learning versus policy learning |
| 22–24 | Digging deeper into the Q-function: two Atari Breakout state-action pairs, A and B, with videos of each policy |
| 25–31 | Deep Q networks: two architectures, the training target, the Q-loss, and the DQN summary |
| 32–34 | DQN Atari results (architecture and the 49-game chart); downsides of Q-learning |
| 35–40 | Policy learning: the policy-gradient key idea, discrete versus continuous action spaces, a Gaussian policy over a continuous action |
| 41–46 | Training policy gradients: the self-driving case study, the training algorithm, the loss and the gradient-descent update |
| 47–49 | Reinforcement learning in real life: why running to termination is a problem, the VISTA data-driven simulator, deployment on a real vehicle |
| 50–56 | Applications: the game of Go and AlphaGo's three-stage pipeline |
| 57 | Summary: foundations, Q-learning, policy gradients |
| 58 | Announcements |

## Slide 1 — Deep Reinforcement Learning

Title slide. Black background; at left a glowing blue network of nodes and lines (a mesh of connected points). A faint large diagonal watermark "MIT 6.S191" sits behind the text. Text, centred at right:

"Deep Reinforcement Learning"
"Alexander Amini"
"MIT Introduction to Deep Learning"
"January 7, 2026"

The MIT logo is at bottom centre-left and an "MIT EECS" logo at bottom right.

*Figure: no*

## Slide 2 — Learning in Dynamic Environments

Text: "Learning in Dynamic Environments". Below it, on a white background, a photograph-style illustration of a chrome robotic hand and forearm (metal with red parts, a red emblem on the forearm) reaching in from the left, with its index finger pointing toward a human hand reaching in from the right, whose index finger points back toward it; the two fingertips almost touch near the centre.

*Figure: yes — a robotic hand and a human hand reaching toward each other with fingertips almost touching*

## Slide 3 — Reinforcement Learning: Robots, Games, the World

Text: "Reinforcement Learning: Robots, Games, the World". Three columns, each with a heading above an image:

- "Robotics": an image split diagonally; the upper-left half shows a silver car on a road with a green arrow and outlined translucent figures of pedestrians on a purple-tinted street scene, and the lower-right half shows yellow and black robotic arms with grippers.
- "Game Play & Strategy" (printed on two lines: "Game Play" / "& Strategy"): an image split diagonally; the upper-left half shows a Go board with black and white stones, and the lower-right half shows the "StarCraft II" logo (printed "STARCRAFT" with a numeral II) over armoured game characters.
- "Language Modeling" (printed on two lines: "Language" / "Modeling"): an illustration of a chat window with a robot face, a speech bubble reading "Hello!", and a user avatar icon with a reply bar below.

*Figure: yes — three images for robotics, game play and strategy, and language modeling*

## Slide 4 — Classes of Learning Problems

Text: "Classes of Learning Problems". Only one column, at left:

"Supervised Learning"
"Data: $(x, y)$"
$x$ is data, $y$ is label
"Goal: Learn function to map $x \rightarrow y$"
"Apple example:" followed by a black-outline drawing of an apple, captioned "This thing is an apple."

*Figure: yes — outline drawing of an apple labelled "This thing is an apple."*

## Slide 5 — Classes of Learning Problems

Build step: adds the "Unsupervised Learning" column to slide 4.

Left column, "Supervised Learning":
"Data: $(x, y)$"
$x$ is data, $y$ is label
"Goal: Learn function to map $x \rightarrow y$"
"Apple example:" with the outline apple drawing, captioned "This thing is an apple."

Middle column, "Unsupervised Learning":
"Data: $x$"
$x$ is data, no labels!
"Goal: Learn underlying structure"
"Apple example:" with two apples side by side, a filled red apple with a green leaf and an outline apple, captioned "This thing is like the other thing." (printed on two lines: "This thing is like" / "the other thing.")

*Figure: yes — apple drawings under the supervised and unsupervised columns*

## Slide 6 — Classes of Learning Problems

![Slide 6 — Classes of Learning Problems](../images/05-reinforcement-learning/slide-6.jpg)

Build step: adds the "Reinforcement Learning" column to slide 5.

Left column, "Supervised Learning":
"Data: $(x, y)$"
$x$ is data, $y$ is label
"Goal: Learn function to map $x \rightarrow y$"
"Apple example:" with the outline apple drawing, captioned "This thing is an apple."

Middle column, "Unsupervised Learning":
"Data: $x$"
$x$ is data, no labels!
"Goal: Learn underlying structure"
"Apple example:" with a filled red apple and an outline apple, captioned "This thing is like the other thing."

Right column, "Reinforcement Learning":
"Data: state-action pairs"
"Goal: Maximize future rewards over many time steps"
"Apple example:" with an outline apple, captioned "Eat this thing because it will keep you alive." (printed on two lines: "Eat this thing because it" / "will keep you alive.")

*Figure: yes — apple drawings under the three columns of learning problems*

## Slide 7 — Classes of Learning Problems

Build step: slide 6 with the supervised and unsupervised columns faded out and a large overlay phrase added. This is a frame caught mid-animation: the faded left and middle columns (headings "Supervised Learning" and "Unsupervised Learning", their data and goal lines, "Apple example:" and the apple drawings with captions) are still faintly visible behind the overlay and are only partly legible; the supervised caption reads faintly as "This is an apple." and the unsupervised caption as "This thing is like the other thing."

Overlay text, large, centred over the faded columns: "RL: our focus today."

Right column, in full black, unchanged from slide 6:
"Reinforcement Learning"
"Data: state-action pairs"
"Goal: Maximize future rewards over many time steps"
"Apple example:" with an outline apple, captioned "Eat this thing because it will keep you alive."

*Figure: no*

## Slide 8 — Reinforcement Learning (RL): Key Concepts

Text: "Reinforcement Learning (RL): Key Concepts". At left, a black filled circle containing a white person icon (head and shoulders), labelled below it "AGENT". Definition at the bottom, centred: "Agent: takes actions." ("Agent" in bold.)

*Figure: yes — a person icon in a black circle labelled AGENT*

## Slide 9 — Reinforcement Learning (RL): Key Concepts

Build step: adds the environment to slide 8.

Text: "Reinforcement Learning (RL): Key Concepts". At left the person icon in a black circle labelled "AGENT"; at right a black circle containing a white tree silhouette with leaves, labelled below it "ENVIRONMENT". Definition at the bottom: "Environment: the world in which the agent exists and operates." ("Environment" in bold.) The slide still shows no "Agent: takes actions." line.

*Figure: yes — agent icon at left and environment (tree) icon at right*

## Slide 10 — Reinforcement Learning (RL): Key Concepts

![Slide 10 — Reinforcement Learning (RL): Key Concepts](../images/05-reinforcement-learning/slide-10.jpg)

Build step: adds actions to slide 9.

Text: "Reinforcement Learning (RL): Key Concepts". The "AGENT" person icon at left and the "ENVIRONMENT" tree icon at right. A red line leaves the bottom of the agent circle, runs down and right under the middle, and rises with an arrowhead into the bottom of the environment circle. On the horizontal part sits a red rounded box with white text "ACTIONS". Above the box, between the two icons, four small black arrows pointing up, right, down and left, and under them the label "Action: $a_t$".

Definitions at the bottom, centred, on two lines:
"Action: a move the agent can make in the environment."
"Action space $A$: the set of possible actions an agent can make in the environment"
("Action" and "Action space" in bold; no full stop after "environment" in the second line, as printed.)

*Figure: yes — agent sends ACTIONS (red arrow) to the environment, with four direction arrows and the label* $a_t$

## Slide 11 — Reinforcement Learning (RL): Key Concepts

Build step: adds observations to slide 10.

Text: "Reinforcement Learning (RL): Key Concepts". The agent and environment icons as before. The red "ACTIONS" path from the agent to the environment, with the label "Action: $a_t$" above it (the four small direction arrows of slide 10 are no longer shown). A new blue line leaves the top of the environment circle, runs up and left across the top, and descends with an arrowhead into the top of the agent circle; on the horizontal part sits a blue rounded box with white text "OBSERVATIONS".

Definition at the bottom: "Observations: of the environment after taking actions." ("Observations" in bold.)

*Figure: yes — agent and environment connected by an ACTIONS arrow (red) and an OBSERVATIONS arrow (blue)*

## Slide 12 — Reinforcement Learning (RL): Key Concepts

Build step: adds the state change to slide 11.

Text: "Reinforcement Learning (RL): Key Concepts". Same diagram as slide 11 (blue "OBSERVATIONS" path from environment to agent along the top; red "ACTIONS" path from agent to environment along the bottom; "Action: $a_t$" above the red box). New: under the blue "OBSERVATIONS" box the label "State changes: $s_{t+1}$".

Definition at the bottom: "State: a situation which the agent perceives." ("State" in bold.)

*Figure: yes — agent and environment loop with ACTIONS, OBSERVATIONS, the action* $a_t$ *and the state change* $s_{t+1}$

## Slide 13 — Reinforcement Learning (RL): Key Concepts

Build step: adds the reward to slide 12.

Text: "Reinforcement Learning (RL): Key Concepts". The same agent and environment loop as slide 12: blue "OBSERVATIONS" path along the top from the environment to the agent, red "ACTIONS" path along the bottom from the agent to the environment, "Action: $a_t$" above the red box. Under the blue box, two lines: "State changes: $s_{t+1}$" and, new, "Reward: $r_t$".

Definition at the bottom: "Reward: feedback that measures the success or failure of the agent's action." ("Reward" in bold; straight apostrophe in "agent's".)

*Figure: yes — agent and environment loop with ACTIONS, OBSERVATIONS, the state change* $s_{t+1}$ *and the reward* $r_t$

## Slide 14 — Reinforcement Learning (RL): Key Concepts

Build step: adds the total reward (return) to slide 13.

Text: "Reinforcement Learning (RL): Key Concepts". The same loop diagram as slide 13 (OBSERVATIONS, "State changes: $s_{t+1}$", "Reward: $r_t$", ACTIONS, "Action: $a_t$"). New, at bottom left, the label "Total Reward" / "(Return)" (two lines, "(Return)" in bold) with an arrow pointing to the displayed equation:

$$R_t = \sum_{i=t}^{\infty} r_i$$

The definition line of slide 13 is no longer shown.

*Figure: yes — loop diagram with the return equation* $R_t = \sum_{i=t}^{\infty} r_i$ *labelled "Total Reward (Return)"*

## Slide 15 — Reinforcement Learning (RL): Key Concepts

Build step: adds the expanded sum to slide 14.

Text: "Reinforcement Learning (RL): Key Concepts". The same loop diagram. At bottom left, the label "Total Reward" / "(Return)" ("(Return)" in bold) with an arrow to the equation, now extended:

$$R_t = \sum_{i=t}^{\infty} r_i = r_t + r_{t+1} \ldots + r_{t+n} + \cdots$$

*Figure: yes — loop diagram with the return written as a sum and as an expanded series*

## Slide 16 — Reinforcement Learning (RL): Key Concepts

Build step: replaces the return of slide 15 with a discounted return.

Text: "Reinforcement Learning (RL): Key Concepts". The same loop diagram. At bottom left the label, on three lines, "Discounted" / "Total Reward" / "(Return)" ("(Return)" in bold), with an arrow to the equation:

$$R_t = \sum_{i=t}^{\infty} \gamma^{i} r_i$$

The expanded series of slide 15 is not shown.

*Figure: yes — loop diagram with the discounted return equation* $R_t = \sum_{i=t}^{\infty} \gamma^i r_i$

## Slide 17 — Reinforcement Learning (RL): Key Concepts

![Slide 17 — Reinforcement Learning (RL): Key Concepts](../images/05-reinforcement-learning/slide-17.jpg)

Build step: adds the expanded series and the discount factor to slide 16.

Text: "Reinforcement Learning (RL): Key Concepts". The same loop diagram. At bottom left the label "Discounted" / "Total Reward" / "(Return)" ("(Return)" in bold), with an arrow to the equation:

$$R_t = \sum_{i=t}^{\infty} \gamma^{i} r_i = \gamma^{t} r_t + \gamma^{t+1} r_{t+1} \ldots + \gamma^{t+n} r_{t+n} + \cdots$$

Below the equation, with the leading $\gamma$ and its colon in bold: $\gamma$: "discount factor;" $0 \lt \gamma \lt 1$

*Figure: yes — loop diagram with the discounted return equation, its expansion and the discount-factor note*

## Slide 18 — Defining the Q-function

Text: "Defining the Q-function". Centred equation at top:

$$R_t = r_t + \gamma r_{t+1} + \gamma^{2} r_{t+2} + \cdots$$

Line below: "Total reward, $R_t$, is the discounted sum of all rewards obtained from time $t$"

Centred equation:

$$Q(s_t, a_t) = \mathbb{E}[R_t \vert s_t, a_t]$$

In the printed equation, $s_t$ is highlighted with a blue box and $a_t$ with a green box.

Text below, on two lines: "The Q-function captures the **expected total future reward** an agent in state, $s$, can receive by executing a certain action, $a$". The words "state, $s,$" are highlighted in blue and "action, $a$" in green, matching the highlights in the equation. ("expected total future reward" is bold.)

Note: the first equation here is written $R_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + \cdots$, whereas slide 17 wrote the powers of $\gamma$ as $\gamma^t$, $\gamma^{t+1}$, $\gamma^{t+n}$ (as printed).

*Figure: no*

## Slide 19 — How to take actions given a Q-function?

Text: "How to take actions given a Q-function?". Centred equation near the top:

$$Q(s_t, a_t) = \mathbb{E}[R_t \vert s_t, a_t]$$

with $s_t$ highlighted in blue and $a_t$ highlighted in green. Beneath it, two thin arrows point up from the label "(state, action)" to the highlighted $s_t$ and $a_t$; "state" is highlighted blue and "action" green within the label.

Text: "Ultimately, the agent needs a **policy $\pi(s)$**, to infer the **best action to take** at its state, s" (printed with a plain "s", no maths italics, and no full stop; "policy $\pi(s)$" and "best action to take" are bold).

Text: "**Strategy:** the policy should choose an action that maximizes future reward"

Centred equation near the bottom:

$$\pi^{\ast}(s) = \underset{a}{\mathrm{argmax}}\thinspace Q(s, a)$$

with $s$ highlighted in blue in $\pi^{\ast}(s)$ and in $Q(s, a)$, and $a$ highlighted in green under "argmax" and in $Q(s, a)$.

*Figure: no*

## Slide 20 — Deep Reinforcement Learning Algorithms

Section slide on a solid blue background. Title in white: "Deep Reinforcement Learning Algorithms". Two rounded white-outlined panels side by side:

Left panel: "Value Learning" (bold), then "Find $Q(s, a)$", then $a = \underset{a}{\mathrm{argmax}}\thinspace Q(s, a)$.

Right panel: "Policy Learning" (bold), then "Find $\pi(s)$", then "Sample $a \sim \pi(s)$".

*Figure: no*

## Slide 21 — Deep Reinforcement Learning Algorithms

Build step: slide 20 with the right panel faded out. The title and the left panel are as in slide 20 and stay in full white; the right panel ("Policy Learning", "Find $\pi(s)$", "Sample $a \sim \pi(s)$") is still faintly visible but faded into the blue background.

Left panel: "Value Learning" (bold), "Find $Q(s, a)$", $a = \underset{a}{\mathrm{argmax}}\thinspace Q(s, a)$.

*Figure: no*

## Slide 22 — Digging deeper into the Q-function

![Slide 22 — Digging deeper into the Q-function](../images/05-reinforcement-learning/slide-22.jpg)

Text: "Digging deeper into the Q-function". Left, a bold heading "Example:  Atari Breakout" (two spaces after the colon, as printed) over a still image of the game. The game still has a black score strip at top with grey blocky digits, then a grey frame (side walls and top). Inside the frame near the top is a band of coloured bricks in rows, from top to bottom red, orange, yellow, green and blue (the blue row is shifted slightly right and starts after a small gap at left). Lower in the black play area there is a small red ball and, at the bottom, a short red paddle, with a small teal square at the bottom of the left wall and a small red square at the bottom of the right wall. Annotation arrows are drawn on the still: a magenta arrow from the paddle up and to the left toward the bricks, a short magenta arrow pointing down and to the left from the ball toward the paddle, and two blue arrows on either side of the paddle, one pointing left and one pointing right.

Right, centred text on two lines: "It can be very difficult for humans to accurately estimate Q-values".

Below it, two black panels side by side. Panel "A" (label "A" in white at top left of the panel): a small red square at the top with a magenta arrow pointing straight down toward a wide red paddle below it, centred under the ball. Panel "B" (label "B"): a small red square at upper right with a short magenta arrow pointing down and to the left, and a wide red paddle at lower left with a short blue arrow pointing right at its right end.

Below the panels, on two lines: "Which $(s, a)$ pair has a higher Q-value?" (printed with bold non-italic "s" and "a"), followed by a thinking-face emoji at right.

*Figure: yes — Atari Breakout still with annotated arrows, and two small state-action panels A and B*

## Slide 23 — Digging deeper into the Q-function

Build step: replaces the left still of slide 22 with a video thumbnail and outlines panel A.

Text: "Digging deeper into the Q-function". Left heading (bold): "Example:  Atari Breakout - Middle". Below it, a game image of Breakout (grey frame, rainbow bricks with a one-brick-wide gap cut upward in the middle, a blue row with gaps, a small paddle at the bottom and a small ball at lower left), with a large red circle with a white play triangle over its centre, as a video thumbnail.

Right: "It can be very difficult for humans to accurately estimate Q-values". Panel "A" (red square above a magenta down arrow and a red paddle) is now enclosed in a dark red rounded outline; panel "B" (red square at upper right, short magenta arrow down-left, red paddle with a short blue arrow pointing right) is not outlined. Below: "Which $(s, a)$ pair has a higher Q-value?" and a thinking-face emoji. The magenta and blue annotation arrows of slide 22's left still are not shown here.

*Figure: yes — Breakout video thumbnail with play button, and panels A (outlined) and B*

## Slide 24 — Digging deeper into the Q-function

Build step: changes the video thumbnail to a "Side" clip and moves the outline from A to B.

Text: "Digging deeper into the Q-function". Left heading (bold): "Example:  Atari Breakout - Side". Below it, a Breakout game image (grey frame, rainbow bricks with several irregular gaps in the lower rows, a small blue and green brick remnant below the bricks at left, a small paddle at the bottom left), with a large red circle with a white play triangle over its centre.

Right: "It can be very difficult for humans to accurately estimate Q-values". Panel "A" is no longer outlined; panel "B" is now enclosed in a dark red rounded outline. Below: "Which $(s, a)$ pair has a higher Q-value?" and a thinking-face emoji.

*Figure: yes — Breakout video thumbnail with play button, and panels A and B (B outlined)*

## Slide 25 — Deep Q Networks (DQN)

Text: "Deep Q Networks (DQN)". Subtitle: "How can we use deep neural networks to model Q-functions?"

Footer credit: Mnih+ *Nature* 2015.

One rounded panel at left. Inside it, from left to right:

- Two inputs stacked. Top: a light-blue square holding a small Breakout game frame (rainbow bricks near the top, a small paddle at the bottom), labelled underneath "state, $s$". Below it: a light-green square holding the italic text "“move right”" (on two lines, "“move" / "right”"), labelled underneath "action, $a$".
- Each input has a black arrow with a right-angle bend pointing into the wide left edge of a peach-coloured trapezoid that narrows to the right, containing the text "Deep NN" (two lines, "Deep" / "NN").
- A black arrow from the narrow right edge of the trapezoid points to $Q(s, a)$.
- Top right of the panel, text on two lines: "Action + State → Expected Return" (with an arrow glyph; "Action + State →" / "Expected Return").
- Along the bottom of the panel, three column labels in bold: "Input" (under the inputs), "Agent" (under the network), "Output" (under the $Q(s, a)$ output).

*Figure: yes — DQN diagram: state and action in, a deep NN, a single Q-value out*

## Slide 26 — Deep Q Networks (DQN)

![Slide 26 — Deep Q Networks (DQN)](../images/05-reinforcement-learning/slide-26.jpg)

Build step: adds a second panel to slide 25.

Text: "Deep Q Networks (DQN)". Subtitle: "How can we use deep neural networks to model Q-functions?"

Footer credit: Mnih+ *Nature* 2015.

Left panel, unchanged from slide 25: state $s$ (Breakout frame, light-blue square) and action $a$ ("“move right”", light-green square) both feed a peach "Deep NN" trapezoid, whose output is $Q(s, a)$; panel text "Action + State → Expected Return"; bottom labels "Input", "Agent", "Output".

New right panel (rounded, same height): heading "State → Expected Return for Each Action" (with an arrow glyph). Inside: a light-blue square holding a Breakout frame labelled "state, $s$", with one black arrow into a peach "Deep NN" trapezoid (narrowing to the right). From its right edge a short stub splits into three arrows pointing to three outputs, listed top to bottom: $Q(s, a_1)$, $Q(s, a_2)$, $Q(s, a_n)$, with a gap between the second and third (no dots printed). In each, the action symbol ($a_1$, $a_2$, $a_n$) is highlighted in green. Bottom labels in bold: "Input", "Agent", "Output".

*Figure: yes — two DQN architectures side by side: state and action in, one* $Q(s, a)$ *out; state in, a Q-value for each action out*

## Slide 27 — Deep Q Networks (DQN): Training

Build step: adds a callout and changes the title of slide 26.

Text: "Deep Q Networks (DQN): Training" (title changed from "Deep Q Networks (DQN)"). Subtitle: "How can we use deep neural networks to model Q-functions?"

Footer credit: Mnih+ *Nature* 2015.

The two panels of slide 26 are unchanged (left: state and action in, $Q(s, a)$ out; right: state in, $Q(s, a_1)$, $Q(s, a_2)$, $Q(s, a_n)$ out, actions highlighted green).

New, centred below the panels: a black rounded callout box with a thinking-face emoji at left and white text on two lines: "What happens if we take all the best actions?" and, in bold italics, "Maximize target return → train the agent".

*Figure: yes — the two DQN panels with a callout asking what happens if we take all the best actions*

## Slide 28 — Deep Q Networks (DQN): Training

Build step: replaces the callout of slide 27 with the target expression.

Text: "Deep Q Networks (DQN): Training". Subtitle: "How can we use deep neural networks to model Q-functions?"

Footer credit: Mnih+ *Nature* 2015.

The two panels of slide 26 and 27 are unchanged. Below them, at centre-left, a curly brace labelled "target" above it and, under the brace, the expression

$$\left( r + \gamma \max_{a'} Q(s', a') \right)$$

At lower right, a black rounded callout box with a yellow light-bulb icon at left and white text on two lines: "Take all the best actions →" and "target return" (with an arrow glyph).

*Figure: yes — the two DQN panels with the target expression* $r + \gamma \max_{a'} Q(s', a')$ *braced and labelled "target"*

## Slide 29 — Deep Q Networks (DQN): Training

Build step: adds the predicted $Q(s, a)$ to slide 28. This frame is caught mid-animation: the "target" label, brace and expression from slide 28 are still printed but faded to light grey.

Text: "Deep Q Networks (DQN): Training". Subtitle: "How can we use deep neural networks to model Q-functions?"

Footer credit: Mnih+ *Nature* 2015.

The two panels are unchanged. Below them at left, faded: the label "target", its brace and the expression $\left( r + \gamma \max_{a'} Q(s', a') \right)$. New, in full black to the right of it: the label "predicted" above a brace over $Q(s, a)$. At lower right, a black rounded callout box with a yellow light-bulb icon and white text on two lines: "Network" / "prediction" (the "Take all the best actions → target return" callout of slide 28 is replaced).

*Figure: yes — the two DQN panels with the faded target expression and the new predicted* $Q(s, a)$ *with a "Network prediction" callout*

## Slide 30 — Deep Q Networks (DQN): Training

![Slide 30 — Deep Q Networks (DQN): Training](../images/05-reinforcement-learning/slide-30.jpg)

Build step: adds the full Q-loss equation to slide 29 (the "target" term is now in full black and the "Network prediction" callout is gone).

Title: "Deep Q Networks (DQN): Training". Subtitle: "How can we use deep neural networks to model Q-functions?"

The two boxes are as on slide 29 (left: state $s$ and action $a$, "move right", into "Deep NN", out to $Q(s,a)$, "Action + State → Expected Return"; right: state $s$ into "Deep NN", out to $Q(s, a_1)$, $Q(s, a_2)$, $Q(s, a_n)$, "State → Expected Return for Each Action"; column labels "Input", "Agent", "Output" under each).

Below, a bracket labelled "target" over $r + \gamma \max_{a'} Q(s', a')$ and a bracket labelled "predicted" over $Q(s,a)$, in the equation:

$$\mathcal{L} = \mathbb{E}\left[ \left\Vert \left(r + \gamma \max_{a'} Q(s', a')\right) - Q(s,a) \right\Vert^2 \right]$$

To the right of the equation, the bold label "Q-Loss".

Footer credit: Mnih+ *Nature* 2015.

*Figure: yes — Q-network diagrams with the Q-loss equation, target and predicted terms bracketed*

## Slide 31 — Deep Q Network Summary

![Slide 31 — Deep Q Network Summary](../images/05-reinforcement-learning/slide-31.jpg)

Title: "Deep Q Network Summary". Subtitle: "Use NN to learn Q-function and then use to infer the optimal policy, $\pi(s)$".

Left: a Breakout-style game frame on a light-blue square labelled "state, $s$". An arrow goes to a peach trapezoid labelled "Deep NN". From its output an arrow splits to three rows, each with a green-highlighted action and a green arrow icon underneath:

- $Q(s, a_1) = 20$ with a green left-pointing arrow below.
- $Q(s, a_2) = 3$ with a green X below.
- $Q(s, a_3) = 0$ with a green right-pointing arrow below.

Arrows from the three values converge on the text at right: $\pi(s) = \operatorname{argmax}_ {a} Q(s,a)$ and on the next line $= a_1$ followed by a green left-pointing arrow. A thick black line leaves this text, runs down and left along the bottom, and points up to the state image; beneath it: "Send action back to environment and receive next state".

*Figure: yes — Q-network outputs three Q-values (20, 3, 0) for left, stay and right; argmax picks the left action, which is sent back to the environment*

## Slide 32 — DQN Atari Results

![Slide 32 — DQN Atari Results](../images/05-reinforcement-learning/slide-32.jpg)

Title: "DQN Atari Results". A network diagram, left to right: a small game screenshot (a dark frame with a blue loop-shaped line) with a highlighted square patch; lines from the patch fan out to a column of seven grey feature-map squares (top and bottom ones faded), under the heading "Convolution" with a small down-triangle; a blue circle icon with a ReLU-like ramp; a second "Convolution" block in two sub-columns: on the left seven larger grey maps (top and bottom faded), each with a vertical column of small blue squares beside it, and on the right seven small grey squares (top and bottom faded), with lines running from the small blue squares to the right-hand squares; a second blue ramp icon; a column pair of vertical dotted columns of nodes under "Fully connected" (many black dots, grey at the top and bottom, lines from one central node fanning to many); a third blue ramp icon; a second "Fully connected" column of dots whose lines converge on a column of 18 blue rounded buttons: "No input", then eight joystick directions (arrows up, up-right, right, down-right, down, down-left, left, up-left) then a red dot (fire), then the eight directions each with "+" and a red dot. At far right, a black joystick with a red button.

Footer credit: Mnih+ *Nature* 2015.

*Figure: yes — DQN architecture for Atari: two convolution layers, two fully connected layers, with outputs for joystick actions*

## Slide 33 — DQN Atari Results

![Slide 33 — DQN Atari Results](../images/05-reinforcement-learning/slide-33.jpg)

Title: "DQN Atari Results". A bar chart of DQN performance on 49 Atari games.

Axes: the vertical axis (on the right side) is labelled "% Human Level Performance", with ticks 0%, 100%, 200%, 300%, 400%, 500%, 600% then a break (double slash), then 1000% and 4500% at the top. The horizontal axis lists game names, one bar per game, rotated labels. The legend, at top right, is two tall vertical rectangles side by side: a blue one with "DQN" printed inside it, rotated, and a grey one with "Best Linear Learner" printed inside it in white, rotated. Each game has a blue bar (DQN) and a grey bar (best linear learner) behind it; many bars carry dark grey error bars with small caps (Video Pinball's reaches nearly to the 4500% tick). A vertical blue line crosses the chart between "H.E.R.O." and "Asterix". Above the chart a double-headed horizontal blue arrow spans both sides of the line, with the text "Surpass human-level" to the left of the line and "Below human-level" to the right.

There are two series: DQN (blue) and Best Linear Learner (grey). The printed percentage labels, in bar order from left to right (the values in the bars are for DQN):

"Video Pinball 2539%", "Boxing 1707%", "Breakout 1327%", "Star Gunner 598%", "Robotank 508%", "Atlantis 449%", "Crazy Climber 419%", "Gopher 400%", "Demon Attack 294%", "Name This Game 278%", "Krull 277%", "Assault 246%", "Road Runner 232%" (its middle digit is blurred at the deck's resolution), "Kangaroo 224%", "James Bond 145%", "Tennis 143%", "Pong 132%", "Space Invaders 121%", "Beam Rider 119%", "Tutankham 112%", "Kung-Fu Master 102%", "Freeway 102%", "Time Pilot 100%", "Enduro 97%", "Fishing Derby 93%", "Up and Down 92%", "Ice Hockey 79%", "Q*Bert 78%", "H.E.R.O. 76%" (all of these left of the line), then "Asterix 69%", "Battle Zone 67%", "Wizard of Wor 67%", "Chopper Command 64%", "Centipede 62%", "Bank Heist 57%", "River Raid 57%", "Zaxxon 54%", "Amidar 43%", "Alien 42%", "Venture 32%", "Seaquest 25%", "Double Dunk 17%", "Bowling 14%", "Ms. Pacman 13%", "Asteroids 7%", "Frostbite 6%", "Gravitar 5%", "Private Eye 2%", "Montezuma's Revenge 0%".

The bars fall from far above 100% at the left (Video Pinball, Boxing and Breakout lie above the axis break) down to near 0% at the right. The grey (linear learner) bar rises above the blue bar on four games: most clearly Double Dunk, where the grey bar reaches roughly 175% (with an error bar) against DQN's 17%; and by smaller margins Tennis (grey to about 158% against 143%), Kung-Fu Master (about 128% against 102%) and Centipede (a thin grey cap above 62%). Ms. Pacman's bar is grey-tinted at its top. The percentage labels are small and were read from enlarged crops; the short dash before some of them (Seaquest, Bowling, Private Eye) is an error-bar cap, not part of the label.

Footer credit: Mnih+ *Nature* 2015.

*Figure: yes — bar chart of DQN versus best linear learner as % of human-level performance on 49 Atari games, sorted from highest to lowest*

## Slide 34 — Downsides of Q-learning

Title: "Downsides of Q-learning". Text, left-aligned:

"**Complexity**:"
- "Can model scenarios where the action space is discrete and small"
- "Cannot handle continuous action spaces"

"**Flexibility**:"
- "Policy is deterministically computed from the Q function by maximizing the reward → cannot learn stochastic policies"

Centred, larger: "To address these, consider a new class of RL training algorithms:" and on the next line "Policy gradient methods".

*Figure: no*

## Slide 35 — Deep Reinforcement Learning Algorithms

Blue background, white text. Title: "Deep Reinforcement Learning Algorithms". Two rounded boxes side by side. The left box is faded: "Value Learning", "Find $Q(s,a)$", $a = \operatorname{argmax}_ {a} Q(s,a)$. The right box is in full white: "Policy Learning", "Find $\pi(s)$", "Sample $a \sim \pi(s)$".

*Figure: no*

## Slide 36 — Deep Q Networks (DQN)

Title: "Deep Q Networks (DQN)". Subtitle: "**DQN:** Approximate Q-function and use to infer the optimal policy, $\pi(s)$".

A Breakout-style game frame on a light-blue square labelled "state, $s$" feeds an arrow into a peach trapezoid "Deep NN". Its output arrow splits into three rows: $Q(s, a_1) = 20$ (green-highlighted $a_1$, green left arrow below), $Q(s, a_2) = 3$ (green X below), $Q(s, a_3) = 0$ (green right arrow below). Arrows from all three go to $\pi(s) = \operatorname{argmax}_ {a} Q(s,a)$, next line $= a_1$ with a green left arrow.

*Figure: yes — Q-network outputs three Q-values and argmax selects the left action*

## Slide 37 — Policy Gradient (PG): Key Idea

![Slide 37 — Policy Gradient (PG): Key Idea](../images/05-reinforcement-learning/slide-37.jpg)

Title: "Policy Gradient (PG):  Key Idea" (two spaces after the colon, as printed). The line "**DQN:** Approximate Q-function and use to infer the optimal policy, $\pi(s)$" is faded. Below it, in full black: "**Policy Gradient:** Directly optimize the policy $\pi(s)$".

A Breakout-style game frame labelled "state, $s$" feeds an arrow into "Deep NN". Its output arrow splits into three rows:

- $P(a_1|s) = 0.9$ with green left arrow.
- $P(a_2|s) = 0.1$ with green X.
- $P(a_3|s) = 0$ with green right arrow.

Arrows from the three go to $\pi(s) \sim P(a|s)$ and next line $= a_1$ with a green left arrow. Above right, the expression $\sum_{a_i \in A} P(a_i|s) = 1$ with an upward-opening curly brace below it and a thin arrow down from the brace to the $\pi(s)$ text.

At the bottom, a black rounded banner with a thinking-face emoji and the white text "What are some advantages of this formulation?".

*Figure: yes — policy network outputs a probability for each of three actions (0.9, 0.1, 0) summing to 1; the action is sampled*

## Slide 38 — Discrete vs Continuous Action Spaces

![Slide 38 — Discrete vs Continuous Action Spaces](../images/05-reinforcement-learning/slide-38.jpg)

Title: "Discrete vs Continuous Action Spaces". Line: "**Discrete action space:** which direction should I move?" followed by three green icons: a left arrow, an X, a right arrow.

Left: a Breakout-style game frame labelled "state, $s$" with a black arrow pointing right to a bar chart. The chart has a vertical axis labelled $P(a|s)$ and a horizontal axis labelled $a$ with arrowheads at both ends. Three green bars sit on the axis, with icons and labels below: "Left" (green left arrow; the tallest bar, left of the vertical axis), "Stay" (green X; a short bar centred on the vertical axis, about a quarter of the height of the Left bar) and "Right" (green right arrow; a very thin, barely visible bar). One series of three bars.

*Figure: yes — bar chart of probabilities over three discrete actions: Left high, Stay low, Right near zero*

## Slide 39 — Discrete vs Continuous Action Spaces

![Slide 39 — Discrete vs Continuous Action Spaces](../images/05-reinforcement-learning/slide-39.jpg)

Build step: adds the continuous-action-space panel to slide 38; the discrete line is faded.

Title: "Discrete vs Continuous Action Spaces". Faded line: "**Discrete action space:** which direction should I move?" with its three arrow icons. In full black: "**Continuous action space:** how fast should I move?" followed by a green left arrow containing the text "0.7 m/s".

Left: the game frame labelled "state, $s$" with a black arrow to a plot. The plot has a vertical axis labelled $P(a|s)$ and a horizontal axis labelled $a$. A green filled bell-shaped curve is centred left of the vertical axis, extends across it, and is near zero at both ends. Below the horizontal axis at left: a green left arrow with the text "Faster Left"; at right: a green right arrow with the text "Faster Right".

*Figure: yes — a Gaussian-shaped probability density over a continuous action (speed and direction), centred left of zero*

## Slide 40 — Policy Gradient (PG): Key Idea

![Slide 40 — Policy Gradient (PG): Key Idea](../images/05-reinforcement-learning/slide-40.jpg)

Title: "Policy Gradient (PG):  Key Idea" (two spaces after the colon, as printed). Line: "**Policy Gradient:** Enables modeling of continuous action space".

The game frame labelled "state, $s$" feeds an arrow into "Deep NN", whose output splits into two:

- "Mean, $\mu$ = $-1$"
- "Variance, $\sigma^2$ = 0.5"

Arrows from both lead to $P(a|s) = N(\mu, \sigma^2)$, then $\pi(s) \sim P(a|s)$, then $= -0.8$ "[m/s]" with a green left arrow below. Above, the expression $\int_{a=-\infty}^{\infty} P(a|s) = 1$ with a curly brace below it and an arrow down from the brace to the $P(a|s)$ line.

At the bottom, a small plot titled $P(a|s) = N(\mu, \sigma^2)$: a green bell curve with its peak at the tick labelled $-1$ left of the vertical axis, horizontal axis $a$, and under it "Faster Left" with a green left arrow and "Faster Right" with a green right arrow.

*Figure: yes — the network outputs a mean and variance defining a Gaussian over actions, from which an action of −0.8 m/s is sampled*

## Slide 41 — Training Policy Gradients: Case Study

Title: "Training Policy Gradients: Case Study".

Left, "Reinforcement Learning Loop:" a cycle diagram. At left a black circle with a white person silhouette (the agent); at right a black circle with a white tree (the environment). A blue arrow runs from the tree along the top to the person, passing through a blue label "OBSERVATIONS" with the text under it "State changes: $s_{t+1}$" and "Reward: $r_t$". A red arrow runs from the person along the bottom to the tree, passing through a red label "ACTIONS" with the text above it "Action: $a_t$".

Right, "Case Study – Self-Driving Cars" and four lines:

"Agent:" "vehicle"
"State:" "camera, lidar, etc"
"Action:" "steering wheel angle"
"Reward:" "distance traveled"

*Figure: yes — the agent-environment loop (observations of state and reward, actions) beside a self-driving case study*

## Slide 42 — Training Policy Gradients

![Slide 42 — Training Policy Gradients](../images/05-reinforcement-learning/slide-42.jpg)

Title: "Training Policy Gradients". Left: "**Training Algorithm**" and the numbered list:

"1. Initialize the agent"
"2. Run a policy until termination"
"3. Record all states, actions, rewards"
"4. Decrease probability of actions that resulted in low reward"
"5. Increase probability of actions that resulted in high reward"

Right: a top-down road drawn as two vertical dashed black lines. A blue car at the bottom, between the lines. A blue curved line (the trajectory) leaves the car, bends first to the right (around points 1 and 2) and then to the left, ending at the left dashed line with a red and yellow collision burst. Black dots lie along the trajectory, each with a dashed line to a label on the right: from the bottom up $(s_0, a_0, r_0)$ (at the car), $(s_1, a_1, r_1)$, $(s_2, a_3, r_2)$, $(s_3, a_3, r_3)$, $(s_4, a_4, r_4)$ (at the collision). The label $(s_2, a_3, r_2)$ is printed with $a_3$, as printed. The lower part of the road background is shaded green (around points 0 and 1) and the upper part red (around points 2, 3 and 4); both bands extend past the dashed lines.

Footer credit: Williams *Reinforcement Learning* 1992.

*Figure: yes — a car trajectory recorded as states, actions and rewards, ending in a collision, with green (good) and red (bad) shaded regions*

## Slide 43 — Training Policy Gradients

![Slide 43 — Training Policy Gradients](../images/05-reinforcement-learning/slide-43.jpg)

Build step: the list is unchanged from slide 42; the road figure shows a different trajectory, without the $(s,a,r)$ labels.

Title: "Training Policy Gradients". Left: "**Training Algorithm**" and the same five-item list as slide 42 ("1. Initialize the agent", "2. Run a policy until termination", "3. Record all states, actions, rewards", "4. Decrease probability of actions that resulted in low reward", "5. Increase probability of actions that resulted in high reward").

Right: two vertical dashed lines. A blue car at the bottom; the blue trajectory weaves up and to the right, with black dots along it, ending at the right dashed line with a red and yellow collision burst. A green shaded block lies behind the lower dots and a red shaded block behind the upper ones. No $(s,a,r)$ labels are shown here.

*Figure: yes — a second car trajectory ending in a collision at the right lane line, with green and red shaded regions*

## Slide 44 — Training Policy Gradients

![Slide 44 — Training Policy Gradients](../images/05-reinforcement-learning/slide-44.jpg)

Build step: the list is unchanged from slide 43; the road figure shows a different trajectory, with no dots or shading.

Title: "Training Policy Gradients". Left: "**Training Algorithm**" and the same five-item list as slide 42.

Right: two vertical dashed lines. A blue car at the bottom; a blue curve leaves it, swings right and then left, and ends at the top of the left dashed line with a red and yellow collision burst. No dots, labels or shading.

*Figure: yes — a car trajectory ending in a collision at the top of the left lane line*

## Slide 45 — Training Policy Gradients

![Slide 45 — Training Policy Gradients](../images/05-reinforcement-learning/slide-45.jpg)

Build step: shows a third trajectory and boxes items 4 and 5 of the list from slide 44.

Title: "Training Policy Gradients". Left: "**Training Algorithm**" and the same five-item list as slide 42. Items 4 and 5 ("4. Decrease probability of actions that resulted in low reward", "5. Increase probability of actions that resulted in high reward") are enclosed in a green rounded rectangle, with a thinking-face emoji at its lower right corner.

Right: two vertical dashed lines and a blue car at the bottom. A blue curve leaves the car and runs the whole length of the road between the lines, wiggling slightly, to the top with no collision.

*Figure: yes — a car trajectory that stays within the lane, beside the boxed update steps*

## Slide 46 — Training Policy Gradients

Build step: adds the loss and the gradient descent update to slide 45 and removes the road figure.

Title: "Training Policy Gradients". Left: the heading "**Training Algorithm**" and the same five-item list as slide 42, with items 4 and 5 in the green rounded rectangle (no emoji).

Right: a label "log-likelihood of action" in green above the term $\log P(a_t|s_t)$ (green highlight), and a label "reward" in orange below $R_t$ (orange highlight), in the equation:

$$\mathbf{loss} = -\log P(a_t|s_t) \thinspace R_t$$

Below it, the bold heading "**Gradient descent update:**" and two lines:

$$w' = w - \nabla \mathbf{loss}$$

$$w' = w + \nabla \log P(a_t|s_t) \thinspace R_t$$

The term $\nabla \log P(a_t|s_t) \thinspace R_t$ in the second line is enclosed in a blue rounded box, with the blue label "Policy gradient!" beneath it.

Footer credit: Williams *Reinforcement Learning* 1992.

*Figure: no*

## Slide 47 — Reinforcement Learning in Real Life

Title: "Reinforcement Learning in Real Life". Left: "**Training Algorithm**" and the same five-item list as slide 42 ("1. Initialize the agent", "2. Run a policy until termination", "3. Record all states, actions, rewards", "4. Decrease probability of actions that resulted in low reward", "5. Increase probability of actions that resulted in high reward"). Item 2, "2. Run a policy until termination", is enclosed in a red rounded rectangle.

Right: a video still (a play button in a red circle at its centre) of a car on a curving paved road at the edge of a steep, rocky hillside under a cloudy sky; a small figure sits on the roadside ahead. A black skull-and-crossbones icon is at the top right of the image.

Footer credit: Amini+ *IEEE RA-L* 2020.

*Figure: yes — a video still of a car on a mountain road with a skull-and-crossbones icon, beside the training algorithm with step 2 boxed in red*

## Slide 48 — Data-driven Simulation for Autonomous Vehicles

![Slide 48 — Data-driven Simulation for Autonomous Vehicles](../images/05-reinforcement-learning/slide-48.jpg)

Title: "Data-driven Simulation for Autonomous Vehicles". Subtitle: "**VISTA**: Photorealistic and high-fidelity simulator for training and testing self-driving cars".

A grid of 18 frames (3 rows of 6), each a dashboard-camera view from a car whose bonnet is visible at the bottom. Row 1: a snowy path with bare trees; a residential street with a house and wires; a parking garage; a highway; a city crosswalk with high-rises; a road behind a cement-mixer truck. Row 2: an intersection with a silver SUV and a brick tower; a dark night frame with glare; a road with a white SUV and bare trees; a road with a white building and a signal, partly behind the play button; a wide tree-lined daytime road with cars; a night road with a lamp post and a yellow lane line. Row 3: a riverside road with a brick building; a road with a pickup truck and bare trees; a street with houses and a pedestrian; a dark night street with a lamp; an autumn road with parked cars; an autumn road with a guardrail and a dark car. A red circle with a white triangle and a white rim, a video play button, sits between columns 3 and 4 of row 2.

Footer credit: Amini+ *IEEE RA-L* 2020.

*Figure: yes — a grid of 18 driving-camera frames from the VISTA simulator across different roads, lighting and seasons, with a video play button*

## Slide 49 — Deploying End-to-End RL for Autonomous Vehicles

Title: "Deploying End-to-End RL for Autonomous Vehicles".

Left: a video still (red play button at its centre) from a car driving along a narrow paved road through bare trees and dry leaves, with the car's bonnet at the bottom. Overlaid: a green circle at top left with green text "AUTONOMOUS" and white text "9.7 kph" beneath it; red text "EXTERIOR" at top right; at the bottom right an inset photo of the car's interior (steering wheel and dashboard) with the red text "INTERIOR"; at the bottom left, red text "2X playback".

Right, three centred text blocks separated by two green downward chevrons:

"Policy Gradient RL agent trained entirely within VISTA simulator"
(green chevron)
"End-to-end agent directly deployed into the real-world"
(green chevron)
"**First full-scale autonomous vehicle trained using RL entirely in simulation and deployed in real life!**"

Footer credit: Amini+ *IEEE RA-L* 2020.

*Figure: yes — a video still of the autonomous vehicle on a real road with exterior and interior views, beside a three-step flow from simulation to real-world deployment*

## Slide 50 — Deep Reinforcement Learning Applications

Section divider. Blue background; centred white text: "Deep Reinforcement Learning Applications".

*Figure: no*

## Slide 51 — Reinforcement Learning and the Game of Go

Title: "Reinforcement Learning and the Game of Go". A photograph of a wooden Go board seen at an angle, covered with black and white stones.

Footer credit: Silver+ *Science* 2016; Silver+ *Nature* 2017.

*Figure: yes — a photograph of a Go board with black and white stones*

## Slide 52 — The Game of Go

Title: "The Game of Go". Line: "**Aim:** Get more board territory than your opponent."

Left: a Go board diagram (19 by 19 grid, wooden colour) with black and white stones in many positions and one black stone marked with a red ring.

Right: a table with four columns. Headers: "Board Size n x n", "Positions $3^{n^2}$", "% Legal", "Legal Positions". Rows:

| Board Size n x n | Positions $3^{n^2}$ | % Legal | Legal Positions |
| --- | --- | --- | --- |
| 1×1 | 3 | 33.33% | 1 |
| 2×2 | 81 | 70.37% | 57 |
| 3×3 | 19,683 | 64.40% | 12,675 |
| 4×4 | 43,046,721 | 56.49% | 24,318,165 |
| 5×5 | 847,288,609,443 | 48.90% | 414,295,148,741 |
| 9×9 | $4.434264882 \times 10^{38}$ | 23.44% | $1.03919148791 \times 10^{38}$ |
| 13×13 | $4.300233593 \times 10^{80}$ | 8.66% | $3.72497923077 \times 10^{79}$ |
| 19×19 | $1.740896506 \times 10^{172}$ | 1.20% | $2.08168199382 \times 10^{170}$ |

Below the table: "Greater number of legal board positions than atoms in the universe."

Footer credit: Source: Wikipedia.

*Figure: yes — a Go board diagram and a table of board sizes with numbers of positions and legal positions*

## Slide 53 — AlphaGo Beats Top Human Player at Go

Title: "AlphaGo Beats Top Human Player at Go". A left-to-right pipeline of icons, each with a label above, with all labels as printed:

- "Human expert positions": a Go board image.
- A thick black arrow labelled "Classification" pointing to
- "Supervised Learning policy network": a small green network of nine nodes with connecting lines.
- A black circular double-arrow icon with the text "Self Play" inside.
- "RL policy network": a green network icon.
- A second "Self Play" circular-arrow icon.
- "Self-play data": a Go board image.
- A thick black arrow labelled "Regression" pointing to
- "Value network": an orange network icon.

The lower part of the slide is empty.

Footer credit: Silver+ *Science* 2016.

*Figure: yes — the AlphaGo training pipeline from human positions through supervised, RL and value networks*

## Slide 54 — AlphaGo Beats Top Human Player at Go

Build step: adds a bracket and the label "1) Initial training: human data" to slide 53.

Title: "AlphaGo Beats Top Human Player at Go". The pipeline is as on slide 53: "Human expert positions" (board image), arrow "Classification", "Supervised Learning policy network", circular arrows "Self Play", "RL policy network", circular arrows "Self Play", "Self-play data" (board image), arrow "Regression", "Value network".

Below the pipeline, at left, a curly bracket spans from the human positions image to the Supervised Learning policy network, with the text "1) Initial training: human data".

Footer credit: Silver+ *Science* 2016.

*Figure: yes — the AlphaGo pipeline with step 1 (initial training on human data) bracketed*

## Slide 55 — AlphaGo Beats Top Human Player at Go

Build step: adds a second bracket and the label "2) Self-play and reinforcement learning → super-human performance" to slide 54.

Title: "AlphaGo Beats Top Human Player at Go". The same pipeline as on slide 53, with the bracket and "1) Initial training: human data" from slide 54. Below it, a second curly bracket spans from just right of the first one (under the Supervised Learning policy network) to the "Self-play data" board, with the text "2) Self-play and reinforcement learning" and on the next line "→ super-human performance".

Footer credit: Silver+ *Science* 2016.

*Figure: yes — the AlphaGo pipeline with steps 1 and 2 bracketed*

## Slide 56 — AlphaGo Beats Top Human Player at Go

![Slide 56 — AlphaGo Beats Top Human Player at Go](../images/05-reinforcement-learning/slide-56.jpg)

Build step: adds a third bracket and the label "3) “Intuition” about board state" to slide 55.

Title: "AlphaGo Beats Top Human Player at Go". The same pipeline as on slide 53, with the brackets "1) Initial training: human data" and "2) Self-play and reinforcement learning → super-human performance" from slide 55. A third curly bracket, lower down at right, spans from the "Self-play data" board to the "Value network", with the text "3) “Intuition” about board state" (curly quotation marks as printed).

Footer credit: Silver+ *Science* 2016.

*Figure: yes — the AlphaGo pipeline with all three stages bracketed and labelled*

## Slide 57 — Deep Reinforcement Learning: Summary

Title: "Deep Reinforcement Learning: Summary". Three columns, each with a blue rounded header and a bullet list, and an image below.

"Foundations":
- "Agents acting in environment"
- "State-action pairs → maximize future rewards"
- "Discounting"
Below: a black circle with a white person silhouette.

"Q-Learning":
- "Q function: expected total reward given $s$, $a$" (the $s$ and $a$ are in a bold serif face)
- "Policy determined by selecting action that maximizes Q function"
Below: a Breakout-style game frame (black field, rainbow rows of bricks, red paddle, a score line at the top).

"Policy Gradients":
- "Learn and optimize the policy directly"
- "Applicable to continuous action spaces"
Below: a black steering-wheel icon.

*Figure: yes — summary columns for foundations, Q-learning and policy gradients, with a person icon, a game frame and a steering wheel*

## Slide 58 — T-Shirts Coming Tomorrow!

Announcement slide, black background. At left, a photograph of a dark grey T-shirt with a red and white logo made of connected-network columns spelling "MIT", the vertical text "6.S191" and the text "DEEP LEARNING". Right, white text:

"T-Shirts Coming Tomorrow!"
"**SYLLABUS:** bit.ly/6s191-syllabus" (the link in red, underlined)
"1. Project sign-ups due **TMRW 1/8 11:59pm ET**"
"2. Lab competitions and prizes!"
"EXTENDED DEADLINE: Friday 1/9 11:00am ET" (bold "EXTENDED DEADLINE:" and "Friday 1/9 11:00am ET" as printed)
"3. **Project and lab submission links on syllabus!**"
"4. **RESUME DROP** to sponsoring companies!"
"introtodeeplearning.com/jobs.html" (red, underlined, bold)

*Figure: no*
