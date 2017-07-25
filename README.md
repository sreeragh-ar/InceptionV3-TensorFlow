#launch docker
docker run -it   --publish 6006:6006   --volume ${HOME}/tf_files:/tf_files   --workdir /tf_files   gcr.io/tensorflow/tensorflow:latest-devel bash

#retrain inception with your own classes (now you are inside the docker)
python retrain.py \
  --bottleneck_dir=bottlenecks \
  --how_many_training_steps=500 \
  --model_dir=inception \
  --summaries_dir=training_summaries/basic \
  --output_graph=retrained_graph.pb \
  --output_labels=retrained_labels.txt \
  --image_dir=cars

#Evaluation
python evaluation.py <image-name>.jpg
