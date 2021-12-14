# Quarkus Getting-Started example

## Add the configmap to the cluster
> oc create -f /your-path/basic-configmap.yaml

## Building the image & Deploying to Openshift via S2Image

### Compile binary native executable skipping tests
> mvn package -Pnative -DskipTests

### Otherwise compile JVM executable skipping tests
> mvn package -DskipTests

## Run the application
> curl -k -v http://your-openshift-cluster.ocp-project/hello

## More details
For more details look at the README-original.md file
