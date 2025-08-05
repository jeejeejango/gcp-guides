# Vertex AI Gemini with Service Account ADC

## Create the Service Account

1. Create the service account from [Console](https://cloud.google.com/iam/docs/service-accounts-create#console)
2. Assign service account with IAM permission - Vertex AI User (roles/aiplatform.user)

## Prepare the Service Account

1. Make sure the service account has the right permission (e.g. Editor role) in [IAM console](https://console.cloud.google.com/iam-admin/iam)
2. Generate service account key for the SA in [Service Account](https://console.cloud.google.com/iam-admin/serviceaccounts) and saved locally

## Prepare your local environment

1. Use environment variable for ADC with the json file:

```bash
    export GOOGLE_APPLICATION_CREDENTIALS=<path to json file>
```

## Using REST Endpoint

1. Using gcloud and ADC to get the access token:

```bash
    ACCESS_TOKEN=$(gcloud auth application-default print-access-token)
```

2. Input the environment variables based on the GCP project and model:

```bash
PROJECT_ID="<your project id>"
LOCATION_ID="global"
API_ENDPOINT="aiplatform.googleapis.com"
MODEL_ID="gemini-2.5-flash"
GENERATE_CONTENT_API="streamGenerateContent"
```

Alternative `MODEL_ID="gemini-2.5-pro"`

### Invoking the Vertex AI Gemini endpoint

3. Prepare your input in request.json

4. Invoke the API endpoint:

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer ${ACCESS_TOKEN}" \
"https://${API_ENDPOINT}/v1/projects/${PROJECT_ID}/locations/${LOCATION_ID}/publishers/google/models/${MODEL_ID}:${GENERATE_CONTENT_API}" -d '@request.json'
```

## Using Python SDK

1. Go to [Vertex AI Studio](https://console.cloud.google.com/vertex-ai/studio/)
2. Click **Build with code** button > **Get code** to get the Python code to run the Gemini endpoints
3. Install the Vertex AI SDK to your application
4. Embed/Modify the code in your application

# References

- [feedbackMigrate from the Gemini Developer API to the Gemini API in Vertex AI](https://cloud.google.com/vertex-ai/generative-ai/docs/migrate/migrate-google-ai)
- [Authenticate to Vertex AI](https://cloud.google.com/vertex-ai/docs/authentication)
- [feedbackSet up ADC for on-premises or another cloud provider](https://cloud.google.com/docs/authentication/set-up-adc-on-premises)
