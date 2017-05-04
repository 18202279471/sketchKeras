# sketchKeras
An u-net with some algorithm to take sketch from paints.

# requirement
* Keras
* Opencv
* tensorflow/theano
* numpy

# download mod
see release

# performance
Currently there are many edge-detecting algrithoms or nerual networks. But few of them has good performance on paintings, espatially those from comic or animate. Most of these existing methods just detect the edge and then add lines to the edge. However, we need a method to convert the painting to a sketch which looks like a painter drawed the outline of picture. It is important when we want to train a nerual networks to colorlize pictures.**(Paper is on the way)**

Here is a example of artificial sketch for reference.

![goal](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/github/example.png)

Here a conclusion of existing methods to handle the problem.
* use opencv and implements a high-pass effect to get edge
* train a nerual network (HED Edge Detect)(PaintsChainer's lnet)
* use this sketchKeras which combined algorithm and nerual networks

Take this pic as an example (get from internet and I am finding the author.)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/raw.jpg)

If we use the high-pass algorithm via opencv or something else, we may get this one:

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/opencv.jpg)

As we can see, the result is far from artificial sketch. To achieve better performance, we may modify the parameters and enhance the pic, then this one:

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/opencv_enhanced.jpg)

The result is still not good. People like to add shadow to their drawing by add dense lines and these lines or points will become noise and disturb the high-pass algorithm. It is apprent that we can modify the parameters or use denoise methods to improve these, but drawings differ from one another and it is impossible to handle these automatically.

Then let us try the **lnet of PaintsChainer** (similar to HED)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/paintsChainer_lnet.jpg)
d
The result from nerual networks looks different from those from algorithm. However, this is still not so good.
The author of PaintsChainer use threslod to avoid noise and normalize the line, as this:

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/paintsChainer_lnet_threshold.jpg)

In this picture, we can see clearly that the noise, espeacilly near eyes and in the shadow of hair. "threslod" can filter some noise but some useful lines is also dropped. Last but not least, the lines are too coarse and thick. Here is a reference of thresloded artificial sketch:

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/github/example.jpg)

eAs we can see, though the picture is denoised by "threslod", it differs far from real artificial sketch. So it remains much improvement place in paintsChainer.

Finally, let us see the result of sketchKeras:

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/sketchKeras.jpg)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/sketchKeras_enhanced.jpg)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/sketchKeras_pured.jpg)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test1/sketchKeras_colored.jpg)

The four results are generated by sketchKeras. You can use your favorite one to generate your own training dataset for colorize networks.

---

## another example

(picture is from internet and I am finding the author.)
raw picture:

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/raw.jpg)

opencv and high-pass (all detail and noise remained so it is not suitable for training a colorize network)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/opencv.jpg)

opencv and high-pass enhanced (still not so good and we can see the pic is going to become a grayscaled detailed pic but not a sketch)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/opencv_enhanced.jpg)

paintsChainer's lnet (all detail and noise remained, espcially the hair)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/paintsChainer_lnet.jpg)

paintsChainer's lnet (thresloded) (just look at the hair)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/paintsChainer_lnet_threshold.jpg)

Pics below are generated by sketchKeras. It can drop some noise and unimportant detail to achieve better performance.

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/sketchKeras.jpg)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/sketchKeras_enhanced.jpg)

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/sketchKeras_pured.jpg)

## ability to generate colored highlighted sketch

As you can see, sketchKeras has the ability to generate colored highlighted sketch.

![pic](https://raw.githubusercontent.com/lllyasviel/sketchKeras/master/test2/sketchKeras_colored.jpg)
