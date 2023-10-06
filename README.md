# Fashion Classifier Deep Learning Model with FastAPI Backend

This repository contains code for a fashion classifier deep learning model and a FastAPI backend that serves the model as an API. The goal is to make the model available for predictions through API endpoints. Additionally, it provides instructions on how to deploy the API on Amazon Elastic Container Service (ECS) using Docker (though deployment is optional and can be adapted as needed).

## Code Files

### `main.py`

This file contains the FastAPI application and the functions responsible for preprocessing images, loading the TensorFlow Lite model, making predictions, and decoding the results. Here's a breakdown of the key components:

1. **FastAPI Setup**: The FastAPI application is created in this file, and it includes the following endpoints:

   - `POST "/"`: This endpoint allows users to upload an image for classification. It preprocesses the image, passes it through the TensorFlow Lite model, and returns the predicted label.
   - `GET "/health"`: This is a health check endpoint to verify the status of the application.
   - `GET "/labels"`: This endpoint returns a list of possible labels/categories for the fashion items that the model can classify.

2. **Preprocessing**: The `preprocess` function reads an image from the request, converts it to the required format, and preprocesses it for model input.

3. **Model Loading and Prediction**: The `model` function loads the TensorFlow Lite model (`clothing-model-v4.tflite`) and makes predictions on the preprocessed image.

4. **Decoding Predictions**: The `decode` function maps the model's prediction results to human-readable labels.

### `Dockerfile`

The Dockerfile is used to build a Docker image that includes the necessary dependencies and files for running the FastAPI application. The steps include installing Python packages from `requirements.txt`, copying the TensorFlow Lite model and the `main.py` file, and specifying the command to run the FastAPI application with Uvicorn.

## Deployment (Optional)

To deploy this FastAPI application on Amazon ECS using Docker, you can follow these steps:

1. Build the Docker image:

   ```bash
   docker build -t fashion-classifier-api .
   ```

2. Push the Docker image to a container registry (e.g., Amazon ECR) if needed.

3. Create an ECS cluster and task definition that uses the Docker image you built.

4. Deploy the task to the ECS cluster.

5. Set up an Application Load Balancer (ALB) to route incoming requests to the ECS service.

6. Configure security groups and network settings as needed for your specific deployment.

7. Access the API through the ALB's URL.

## Requirements

The `requirements.txt` file contains the necessary Python packages and dependencies required to run the FastAPI application and TensorFlow Lite model. Ensure that these dependencies are installed in your environment before running the application.

Please note that this README assumes basic knowledge of Docker and Amazon ECS for deployment. Adjust the deployment steps according to your specific cloud provider and infrastructure setup.

Feel free to modify and adapt the code and deployment process to suit your project's requirements. Enjoy using the Fashion Classifier API!
