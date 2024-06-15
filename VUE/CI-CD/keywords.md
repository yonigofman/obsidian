
| **Keyword**             | **Description**                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------ |
| `image`                 | Specifies the Docker image to use for the job.                                       |
| `services`              | Additional Docker images linked to the job's image.                                  |
| `stages`                | Defines the stages of the pipeline (e.g., build, test, deploy).                      |
| `before_script`         | Commands to run before each job's script.                                            |
| `after_script`          | Commands to run after each job's script, regardless of the outcome.                  |
| `variables`             | Define environment variables for the pipeline.                                       |
| `cache`                 | Cache directories between jobs to speed up subsequent pipeline runs.                 |
| `artifacts`             | Define files or directories to save after a job completes.                           |
| `only`                  | Specify conditions to limit when jobs run (e.g., branches, tags, variables).         |
| `except`                | Specify conditions to exclude when jobs run (opposite of `only`).                    |
| `rules`                 | More flexible and complex conditions for job execution.                              |
| `script`                | The main commands to execute for the job.                                            |
| `extends`               | Inherit configuration from another job defined in the same file.                     |
| `include`               | Include external YAML files in the configuration.                                    |
| `needs`                 | Specify jobs that need to complete before the current job runs.                      |
| `dependencies`          | Specify jobs whose artifacts are required for the current job.                       |
| `tags`                  | Define tags to run jobs on specific runners.                                         |
| `allow_failure`         | Allow the job to fail without impacting the pipeline status.                         |
| `when`                  | Specify when to run jobs (e.g., `on_success`, `on_failure`, `always`).               |
| `retry`                 | Specify how many times a job should be retried in case of failure.                   |
| `timeout`               | Set a time limit for job execution.                                                  |
| `parallel`              | Define parallel jobs with a matrix of variables.                                     |
| `trigger`               | Trigger another pipeline from the current pipeline.                                  |
| `coverage`              | Define how to extract test coverage data from the job output.                        |
| `interruptible`         | Define if a job can be canceled when a new pipeline starts before the job completes. |
| `resource_group`        | Limit concurrency for jobs using the same resource group.                            |
| `rules:changes`         | Trigger jobs based on file changes in the repository.                                |
| `environment`           | Define environments for deployment (e.g., `name`, `url`, `on_stop`).                 |
| `release`               | Create releases in GitLab (e.g., `tag_name`, `description`).                         |
| `pages`                 | Configure GitLab Pages deployments.                                                  |
| `secrets`               | Define secrets to be used in jobs.                                                   |
| `inherited`             | Determine if the job inherits variables from the pipeline.                           |
| `before_script`         | Commands to run before each job's script.                                            |
| `after_script`          | Commands to run after each job's script, regardless of the outcome.                  |
| `include`               | Include external YAML files in the configuration.                                    |
| `extends`               | Inherit configuration from another job defined in the same file.                     |
| `interruptible`         | Define if a job can be canceled when a new pipeline starts before the job completes. |
| `needs`                 | Specify jobs that need to complete before the current job runs.                      |
| `environment`           | Define environments for deployment (e.g., `name`, `url`, `on_stop`).                 |
| `resource_group`        | Limit concurrency for jobs using the same resource group.                            |
| `rules:exists`          | Trigger jobs based on the existence of files.                                        |
| `cache:policy`          | Specify the caching policy (e.g., `pull-push`, `push`, `pull`).                      |
| `artifacts:reports`     | Define report types generated by jobs (e.g., `junit`, `codequality`).                |
| `script:before`         | Commands to run before the main script.                                              |
| `script:after`          | Commands to run after the main script.                                               |
| `trigger:strategy`      | Define the strategy for triggering child pipelines (`depend` or `mirror`).           |
| `schedule`              | Define scheduled pipelines with cron syntax.                                         |
| `rules:variables`       | Trigger jobs based on CI variables.                                                  |
| `variables:description` | Describe the purpose of a variable.                                                  |
| `dependencies:job`      | Specify the job whose artifacts are required.                                        |
| `variables:masked`      | Mask the variable in job logs.                                                       |
| `timeout:strategy`      | Define the strategy for job timeouts.                                                |
| `environment:on_stop`   | Define a job that stops the environment.                                             |
| `release:assets`        | Define assets to be attached to a release.                                           |
| `pages:artifacts`       | Define artifacts to be used for GitLab Pages.                                        |
| `cache:key`             | Specify the key for caching.                                                         |
| `artifacts:paths`       | Define paths to be included in the artifacts.                                        |
| `trigger:project`       | Specify the project to trigger.                                                      |
| `release:description`   | Describe the release.                                                                |
| `rules:if`              | Conditional rules to determine if the job should run.                                |
