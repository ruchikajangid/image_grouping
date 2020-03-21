## Image Grouping

There are two ways of getting features from image, first is an image descriptors(white box algorithms), second is a neural nets(black box algorithms). Here the first method is implemented.
There are many algorithms for feature extraction, most popular of them are SURF, ORB, SIFT, BRIEF. Most of this algorithms based on image gradient. Here KAZE descriptor is used, because it shipped in the base OpenCV library, while others are not, just to simplify installation.
The feature extractor was made.

Most of feature extraction algorithms in OpenCV have same interface.
So extract_features first detect keypoints on image(center points of our local patterns). The number of them can be different depend on image so we add some clause to make our feature vector always same size(this is needed for calculation, because we can’t compare vectors of different dimensions)
Then we build vector descriptors based on our keypoints, each descriptor has size 64 and we have 32 such, so our feature vector is 2048 dimension.
batch_extractor just run our feature extractor in a batch for all our images and saves feature vectors in pickled file for further use.
Then the Matcher class was made that was used for matching our search image with images in our database.

Here we are loading our feature vectors from previous step and create from them one big matrix, then we compute cosine distance between feature vector of our search image and feature vectors database, and then just output Top N results.
This is just a demo, for production use better to use some algorithm for fast computation of cosine distance for millions of images.
