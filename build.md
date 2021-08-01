# Build Notes

```
docker buildx build --build-arg BRANCH=main --push --platform linux/arm64,linux/amd64 --tag lryanuk/chaingreen-docker:latest .
```