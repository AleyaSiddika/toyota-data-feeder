# Step by step commands for the whole implementation of my assignment:

For my Exercise 1 Docker Basics, I have gone through building and running the Toyota Data Feeder Docker container and using `mosquitto_sub` to confirm message reception.

**Build Docker Image**

```bash
docker build -t toyota_data_feeder:1.0 .
```

**Tag the Docker image:**

```bash
docker tag toyota_data_feeder:1.0 aleyasiddika/toyota_data_feeder:1.0
```

**Login to Docker Hub:**

```bash
docker login
```

**Push the Docker image to Docker Hub:**

```bash
docker push aleyasiddika/toyota_data_feeder:1.0
```

**Run Docker Container**

```bash
docker run -e MQTT_URL=mqtt-test.rahtiapp.fi -e MQTT_PORT=443 -e CLIENT_ID=asiddika toyota_data_feeder:1.0
```

This command runs the Docker container, setting environment variables for MQTT connection (`MQTT_URL`, `MQTT_PORT`, `CLIENT_ID`).

**Confirm Message Reception**

```bash
mosquitto_sub -h mqtt-test.rahtiapp.fi -p 443 -t "asiddika/toyota/#" --verbose --insecure --cafile ca.crt
```

Use `mosquitto_sub` to subscribe to MQTT topics and confirm message reception. Adjust the parameters as needed.

**View Running Containers**

```bash
docker ps
```

This command lists all running Docker containers, providing container information.

**List Files in Running Container**

```bash
docker exec -it <container_name_or_id> ls /app
```

---

---

### Pushing an image to the CSC Rahti registry involves a few steps. Here's a general guide:

**Login to Rahti Registry:**

**Build Docker Image:**

```bash
oc new-build --name=toyota_data_feeder --binary=true -l app=toyota_data_feeder
oc start-build toyota_data_feeder --from-dir=. --follow
```

**Tag the Docker Image:**

```bash
oc tag toyota_data_feeder:1.0 rahti.csc.fi/csc_project/toyota_data_feeder:1.0
```

**Push the Docker Image to Rahti Registry:**

```bash
oc import-image csc_project/toyota_data_feeder:1.0 --from=toyota_data_feeder:1.0 --confirm
```

---

## or,

**Login to Rahti Registry:**

**Build Docker Image:**

```bash
oc build -t rahti.csc.fi/csc_project/toyota_data_feeder:1.0 .
```

**Tag the Docker Image:**

Tag the Docker image with the Rahti Registry URL:

```bash
oc tag rahti.csc.fi/csc_project/toyota_data_feeder:1.0 rahti.csc.fi/csc_project/toyota_data_feeder:1.0
```

**Push the Docker Image to Rahti Registry:**

Push the Docker image to the Rahti Registry:

```bash
oc push rahti.csc.fi/csc_project/toyota_data_feeder:1.0
```