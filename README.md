name: Docker Image Pull, Tag, and Push

on: [push]

jobs:
  docker:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Pull Docker image
      run: docker pull langgenius/dify-api:0.8.3

    - name: Tag Docker image
      run: docker tag langgenius/dify-api:0.8.3 registry.cn-zhangjiakou.aliyuncs.com/uchonor/dify-api:0.8.3

    - name: Log in to Docker registry
      run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin registry.cn-zhangjiakou.aliyuncs.com

    - name: Push Docker image
      run: docker push registry.cn-zhangjiakou.aliyuncs.com/uchonor/dify-api:0.8.3
