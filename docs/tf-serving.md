---
title: TensorFlow Serving
---


#### Serve a Tensorflow model in 60 seconds

```
# Download the TensorFlow Serving Docker image and repo
docker pull tensorflow/serving

git clone https://github.com/tensorflow/serving

# Location of demo models
TESTDATA="$(pwd)/serving/tensorflow_serving/servables/tensorflow/testdata"

# Start TensorFlow Serving container and open the REST API port
docker run -t --rm -p 8501:8501 \
    -v "$TESTDATA/saved_model_half_plus_two_cpu:/models/half_plus_two" \
    -e MODEL_NAME=half_plus_two \
    tensorflow/serving &

# Query the model using the predict API
curl -d '{"instances": [1.0, 2.0, 5.0]}' \
    -X POST http://localhost:8501/v1/models/half_plus_two:predict

# Returns => { "predictions": [2.5, 3.0, 4.5] }

```

<br>

#### What is TensorFlow Serving?
 * TensorFlow Serving is a **flexible, high-performance** serving system for machine learning models, designed for **production** environments.
 * It deals with the inference aspect of machine learning, taking models after training and managing their lifetimes, providing clients with versioned access via a high-performance, reference-counted lookup table.
 * TensorFlow Serving provides out-of-the-box integration with TensorFlow models, but can be easily extended to serve other types of models and data.

---
#### References
 * [TensorFlow Serving](https://github.com/tensorflow/serving)
 * [MINST Example](https://colab.research.google.com/github/tensorflow/tfx/blob/master/docs/tutorials/serving/rest_simple.ipynb#scrollTo=0w5Rq8SsgWE6)
 * [Building Standard TensorFlow ModelServer](https://www.tensorflow.org/tfx/serving/serving_advanced)
