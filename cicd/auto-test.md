You can kick off a CI/CD container like,

```
docker run \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v `pwd`:/workspace/ \
  -w=/workspace/ \
  drone/drone-runner-docker:1 exec drone.yml
```