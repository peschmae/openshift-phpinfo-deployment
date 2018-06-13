# PHPInfo in a minishift/openshift cluster

## Deploy to minishift
### Start minishift (if not already running)
```
minishift start
```

### Login to minishift registry
```
eval $(minishift docker-env)
docker login -u developer -p $(oc whoami -t) $(minishift openshift registry)
```

### Build image
```
git clone https://github.com/peschmae/openshift-apache-php7.git
cd openshift-apache-php7
docker build . -t openshift-phpinfo
```

### Properly tag image and push to registry
```
docker tag openshift-phpinfo $(minishift openshift registry)/myproject/phpinfo
docker push $(minishift openshift registry)/myproject/phpinfo
```

### Apply openshift config
```
# if still in `openshift-apache-php7` directory
cd ../
oc apply -f phpinfo.yml
```
