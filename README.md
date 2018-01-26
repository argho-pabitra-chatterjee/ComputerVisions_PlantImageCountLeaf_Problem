# Find how many leaves are visible in the plant image - Computer Visions Problem Object detection 

CV problems are both interesting and challenging, especially when we want something very specific. CV techniques do not generalize well in an uncontrolled environments.

In a 2-day effort, tried 3 techniques - 
1) morphological transformations
2) Haar Cascade classifier
3) template matching [matching the tip of leaves to generalize for other leaves]

So a classifier to detect objects can be the best solution, here I have trained manually a Haar Cascade classifier, which is detecting leaves but with more data, memory resources  and time, it can be more accurate.

There were other techniques like SVM linear kernel, KNN as which I plan to train and upload results soon.

Accuracy is highly dependent on the image[i.e. how well it is suiting to the controlled environments.]  I have outlined some observed points:

Template Matching
-----------------------
They perform better over rigid bodies. Since Leaves are not rigid body, I have considered only the tip with a threshold of 0.7-0.8 so that it generalizes well over new leaf samples [as tips are similar, especially in black and white images]
This solution works only on a very controlled environment. They perform better with overlapping edges, provided at least a partial leaves outline is visible on the background.
So if we have large number of such templates, it generalizes well on the tips of leaves.
But it will not be able to detect those leafs whose tips are not visible on the outline.


Thresholding + Morphological Operations + Contour detection
-------------------------------------------------------------------------------------------
This techniques are useful when the leaves are visible on the outline of the plant.
For slight overlapping, these techniques can work fine, but for thick overlapping, these techniques might not help here because Contour finding cannot segregate the overlapping structures and hence we get joint contour for some complicated structures.
These techniques work best when images are captured in a controlled environment.


Haar Cascade Classifier
-------------------------
This solution works best in real word compared to other traditional CV techniques described above, provided we have ample variations and enough set of each variations to train and test a model.
Here I used the opencv_createsamples to create positive samples, which basically superimposes portions of the leaf part on the background. The background is the negative sample. I took around 1200 positive samples and 3000 negative samples and trained it for 9 stages. The leaf data was manually selected before creating positive samples.

This technique performs better and can identify leaves with background noise in complicated structures like a leaf not visible on the outline of the image, plus also it does well where leaves are thickly overlapping.

Conclusion
------------------
Due to the limitations of traditional CV techniques, machine learning techniques like deep learning using CNN, SVM linear kernel, etc. have come up with promising outputs. The only challenge is that it requires a lot of computational power and variations in the data to show good results.
