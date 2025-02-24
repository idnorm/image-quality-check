# Docker compose

This folder holds the simplest version of deploying our solution using docker compose.

> Docker images expect x86 CPU architecture, or in docker terms `linux/amd64` platform, currently we do not support ARM or Apple silicon platforms.

This docker compose starts `3` services:
- `model-dl` - Download and prepare models for inference
- `serving` - Run ML model inference
- `iq` - Runs image quality check server

It is configurable using env vars. They can be provided using environment variables or setting them in the `.env` file.
The `.env` file is located in the same directory as `docker-compose.yml`.

The only value that you **MUST** specify is `IQ_LICENSE_KEY`, this must be set to the license key you acquired for our service.

Depending on your CPU architecture you might need to specify a different vale for `SERVING_TAG`. By default, we specify `-skylake`,
but if you are running on an older CPU you might need to specify `-haswell` or `-broadwell`.

## Running the services

To start the services, run the following command in the directory containing `docker-compose.yml`:

```bash
docker-compose up -d
```

To stop the services, run the following command in the directory containing `docker-compose.yml`:

```bash
docker-compose down
```

Once started, the solution endpoint will be available for your application integration at localhost on port `8005` (or whicherver port you specified in `.env` file).
You can inspect the logs using

```bash
docker compose logs iq -f
```

Once you see
```text
{"level":"info","time":"2025-02-24T12:58:19Z","message":"Serving grpc on port 8005"}
{"level":"info","time":"2025-02-24T12:58:19Z","message":"Serving gateway on port 8000"}
```

the service is ready to accept and process requests.

To test the service you can use helper script in the root of the repo `send-rest-request.sh`.

```bash
./send-rest-request.sh <path_to_image>
```
