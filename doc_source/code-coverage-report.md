# Code coverage reports<a name="code-coverage-report"></a>

## <a name="code-coverage-desc-section"></a>

CodeBuild allows you to generate code coverage reports for your tests\. The following code coverage reports are provided:

Line coverage  
Line coverage measures how many statements your tests cover\. A statement is a single instruction, not including comments or conditionals\.  
`line coverage = (total lines covered)/(total number of lines)`

Branch coverage  
Branch coverage measures how many branches your tests cover out of every possible branch of a control structure, such as an `if` or `case` statement\.  
`branch coverage = (total branches covered)/(total number of branches)`

The following code coverage report file formats are supported:
+ JaCoCo XML
+ SimpleCov JSON
+ Clover XML
+ Cobertura XML

## Create a code coverage report<a name="code-coverage-report-create"></a>

To create a code coverage report, you run a build project that is configured with at least one code coverage report group in its buildspec file\. AWS CodeBuild will interpret the code coverage results and provide a code coverage report for the run\. A new test report is generated for each subsequent build that uses the same buildspec file\. 

**To create a test report**

1. Create a build project\. For information, see [Create a build project in AWS CodeBuild](create-project.md)\.

1. Configure the buildspec file of your project with test report information:

   1. Add a `reports:` section and specify the name for your report group\. AWS CodeBuild creates a report group for you using your project name and the name you specified in the format `project-name`\-`report-group-name-in-buildspec`\. If you already have a report group you want to use, specify its ARN\. If you use the name instead of the ARN, AWS CodeBuild creates a new report group\. For more information, see [Reports syntax in the buildspec file](build-spec-ref.md#reports-buildspec-file)\. 

   1. Under the report group, specify the location of the files that contain the code coverage results\. If you use more than one report group, specify result file locations for each report group\. A new code coverage report is created each time your build project runs\. For more information, see [Specify test files](report-group-test-cases.md)\.

      This is an example that generates a code coverage report for a JaCoCo XML results file located in test\-`results/jacoco-coverage-report.xml`\.

      ```
      reports:
        jacoco-report:
          files:
            - 'test-results/jacoco-coverage-report.xml'
          file-format: 'JaCoCoXml'
      ```

   1. In the `commands` section of the `build` or `post_build` sequence, specify the commands that run the code coverage analysis\. For more information, see [ Specify test commands ](report-group-test-case-commands.md)\. 

1. Run a build of the build project\. For more information, see [Run a build in AWS CodeBuild](run-build.md)\.

1. When the build is complete, choose the new build run from **Build history** on your project page\. Choose **Reports** to view the code coverage report\. For more information, see [View test reports for a build](test-view-reports.md#test-view-project-reports)\.