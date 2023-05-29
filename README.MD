Create docker user (-m create homecategory)
```
useradd -m -s /bin/bash username
```

Add user to docker group (in example docker) <- user (username)
```
usermod -aG docker username
```

Check which groups are exist created user -> Print out applyed groups
```
id username
```

Check if user can run docker

```
su - username
```
```
docker --version
```
