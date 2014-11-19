# Secure Mobile Development

At NowSecre we spend a lot of time attacking mobile apps. Hacking. Breaking encryption, finding flaws, pen testing and looking for sensitive data stored insecurely. We do it for the right reasons - to help companies make their apps more secure. This document represents some of the wisdom we share with our clients and partners. **We are driven to advance mobile security worldwide.**

## Using this Guide

This guide gives specific recommendations to use during your development process. The descriptions of attacks and security recommendations in this report are not exhaustive or perfect, but you will get practical advice that you can use to make your app(s) more secure.

To learn about all the vectors that attackers might use on your app, read our [Mobile Security Primer][1].

This guide is ultimately published [here][4] as changes are accepted into the main repository.

### Technology Stack

Jekyll is the main driving force behind creating the website that gets publish, but to keep things simple, we've opted to keep this repository just about the content. During publishing this repository is pulled into another to generate the output. Because of this behavior, there are a few nuances that have to be observed when submitting changes, these are outlined below in the contributing section.

## Contributing

We welcome everyone who wants to contribute to this repository to do so.

We reserve the right to release updated recommendations. If you have questions or feedback please [let us know][2].

### Instructions

First fork this repository, make your changes and submit them back to this repository as a Pull Request. If you are unfamiliar with this process, please read the [GitHub User Documentation][3].

#### Adding a Best Practice

To add a new best practice, you should first identify which category it should belong under. Then create your markdown file using the following file format: `YYYY-MM-DD-title-of-the-best-practice.md`. The `YYYY-MM-DD` ultimately does not matter, because we are using Jekyll's post mechanism, it expects it to be in the file name. Use the `template.md` as a start to the best practice and change the details where needed.

<!-- Links -->
[1]: https://www.nowsecure.com/resources/secure-development/primer/ "Mobile Security Primer"
[2]: https://viaforensics.com/company/contact/ "Contact Us"
[3]: https://help.github.com/articles/creating-a-pull-request/ "Creating a Pull Request"
[4]: https://www.nowsecure.com/resources/secure-development/ "Secure Mobile Development"
