Download Link: https://assignmentchef.com/product/solved-cs520assignment-4-colorization
<br>
The purpose of this assignment is to demonstrate and explore some basic techniques in supervised learning and computer vision.

<strong>The Problem: </strong>Consider the problem of converting a picture to black and white.

Figure 1: Training Data – A color image and its corresponding greyscale image.

Typically, a color image is represented by a matrix of 3-component vectors, where Image[<em>x</em>][<em>y</em>] = (<em>r,g,b</em>) indicates that the pixel at position (<em>x,y</em>) has color (<em>r,g,b</em>) where <em>r </em>represents the level of red, <em>g </em>of green, and <em>b </em>blue respectively, as values between 0 and 255. A classical color to gray conversion formula is given by

Gray(<em>r,g,b</em>) = 0<em>.</em>21<em>r </em>+ 0<em>.</em>72<em>g </em>+ 0<em>.</em>07<em>b,                                </em>(1)

where the resulting value Gray(<em>r,g,b</em>) is between 0 and 255, representing the corresponding shade of gray (from totally black to completely white).

Note that converting from color to grayscale is (with some exceptions) <em>losing </em>information. For most shades of gray, there will be many (<em>r,g,b</em>) values that correspond to that same shade.

However, by training a model on similar images, we can make contextually-informed guesses at what the shades of grey ought to correspond to. In an extreme case, if a program recognized a black and white image as containing a tiger (and had experience with the coloring of tigers), that would give a lot of information about how to color it realistically.

Figure 2: Trained on the Color/Grayscale image in Fig.1, recovers some green of the trees, and distinguishing blues between sea and sky. But there are definitely some obvious mistakes as well.

You have a lot of freedom in your approach to this, but carefully formulate each of the following in outlining your solution to the problem, expressing your design choices, the math, and the algorithms behind your solution:

1

<strong>Computer Science Department – Rutgers University                                                          Fall 2018</strong>

<ul>

 <li><strong>Representing the Process: </strong>How can you represent the coloring process in a way that a computer can handle? What spaces are you mapping between? What maps do you want to consider? Note that mapping from a single grayscale value <strong>gray </strong>to a corresponding color (<em>r,g,b</em>) on a pixel by pixel basis, you do not have enough information in a single gray value to reconstruct the correct color (usually).</li>

 <li><strong>Data: </strong>Where are you getting your data from to train/build your model? What kind of pre-processing might you consider doing?</li>

 <li><strong>Evaluating the Model: </strong>Given a model for moving from grayscale images to color images (whatever spaces you are mapping between), how can you evaluate how good your model is? How can you assess the error of your model (hopefully in a way that can be learned from)? Note there are at least two things to consider when thinking about the error in this situation: numerical/quantified error (in terms of deviation between predicted and actual) and <em>perceptual </em>error (how good do humans find the result of your program).</li>

 <li><strong>Training the Model: </strong>Representing the problem is one thing, but can you train your model in a computationally tractable manner? What algorithms did you draw on? How did you determine convergence? How did you avoid overfitting?</li>

 <li><strong>Assessing the Final Project: </strong>How good is your final program, and how can you determine that? How did you validate it? What is your program good at, and what could use improvement? Do your program’s mistakes ‘make sense’? What happens if you try to color images unlike anything the program was trained on? What kind of models and approaches, potential improvements and fixes, might you consider if you had more time and resources?</li>

</ul>

<strong>Some Possible Approaches</strong>

Some possible approaches you might take to the problem include the following (and where used to generate the small example above):

<ul>

 <li>While mapping from gray 7→ (<em>r,g,b</em>) cannot reliably reconstruct the true color of a pixel, not having enough information in a single gray value, consider looking at a small 3 × 3 pixel window of gray values, and mapping this set of <em>nine </em>gray values to a single (<em>r,g,b</em>) color vector, which could for instance be the color of the middle pixel in this window. In this case, the surrounding eight gray values give additional context and information to build a color for the central pixel. With such a map, a grayscale image could be colored by simply taking every 3 × 3 pixel patch, and determining what color the central pixel should be.</li>

 <li>To further simplify things, the problem can be shifted from a <em>regression </em>problem to a <em>discrete classification </em>problem in the following way: consider building an initial palette of <em>K </em>representative colors, and instead of trying to reconstruct the true color of a pixel, determine which of these <em>K </em>colors should best be applied to a given pixel. How can you determine which <em>K </em>colors are best to use, however? And be careful as well – how should you assess error and the quality of a model when coloring in this way?</li>

 <li>It may also be useful to reduce the input space as well as the output space – consider for instance the set of all possible 3 × 3 pixel patches that occur in a given image, much like overlapping jigsaw puzzle pieces. Do all possible jigsaw puzzle pieces occur in representing a given image, or could the overall space be reduced to consider only a set of ‘representative’ puzzle pieces?</li>

</ul>

2





