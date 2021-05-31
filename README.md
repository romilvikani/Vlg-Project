# Transfer Learning
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
- **convert_image_into_np_array**: an image from a file is loaded into a numpy array hence, it returns a uint8 numpy array with shape (img_height, img_width, 3) and has the file path as its argument. Here, the 3 refers to channels which is 3 in case of RGB.
- **draw_detections**: it uses visualize_boxes_and_labels_on_image_array method present in the viz_utils library to visualize the detections hence, produces images as output when called. Its important arguments are the annotated_image_np array, boxes, classes, and scores.

7. The file paths of all the training images of the model are stored in a variable named image_path and the convert_image_into_np_array method created in previous step is called for each of the individual image_path.

8. annotate method of colab_utils library is used to manually annotate the training images by putting boxes around the toy ducks and clicking next image until “All images completed!!” is shown after which submit button shall be clicked. If it is successful, --boxes array populated-- is shown and the gt-boxes named numpy array is filled with data of these images. It is stored in the format (x-coordinate of top left corner of the box, x-coordinate of top left corner of box, width of the box, height of the box)

9. The data is prepared for training in this step. The duck class is assigned a class id of 1 and as there is only class to detect, number of classes is set to 1. Then a for loop is run for each pair of training image and its corresponding data present in gt_box_np, which are in train_images_np and gt_boxes, respectively. The train_image_np array is converted to a tensor and added to train_image_tensors along with addition of a new dimension in the tensor at axis = 0. Hence, np array of shape (width, height, 3) is converted to tensor of shape (1, width, height, 3). 

   Similarly, gt_box_np is converted to a tensor and stored in gt_boxes_tensors. 

   The non-background classes start counting at 1 index. So to start counting at the zeroth index we shift the classes by 1 index using class_id_decrement variable and store it    in tensor 'zero_indexed_groundtruth_classes' which are then converted to one_hot_tensors in the next line.
   
10. The SSD ResNet50 checkpoint is downloaded.

11. The pipeline configuration is loaded here and a detection model is built using the model_builder library. Also the num_classes is overridden to be 1 here as it is 90 initially as we are using a COCO architecture which has 90 classes by default.
  
