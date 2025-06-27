# Vertex AI Gemini with Service Account ADC

## Prepare the Service Account

1. Make sure the service account has the right permission (e.g. Editor role) in [IAM console](https://console.cloud.google.com/iam-admin/iam)
2. Make sure the key is valid for the SA in [Service Account](https://console.cloud.google.com/iam-admin/serviceaccounts)

## Prepare your local environment

3. Use environment variable for ADC with the json file:

```bash
    export GOOGLE_APPLICATION_CREDENTIALS=<path to json file>
```

4. Using gcloud and ADC to get the access token:

```bash
    ACCESS_TOKEN=$(gcloud auth application-default print-access-token)
```

5. Input the environment variables based on the GCP project and model:

```bash
PROJECT_ID="<your project id>"
LOCATION_ID="global"
API_ENDPOINT="aiplatform.googleapis.com"
MODEL_ID="gemini-2.5-flash"
GENERATE_CONTENT_API="streamGenerateContent"
```

Alternative `MODEL_ID="gemini-2.5-pro"`

## Invoking the Vertex AI Gemini endpoint

6. Prepare your input in request.json

7. Invoke the API endpoint:

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer ${ACCESS_TOKEN}" \
"https://${API_ENDPOINT}/v1/projects/${PROJECT_ID}/locations/${LOCATION_ID}/publishers/google/models/${MODEL_ID}:${GENERATE_CONTENT_API}" -d '@request.json'
```

# References

- [feedbackMigrate from the Gemini Developer API to the Gemini API in Vertex AI](https://cloud.google.com/vertex-ai/generative-ai/docs/migrate/migrate-google-ai)
- [Authenticate to Vertex AI](https://cloud.google.com/vertex-ai/docs/authentication)
