# Vlg-Project
## Project’s Aim
•	To collect 5-15 images of a rubber duck and then manually annotate them i.e. put bounding boxes around them to get the labels for (x,y,w,h).\
•	Load a pretrained SSD with ResNet-50 and finetune it on these images.\
•	Run the object detection algorithm on a new image to identify the rubber duck.

## Code Explained
1. Tensorflow-gpu 2.5.0 is installed using pip install command.
2. Then TensorFlow library is imported as tf for usage ahead. Also, OS module that provides functions to interact with operation system, Pathlib module that provides functions to work on paths of files in system and IO module which aids in dealing with various input/output are imported.
3. The TensorFlow model’s repository is cloned.
4. The object detection api is installed. First the protocol buffers of the api are compiled and then the setup is installed using pip install.
5. Few more required libraries are imported. Ipython.display libraries, imageio, Image and visualization_utils for visualizing the output images. colab_utils for manually annotating the images.
6. 2 methods are defined here:-                                                                    
- convert_image_into_np_array: an image from a file is loaded into a numpy array hence, it returns a uint8 numpy array with shape (img_height, img_width, 3) and has the file path as its argument. Here, the 3 refers to channels which is 3 in case of RGB./
- draw_detections: it uses visualize_boxes_and_labels_on_image_array method present in the viz_utils library to visualize the detections hence, produces images as output when called. Its important arguments are the annotated_image_np array, boxes, classes, and scores.
  
