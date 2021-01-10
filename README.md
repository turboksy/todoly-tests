# Todo.ly API testing
_Author: Ksenia Vakhmenina_

# Project overview

The tests cover handling of main Todoly resources: `Users`, `Projects`, `Items`, and `Filters`. Postman collection is split on 4 folders, each for every resource. Each folder can be run separately and multiple times, as it creates new data every time. Every request has multiple tests to validate response. Requests in a folder are expected to run in given order.
Projects, Items, and Filters folders start with sing up and login as newly generated user. So they always deal with clean data and don't have collisions.

# How to run

## From Docker CLI

### Requirments
1. Docker
2. Git

### Steps
1. Clone repository
```bash
git clone https://github.com/turboksy/todoly-tests.git
```
2. Change directory
```
cd todoly-tests
```
3. To run all tests
```bash
docker run \
    -v $(pwd)/src:/etc/newman \
    -t postman/newman \
    run Todo.ly.postman_collection.json \
    --environment Todo.ly.postman_environment.json \
    --reporters junit,cli \
    --reporter-junit-export="newman-report.xml"
```
_Note: Test results are written to cli output. Report is generated in file `src/newman-report.xml`, it has jUnit format, so can be used in CI._
4. To run specific folder
```bash
docker run \
    -v $(pwd)/src:/etc/newman \
    -t postman/newman \
    run Todo.ly.postman_collection.json \
    --environment Todo.ly.postman_environment.json \
    --reporters junit,cli \
    --reporter-junit-export="newman-report.xml" \
    --folder "User API"
```


## From Postman

### Requirments:
1. Postman

### Steps:
1. Import collection from file `src/Todo.ly.postman_collection.json` to Postman
2. Import environment from file `src/Todo.ly.postman_environment.json` to Postman
3. Run collection

# Found bugs
