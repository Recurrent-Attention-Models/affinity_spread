# affinity_spread



display_images : This folder contains the images used in the experiment. All selected from COCO 2017 validation set. 

display_images_with dots : This folder contains the images used in the experiment with the four versions of dot placements. 

datasets -> datasets_grouping -> test_data_groupiong.xls : This excel file contains the info for all the 1020 experimental trials. Each row specified one trial with these info:

['img_id',
 'img_name',
 'same_diff',
 'close_far',
 'first_dot_xy',
 'second_dot_xy',
 'same_object_anns_ind',
 'diff_object_anns_ind',
 'distance',
 'Img_shape']

datasets -> datasets_grouping -> train_data_groupiong.xls : We applied our dot placement algorithm to the COCO 2017 training set in order to select many more trials. If you intend to train your model on the same-different task use this file. The images are completely separate from the images used in the experiment. The file contains the same info with the same format as the test_data_grouping.xls. 


datasets -> loaddata_g.py : This file can read in the excel files for testing and training and give you a pytorch dataloader with the below function:  

fetch_dataloader(args, batch_size, train='train', shuffle=True)

The args needs to have these components: 
args.batch_size – set as 1 because images have different sizes 
args.resize – whether to resize the images - only in use when running detr 
args.coco2017_path  – path to coco, have to be downloaded separately 
args.dataset_grouping_dir  - this is the folder where the xls files are

Also a function is included to plot the dots over images. 


utils for display images and dot locations.ipynb : Some useful stuff to play around the display images and plot them. 

datasets -> datasets_grouping -> Human_grouping_data.xls : This is the main file containing raw behavioral data. We have 72 subjects in total. 

['RECORDING_SESSION_LABEL',
 'Trial_Index_',
 'subj_id',
 'trial_id',
 'block_id',
 'trial_id_block',
 'trial_type',
 'image_id',
 'img_id',
 'image',
 'image_dims',
 'target',
 'same_diff',
 'close_far',
 'first_dot_xy',
 'second_dot_xy',
 'first_dot_to_image',
 'first_dot_to_second_dot',
 'soa',
 'same_button',
 'REACTION_TIME',
 'RT_EVENT_BUTTON_ID']

preprocess behavioral data.ipynb : Use this notebook to preprocess the behavioral data. I have already saved the preprocessed files (test_data_grouping_with_all_beh.xls, test_data_grouping_with_mean_beh.xls, df_beh_c.xls) in the datasets -> datasets_grouping folder so you don’t really have to run this file, unless you want to change something. 

human behavior analyses.ipynb : This notebook takes in the preprocessed files and analyzes the RTs and percentiles. It also calculates the subject-subject agreements and some sample trials with average RTs from subjects. 

model results analyses.ipynb : 

Affinity_spread_demo_standalone_colab.ipynb : This is a standalone simplified version of the code to run in Colab. 


experimental methods.gdoc : provides the method details of the experiment 

Behavioral methods

Participants:

72 Stony Brook University undergraduate students participated in our experiment for course credit. Their mean age was 20.4 years (range = 17–32) and all had normal or corrected-to-normal vision. This study was approved by the school Institutional Review Board. 

Stimuli and Apparatus:

We selected 288 images from the Microsoft COCO (Common Objects in Context) dataset, which has images of complex everyday scenes depicting common objects in their natural context. The images also come with object-level segmentations, which we used to generate four versions of each display: "same-close" (two dots in the same object with a close distance), "same-far" (two dots in the same object with a far distance), "different-close" (two dots in two different objects with a close distance), and "different-far" (two dots in two different objects with a far distance). We ensured that the distances are controlled for between the two same/different conditions preventing the participants to make the same/different decision based on distance. Fig.~\ref{fig:beh_exp}C shows the placement of the dots across all four conditions. The assignment of images to the four conditions was counterbalanced across participants. The experiment was conducted on a 19-inch flat-screen CRT ViewSonic SVGA monitor with a screen resolution of 1024×768 pixels and a refresh rate of 100 Hz. Participants were seated approximately 70 cm away from the monitor, which resulted in the screen subtending a visual angle of 30◦ ×22◦. This meant that around 34 image pixels spanned approximately 1 degree of visual angle. The two dots used in the experiment were located around 3 degrees from the central fixation point for the close condition and 6 degrees for the peripheral dot. Gaze position during reading was recorded using an EyeLink 1000 eye-tracking system (SR Research) with a sampling rate of 1000 Hz. Gaze coordinates were parsed into fixations using the default Eyelink algorithm, which employed a velocity threshold of 30 degrees per second and an acceleration threshold of 8000 degrees per second squared. Calibration drift was checked before every trial, and recalibration was performed if necessary to ensure accurate eye-tracking data. 

Procedure:

Participants were instructed to determine whether two dots belonged to the same object or different objects. Each trial started with the presentation of a fixation cross, which remained on the screen for 500 ms, indicating the location of the central dot. At the start of each trial, both central and peripheral cues were displayed for 1,000 ms without the image. Next the cues were superimposed and flickered at a frequency of 5 Hz to ensure their visibility. During the trial, participants were required to maintain their gaze on the screen for the entire duration. If their gaze deviated more than 1 degree of visual angle away from the first dot during this period, the trial was terminated. To record their responses, participants utilized a Microsoft gamepad controller, with buttons randomly assigned to the "same" or "different" condition. The experiment consisted of a total of 32 practice trials and 256 experimental trials. The experimental trials were divided into four blocks, with breaks provided between the blocks. The order of image presentation was randomized across the trials. To provide accuracy feedback, a sound alarm was used to indicate an incorrect response to participants. We removed one experimental image from our analyses as the ground truth response was ambiguous leavening 255 experimental images and 1020 (255*4) trials for behavioral analyses and model comparison. 





