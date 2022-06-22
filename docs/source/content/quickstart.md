# Quickstart

<br/>

Lets get you up and running!
___

### Install the python package

```python
pip install eucalyptus
```

### Import package and initialize sdk
```python
import eucalyptus

eucalyptus.initialize(api_token="<API_TOKEN_STRING>")
```


> **Note**: API tokens can be generated through the dashboard

### Register a new model
```python
features = pd.DataFrame(data=iris.data, columns=iris.feature_names)
target = pd.DataFrame(data=iris.target, columns=['target'])
eucalyptus.create_new_model("iris_classifier", "v1", "classifier", features, target)
```

### Log the training data for reference
```python
eucalyptus.log_training_data("iris_classifier", "v1", features, target)
```

> **Note**: We do not store the raw data in our database. Only the data distribution get saved.

### Logging Predictions
```python
for i in range(5):
    eucalyptus.log_prediction(model_name="iris_classifier", model_version="v1",
                              features={"sepal_length_cm": round(random.uniform(0, 5), 2),
                                        "petal_width_cm": round(random.uniform(0, 5), 2),
                                        "sepal_width_cm": round(random.uniform(0, 5), 2),
                                        "petal_length_cm": round(random.uniform(0, 5), 2)
                                        },
                              prediction=random.choice([0, 1, 2, 3])
                              )
```

### Log ground truth values
```python
request_ids = [
    "9bff624d-9cc8-462c-890f-93c678f2444c",
    "4cf61751-81b4-44d1-8f09-42e762bc65ff",
    "54f7fea3-b9f8-4edd-9b0b-fa0d1bd7bb3b"
]
actuals = [3, 0, 0]
eucalyptus.log_actuals("iris_classifier", request_ids=request_ids, actuals=actuals)
```
> **Note**: You can get the request_ids from the dashboard


