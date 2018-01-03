#Create a folder on your computer. 

cd ~

mkdir tf_files

tf_files $ ls

bottlenecks             food                    inception               label_image.py          retrained_graph.pb      retrained_labels.txt

tf_files $ cd food/

food $ ls

ba_gua          ba_zhang        chakli          jalebi          samosa


#Start a docker virtual container (virtual VM) and copy tf_files to your container

using this command

docker run -it -v $HOME/tf_files:/tf_files gcr.io/tensorflow/tensorflow:latest-devel

------------------------- Do this in the Docker image -------------------------------

Retrieve the training code:

cd /tensorflow

git pull

Start training your model:

python /tensorflow/tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/tf_files/bottlenecks \
--how_many_training_steps 500 \
--model_dir=/tf_files/inception \
--output_graph=/tf_files/retrained_graph.pb \
--output_labels=/tf_files/retrained_labels.txt \
--image_dir /tf_files/food



Classify a Ba Gua:

python /tf_files/label_image.py /tf_files/food/ba_gua/pic_001.jpg


You will get a result something like this:

For Ba Gua:

ba gua (score = 0.97737)

ba zhang (score = 0.02263)

For Ba Zhang:

ba zhang (score = 0.96333)

ba gua (score = 0.03667)