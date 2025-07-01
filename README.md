# docker-gs-ping

A simple Go server/microservice example for [Docker's Go Language Guide](https://docs.docker.com/language/golang/).

Notable features:

* Includes a [multi-stage `Dockerfile`](https://github.com/olliefr/docker-gs-ping/blob/main/Dockerfile.multistage).
* Has a CI pipeline using GitHub Actions to run tests.
* Has a CD pipeline using GitHub Actions to publish to Docker Hub.

## Want _moar_?!

There is a more advanced example in [olliefr/docker-gs-ping-roach](https://github.com/olliefr/docker-gs-ping-roach) using [CockroachDB](https://github.com/cockroachdb/cockroach).

## Contributing

This was written for an _introduction_ section of the Docker tutorial and as such it favours brevity and pedagogical clarity over robustness. 

Thus, feedback is welcome, but please no nits or pedantry. Ain't nobody got time for that 🙃

## License

[Apache-2.0 License](LICENSE)

## Use on Mac M1:


### w/manual build of the image

#### Quay part
* login to quay-its.epfl.ch
* create new repository for svc0166
* create (e.g. `mm-docker-gs-ping`)
* ensure the access to the repo for robots accounts:
    * pull in `svc0166+pull_only`
    * pull/push for ` svc0166+pull_push`


#### docker (image build and push) part:
```shell
docker login quay-its.epfl.ch -u macowicz
```

Force to build for amd64 architecture (use buildx + --platform=... in Dockerfile stages)
 ```shell
docker buildx build --platform linux/amd64 -t quay-its.epfl.ch/svc0166/mm-docker-gs-ping:latest  .
docker push quay-its.epfl.ch/svc0166/mm-docker-gs-ping:latest
```

#### OC part

1. Create the OC project `svc0166t-mm-docker-gs-ping` (via XaaS portal K8s namespace)
2. Create secrets `pull-only` from quay robot account `svc0166+pull_only`
3. Create the app `mm-docker-gs-ping-app` from container repository.

Check if it worked:
```shell
oc port-forward services/mm-docker-gs-ping 8087:8080
```



