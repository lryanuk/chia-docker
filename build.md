# Build Notes

```
docker buildx build --build-arg BRANCH=master --push --platform linux/arm64,linux/amd64 --tag lryanuk/spare-docker:latest .
```