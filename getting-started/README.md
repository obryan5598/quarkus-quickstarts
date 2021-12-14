### Compile binary native executable skipping tests
> mvn package -Pnative -DskipTests

### Build image with Buildah using distroless base image
> buildah build-using-dockerfile -f /<your-path>/quarkus-quickstarts/getting-started/src/main/docker/Dockerfile.native-distroless -t getting-started-native:1.0.0 .

### Push image to public Quay repository
> buildah login -u <your-quay-user> -p <your-quay-pwd> quay.io
> buildah push <image-id> docker://quay.io/<your-user>/getting-started-native:1.0.0

### Discover you private cluster registry
> oc registry info
> $ default-route-openshift-image-registry.<openshift-cluster>.com

### Copy image from Quay to private Openshift repository
> skopeo copy --src-creds <your-quay-user>:<your-quay-pwd> --dest-creds kubetcl:$(oc whoami -t) docker://quay.io/<your-user>/getting-started-native:1.0.0 docker://default-route-openshift-image-registry.<openshift-cluster>.com/<ocp-project>/getting-started-native:1.0.0

### Enable pulling permissions
> oc policy add-role-to-user system:image-puller system:serviceaccount:gastarit-quarkus-rest-on-ocp:getting-started-native --namespace=default

### Run the application
> curl -k -v http://<your-openshift-cluster>.<ocp-project>/hello

### More details
For more details look at the README-original.md file
