![](https://img.shields.io/github/package-json/v/kaskadi/template-kaskadi-api)
![](https://img.shields.io/badge/code--style-standard-blue)
![](https://img.shields.io/github/license/kaskadi/template-kaskadi-api?color=blue)

**GitHub Actions workflows status**

[![](https://img.shields.io/github/workflow/status/kaskadi/template-kaskadi-api/deploy?label=deployed&logo=Amazon%20AWS)](https://github.com/kaskadi/template-kaskadi-api/actions?query=workflow%3Adeploy)
[![](https://img.shields.io/github/workflow/status/kaskadi/template-kaskadi-api/build?label=build&logo=mocha)](https://github.com/kaskadi/template-kaskadi-api/actions?query=workflow%3Abuild)
[![](https://img.shields.io/github/workflow/status/kaskadi/template-kaskadi-api/syntax-check?label=syntax-check&logo=serverless)](https://github.com/kaskadi/template-kaskadi-api/actions?query=workflow%3Asyntax-check)

**CodeClimate**

[![](https://img.shields.io/codeclimate/maintainability/kaskadi/template-kaskadi-api?label=maintainability&logo=Code%20Climate)](https://codeclimate.com/github/kaskadi/template-kaskadi-api)
[![](https://img.shields.io/codeclimate/tech-debt/kaskadi/template-kaskadi-api?label=technical%20debt&logo=Code%20Climate)](https://codeclimate.com/github/kaskadi/template-kaskadi-api)
[![](https://img.shields.io/codeclimate/coverage/kaskadi/template-kaskadi-api?label=test%20coverage&logo=Code%20Climate)](https://codeclimate.com/github/kaskadi/template-kaskadi-api)

**LGTM**

[![](https://img.shields.io/lgtm/grade/javascript/github/kaskadi/template-kaskadi-api?label=code%20quality&logo=LGTM)](https://lgtm.com/projects/g/kaskadi/template-kaskadi-api/?mode=list&logo=LGTM)

<!-- You can add badges inside of this section if you'd like -->

****

# Testing

`mocha`, `chai`, `nyc`, `serverless-offline` & `standard` are available as dev dependencies.

A `build` workflow (see [here](./.github/workflows/build.yml)) is running on `pull request` and will execute your test suite before allowing you to merge your PR. It also has a `coverage` job already prepared that you can comment out as soon as your testing is in place and your `REPORTER_ID` is in the repository secrets. This is the ID on _Code Climate_ used for uploading code coverage reports.

Along `build`, a `syntax-check` workflow will also run to check your `serverless.yml` file syntax.

****

# Documentation

This repository comes with a `generate-docs` job inside of the `deploy` workflow that generates documentation automatically for you by reading your main `serverless.yml` configuration file and extracting meta data of all endpoints you defined. See [here](https://github.com/kaskadi/action-generate-docs) for more information.

If you would like to see the workflow configuration, head [here](./.github/workflows/deploy.yml).

You can configure the template used to generate the action documentation [here](./docs/template.md).

****

# Deploying

Deploying to AWS is done automatically via a `deploy` workflow (see [here](./.github/workflows/deploy.yml)). This workflow will run on `push` to `master`. Before publishing, it checks for syntax error in your `serverless.yml` file.

**You'll have to switch the command from `--version` to `deploy -v` in the [workflow configuration file](./.github/workflows/deploy.yml) to actually deploy!**

**Warning: you may need to manually deploy the first time via `Serverless` CLI locally.**

****

# Tools

## Add new endpoints

In order to add new endpoints:
1. Go to the root of your API repository
2. Run `npm run add-lambda <lambda_name> <http_method> <path/to/your/lambda>`
3. Your endpoint is now located under `lambdas/<lambda_name>` and you can start developing!

## Upgrade API version

To update your API version, run `npm run upgrade-version <version_option>`. This takes the same argument as `npm version` (see [here](https://docs.npmjs.com/cli/version)). It will update for you the main `package.json` as well as `serverless.json` but also all `package.json` for all endpoints.

****

# Using custom domain for your API

_For all custom domains you will need a certificate for this domain. Please make sure that you have the proper certificate generated, else create one associated with your domain. All this can be done [here](https://console.aws.amazon.com/acm/home?region=us-east-1#/)_

**Case 1: creating a new custom domain for API**

If the custom domain you wish to use hasn't been created yet (list of custom domains [here](https://eu-central-1.console.aws.amazon.com/apigateway/home?region=eu-central-1#/custom-domain-names)).

1. Go [here](https://eu-central-1.console.aws.amazon.com/apigateway/home?region=eu-central-1#/custom-domain-names) and click on _Create Custom Domain Name_
2. Configure your domain as you wish to
3. Once the domain is created and initialized, go to [Route 53](https://console.aws.amazon.com/route53/home?region=eu-central-1)
4. Go into the _Hosted Zone_ for the domain you wish to use and create a new _A Record_.
5. For this record, you should toggle the _Alias_ option, give for _name_ the custom domain name you wish to use and select for _Alias target_ the API you want to map to this domain. You may need to copy paste the base URL to that API to make this work

**Case 2: using an existing custom domain**

1. Go [here](https://eu-central-1.console.aws.amazon.com/apigateway/home?region=eu-central-1#/custom-domain-names)
2. Click on _Edit_ for the custom domain you wish to use
3. Add a base path you wish to map your API to for this domain and then select the API & its stage in the dropdown menus

**Attention:** you can only use an existing custom domain if this domain doesn't have already an empty path as base path.

****

<!-- automatically generated documentation will be placed in here -->
{{>main}}
<!-- automatically generated documentation will be placed in here -->

<!-- You can customize this template as you'd like! -->