# container-structure-test-github-action
A simple wrapper over GoogleContainerTools container-structure-test https://github.com/GoogleContainerTools/container-structure-test

It accepts two inputs as described below.

dockerimage: the docker image you want ot test. You must pull or build the image in advance.

args: arguments for container-structure-test Tool.

How it's different then other Actions of similar nature:

1. Vanilla and simple wrapper.
2. Does not use docker as you may hit pull limit easily.
3. Gives you full control over arguments. You may use it as you wish.
4. You can run it over docker image tar as well.
5. Flexible reporting.

```yaml
jobs:
  test-image:
    runs-on: ubuntu-latest
    steps:  
      - name: checkout
        uses: actions/checkout@v4
      - name: Pull Docker Image
        run: docker pull gcr.io/google-appengine/python
      - name: "Run Tests"
        uses: amardeep2006/container-structure-test-github-action@v1
        with: 
         dockerimage: gcr.io/google-appengine/python
         args: --config tests/python_command_tests.yaml --config tests/python_file_tests.yaml
```

Here is another example 

```yaml
      - name: "Run Tests and Generate Junit xml reports"
        uses: ./
        with: 
         dockerimage: gcr.io/google-appengine/python
         args: --config tests/python_command_tests.yaml --config tests/python_file_tests.yaml --output junit --test-report junitreport.xml
```
