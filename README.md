# JMeter Performance Testing Project

This repository contains JMeter performance tests for JSON-based API testing. The project includes automated test execution through GitHub Actions, with options to run tests either directly or using Docker containers.

## Project Structure

```
jmeter/
├── UI_Script.jmx   # Main JMeter test plan
├── jsonproject.csv     # Test data file
└── .github/
    └── workflows/
        ├── jmeter-test.yml        # Direct JMeter execution workflow
        └── jmeter-docker-test.yml # Docker-based execution workflow
```

## Test Plan Details

The test plan (`json-project.jmx`) is configured to perform API testing with the following features:
- JSON-based request/response handling
- Data-driven testing using CSV files
- Performance metrics collection
- Detailed HTML reporting

## GitHub Actions Workflows

### 1. Direct JMeter Execution (`jmeter-test.yml`)
This workflow:
- Runs on Ubuntu latest
- Sets up JDK 11
- Installs Apache JMeter 5.6.2
- Executes tests and generates reports
- Artifacts: JTL results and HTML reports

To run:
1. Go to Actions tab
2. Select "JMeter Performance Test"
3. Click "Run workflow"

### 2. Docker-based Execution (`jmeter-docker-test.yml`)
This workflow:
- Uses the `justb4/jmeter:5.5` Docker image
- Provides isolated test environment
- Mounts test files and results directories
- Validates test results automatically
- Artifacts: JTL results and HTML reports

To run:
1. Go to Actions tab
2. Select "JMeter Docker Performance Test"
3. Click "Run workflow"

## Test Results

Both workflows generate:
- JTL files with detailed test results
- HTML reports with performance metrics
- Automatically uploaded artifacts

Test results are available in the Actions tab after each run. Failed tests will cause the workflow to fail, making it easy to identify issues.

## Local Execution

To run tests locally:

### Direct Execution:
```bash
jmeter -n -t API_Script.jmx -l test-results.jtl -e -o html-report
```

### Docker Execution:
```bash
docker run --rm -v "${PWD}:/jmeter" -w /jmeter justb4/jmeter:5.5 \
  -n -t json-project.jmx \
  -l jmeter/results/test-results.jtl \
  -e -o jmeter/reports/html-report
```

