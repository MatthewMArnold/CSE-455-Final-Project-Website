---
title: Machine Learning Approach
layout: template
filename: ml-approach.html
--- 

As mentioned in the classical approach, our machine learning approach builds off of our colleagues
attempts at building a model that can accurately play the rune game. For more information regarding
the rune game and the terminology surrounding it, please refer to the classical-cv documentation.

## Dataset and Limitations
One of the major challenges with using ML to solve this detection problem is a lack of a diverse
dataset. We only have labeled footage from two videos, so any model we train would be extremely
overfit to the data that we do have labeled. While one approach would be to find and label more
data, this approach is challenging since the amount of first person footage of the rune game that we
have access to is limited.

Through our classical CV approach, we used contours and edge detection to locate key parts of the
center and the petal. Unfortunately, our dataset has only labelled the rectangular area of the
plate. This means that we would be unable to make use of the entire structure of both the center and
the petal to better enhance our model's understanding of where the target plate is. This could
potentially lead to identifying any glowing blue/red rectangular object as the target plate which
means our model would not be robust.

## Approach

We decided to test in particular two different types of models. A CenterNet-like model, which has
been used with great success by our team for other tasks in the "RoboMaster" competition and a Fully
Convolutional One-Stage Object Detection model which is based off of previous [open-source
works](https://github.com/tianzhi0549/FCOS).

## Findings

After changing hyperparameters such as the number of layers, the types of Nodes, decays, optimizers,
and activation functions, we could not detect significant change between our model and the model
worked on by our colleagues. It seems as if the type of model that we are using has minimal effect
on the success and accuracy of our model which might suggest that our only avenues of improvement
would be to collect more data rather than to refine our model.

Another problem with the machine learning approach is that the inferencing on the video frames takes
too long. We average approximately 10 frames per second on our more heavyweight models and we
created a lot more lightweight models that were able to average ~20 frames per second with similar
results. However, this still falls short of our 60fps goal which might suggest that a pure machine
learning approach to this problem would not be the right way to approach it.

When running our model on our test video, we can see that it performs relatively well on the red
petals and plates. While our model does seem to miss a couple of frames, we can see that overall
that it is able to sufficiently detect where the plates are. However, tests on the blue video
showcase the downfall of our model. For one, it is unable to accurately determine the position of
the blue plates. Worse, it is mislabelling a red rectangle in the image as one of the plates it is
supposed to target. This provides evidence that the fault in our model lies in its tendency to
overfit to our dataset. Due to the nature of our dataset, we have more frames with red plates that
are labelled than blue plates.

Moving forward, there are a couple of solutions that we could try to solve this issue. One is that
we convert all our images to grayscale before we train our model on them. This will help remove the
problem of the model only finding red rectangles but could cause an issue where it believes that any
rectangle in the frame is a plate. Another solution is to simply increase the number of frames with
labelled blue plates in our dataset. While this would be an ideal solution, obtaining data has been
hard especially with Covid cancelling the past two years of RoboMaster leaving us unable to collect
more data. Finally, we could combine a classical CV approach with our machine learning model. One
approach to this would be to have our machine learning model understand where the entire structure
is in the frame and then use contours and other edge detection methods to determine where the plates
are. This would definitely be something that we would want to investigate in the future.
