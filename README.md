# BOSH Release for cf-mysql-java-broker

## Usage

To use this bosh release, first upload it to your bosh:

```
bosh target BOSH_HOST
git clone https://github.com/cloudfoundry-community/cf-mysql-java-broker-boshrelease.git
cd cf-mysql-java-broker-boshrelease
git submodule update --init
bosh upload release releases/cf-mysql-java-broker-1.yml
```

For [bosh-lite](https://github.com/cloudfoundry/bosh-lite), you can quickly create a deployment manifest:

```
cp examples/bosh-lite-cluster.yml local-cluster.yml
sed -i '' -e "s/DIRECTOR_UUID/$(bosh status | grep UUID | awk '{print $2}')/" local-cluster.yml
bosh deployment local-cluster.yml
bosh -n deploy
```

Register the broker with cf
```
cf add-service-broker --name jmysql-service --username cc --password secret --url http://10.244.0.18

gcf create-service-broker jmysql-service cc secret http://10.244.0.14
```

Create Service
```
cf create-service
```

Bind Service

