# Gitlab Runner Service Example
This project shows how to use [gitlab-runner-action](https://github.com/edersonbrilhante/gitlab-runner-action) in a [github workflow](https://github.com/edersonbrilhante/gitlab-runner-service-example/blob/main/.github/workflows/gitlab-runner.yaml) triggered in a gitlab-job [gitlabci](https://gitlab.com/edersonbrilhante/gitlab-runner-service-example/-/blob/main/.gitlab-ci.yml#L14)


### Triggering a github workflow from a gitlab-ci job
```
start-crosscicd:
  image: alpine
  before_script:
    - apk add --update curl && rm -rf /var/cache/apk/*
  script: |
      curl -H "Authorization: token ${GITHUB_TOKEN}" \
      -H 'Accept: application/vnd.github.everest-preview+json' \
      "https://api.github.com/repos/${GITHUB_REPO}/dispatches" \
      -d '{"event_type": "gitlab_trigger_'${CI_PIPELINE_ID}'", "client_payload": {"registration_token": "'${GITLAB_REGISTRATION_TOKEN}'"}}'
```