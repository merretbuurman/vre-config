FROM python:3.6.12-slim-buster

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install vim wget git

# Dependencies for script:
RUN pip3 install requests docker

# Health check:
COPY ./healthcheck.sh ./
RUN echo "STARTING..." > ishealthy.txt
HEALTHCHECK --interval=10s --timeout=2s --retries=5 CMD ./healthcheck.sh

COPY ./container-deletion-not-interactive.py ./
CMD ["python3", "container-deletion-not-interactive.py"]

# docker build -t container_deletion:20201019 .
# docker tag container_deletion:20201019 registry-sdc.argo.grnet.gr/container_deletion:20201019
# docker push registry-sdc.argo.grnet.gr/container_deletion:20201019

# Run without user login check (NOT RECOMMENDED):
# docker run --name dele --mount type=bind,source="/var/run/docker.sock",target="/var/run/docker.sock" --env EVERY=2 --env PROTECTED_USERNAMES="kingkong" --env PROTECTED_CONTAINERS="bla-protected;bli-protected" --env PREFIX="bla;bli" --env NO_CHECK=true container_deletion:20201019

# Run with user login check (RECOMMENDED):
# docker run --name dele --mount type=bind,source="/var/run/docker.sock",target="/var/run/docker.sock" --env EVERY=2 --env PROTECTED_USERNAMES="kingkong" --env PROTECTED_CONTAINERS="bla-protected;bli-protected" --env PREFIX="bla;bli" --env NUM_DAYS=200 --env API_URL=https://vre.seadatanet.org/getuserauthinfo --env API_PASSWORD=k8T5gh5D container_deletion:20201019

