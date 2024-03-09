# ⚙️ Setup

## Required Vault

```json
{
  "APP_NAME": "{product}-{service_name}",
  "APP_PORT": "{port_http_number}",
  "APP_GRPC_PORT": "{port_grpc_number}",
  "APP_TIMEZONE": "Asia/Jakarta",
  "APP_DEBUG": "false",
  "APP_ENV": "development",
  "APP_READ_TIMEOUT_SECOND": "10",
  "APP_WRITE_TIMEOUT_SECOND": "15",
  "APP_KEY" : "",
  "APP_DEFAULT_LANG": "en",

  "LOGGER_NAME": "{product}-{service_name}",
  "LOGGER_LEVEL": "info",

  "APM_ADDRESS": "",
  "APM_ENABLE": "false",
  "APM_SERVICE_NAME": "{product}-{service_name}",

  "REDIS_HOST": "",
  "REDIS_DB": "0",
  "REDIS_PASSWORD": "",
  "REDIS_READ_TIMEOUT_SECOND": "1",
  "REDIS_WRITE_TIMEOUT_SECOND": "1",
  "REDIS_POOL_SIZE": "200",
  "REDIS_POOL_TIMEOUT_SECOND": "100",
  "REDIS_MIN_IDLE": "50",
  "REDIS_IDLE_TIMEOUT_SECOND": "100",
  "REDIS_IDLE_FREQUENCY_CHECK": "1",
  "REDIS_READ_ONLY": "false",
  "REDIS_ROUTE_BY_LATENCY": "true",
  "REDIS_ROUTE_RANDOMLY": "false",
  "REDIS_MAX_REDIRECT": "3",
  "REDIS_CLUSTER_MODE": "false",
  "REDIS_TLS_ENABLE": "false",
  "REDIS_INSECURE_SKIP_VERIFY": "true",

  "PUBSUB_ACCOUNT_PATH": "config/credential_account_service.json",
  "PUBSUB_PROJECT_ID": "",
  "PUBSUB_PROJECT_NAME": "",
  "PUBSUB_TOPIC": "",
  "PUBSUB_SUBSCRIPTION_TOPIC": "",
  "PUBSUB_RETRY_ATTEMPT_SUBSCRIPTION": "10",
  "PUBSUB_RETRY_DELAY_SUBSCRIPTION": "30",

  "FIRESTORE_ACCOUNT_PATH": "config/credential_account_service.json",
  "FIRESTORE_PROJECT_ID": "",
  "FIRESTORE_PROJECT_NAME": "",
  "FIRESTORE_ROOT_COLLECTION_ID": "",
  "FIRESTORE_ROOT_DOCUMENT_ID": ""
}
```

## Required Config

```yaml
app:
  name: ${APP_NAME}
  port: ${APP_PORT}
  grpc_port: ${APP_GRPC_PORT}
  timezone: ${APP_TIMEZONE}
  debug: ${APP_DEBUG}
  env: ${APP_ENV} # dev | stg | prod
  read_timeout_second: ${APP_READ_TIMEOUT_SECOND}
  write_timeout_second: ${APP_WRITE_TIMEOUT_SECOND}
  key: "${APP_KEY}"
  default_lang: "${APP_DEFAULT_LANG}"

logger:
  name: "${LOGGER_NAME}" # service name
  level: "${LOGGER_LEVEL}" # trace | debug | info | warn | error | fatal | panic

apm:
  address: "${APM_ADDRESS}"
  enable: ${APM_ENABLE}
  name: ${APM_NAME}


redis:
  host: ${REDIS_HOST}
  db: ${REDIS_DB}
  password: ${REDIS_PASSWORD}
  read_timeout_second: ${REDIS_READ_TIMEOUT_SECOND}
  write_timeout_second: ${REDIS_WRITE_TIMEOUT_SECOND}
  pool_size: ${REDIS_POOL_SIZE}
  pool_timeout_second: ${REDIS_POOL_TIMEOUT_SECOND}
  min_idle_conn: ${REDIS_MIN_IDLE}
  idle_timeout_second: ${REDIS_IDLE_TIMEOUT_SECOND}
  route_by_latency: ${REDIS_ROUTE_BY_LATENCY}
  idle_frequency_check: ${REDIS_IDLE_FREQUENCY_CHECK}
  read_only: ${REDIS_READ_ONLY}
  route_randomly: ${REDIS_ROUTE_RANDOMLY}
  max_redirect: ${REDIS_MAX_REDIRECT}
  cluster_mode: ${REDIS_CLUSTER_MODE}
  tls_enable: ${REDIS_TLS_ENABLE}
  insecure_skip_verify: ${REDIS_INSECURE_SKIP_VERIFY} # if tls_enable == true, this config use for tls insecure_skip_verify true or false

pubsub:
  account_path: "${PUBSUB_ACCOUNT_PATH}"
  project_id: "${PUBSUB_PROJECT_ID}"
  project_name: "${PUBSUB_PROJECT_NAME}"
  topic: "${PUBSUB_TOPIC}"
  subscription_topic: "${PUBSUB_SUBSCRIPTION_TOPIC}"
  retry_attempt_sub: "${PUBSUB_RETRY_ATTEMPT_SUBSCRIPTION}"
  retry_delay_sub: "${PUBSUB_RETRY_DELAY_SUBSCRIPTION}" # seconds

firestore:
  account_path: "${FIRESTORE_ACCOUNT_PATH}"
  project_id: "${FIRESTORE_PROJECT_ID}"
  project_name: "${FIRESTORE_PROJECT_NAME}"
  root_collection_id: "${FIRESTORE_ROOT_COLLECTION_ID}"
  root_document_id: "${FIRESTORE_ROOT_DOCUMENT_ID}"
```
