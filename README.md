# AEM 6.5 Search Experiments

This repository contains a collection of Search experiments in a take-home lab format. The content is intended for intermediate to advanced AEM developers and customizers.

## Goal

The goal of these experiments is to demonstrate the impact of search optimization and best practices adoption in Adobe Experience Manager (AEM), and provide a project for test driving its feature set.

## Non-Goals

This repo does not attempt to prescribe a one-size-fits-all solution to search optimization. Due to the myriad use cases that AEM supports, it would be impossible to do so. Instead, pick and choose concepts from the below experiments and try them out on your project.

## Getting set up

You will need the following SDKs, tools, and apps installed to work through the experiments:

- Java `11.0.*`
- [JMeter](https://jmeter.apache.org/)

You will also need a local AEM author setup:

- AEM 6.5 author instance running on `:4502`
    - Ideally, with the latest [Service Pack](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html) installed

# Experiments

## 1. `Performance gains of a Lucene property index`

[⇨ Performance gains of a Lucene property index](experiments/lucene-property-index)

## 2. `Performance gains of simple query refinement`

[⇨ Performance gains of a simple query refinement](experiments/query-refinement)



### Contributing

Contributions are welcomed! Read the [Contributing Guide](./.github/CONTRIBUTING.md) for more information.

### Licensing

This project is licensed under the Apache V2 License. See [LICENSE](LICENSE) for more information.