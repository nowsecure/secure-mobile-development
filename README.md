# Secure Mobile Development

At NowSecure we spend a lot of time attacking mobile apps. Hacking. Breaking encryption, finding flaws, pen testing and looking for sensitive data stored insecurely. We do it for the right reasons - to help developers make their apps more secure. This document represents some of the knowledge we share with our clients and partners. **We are driven to advance mobile security worldwide.**

## Using this Guide

This guide gives specific recommendations to use during your development process. The descriptions of attacks and security recommendations in this report are not exhaustive or perfect, but you will get practical advice that you can use to make your apps more secure.

To learn about all the vectors that attackers might use on your app, read our [Mobile Security Primer][1].

We revise and invite contributions, and the updated guide is published [here][2] as changes are accepted into the main repository. You can also [Download a PDF][3] version with free registration.

We publish this guide under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International [License][4].

### Technology Stack

[Jekyll][5] is the technology behind publishing the website, but to keep things simple we've opted to keep this repository focused on the content. During publishing this repository is pulled into another to generate the output. Because of this behavior, there are a few nuances that have to be observed when submitting changes, these are described in our [contributing][6] page.

## Contributing

We welcome contributions from knowledgeable developers and security professionals. All contributors must read our [Contributing][6] page and accept the terms in their Pull Requests. Please follow the template and format provided if you do contribute.

We will review contributions and periodically publish updated recommendations. If you have questions or feedback please [let us know][7].

### Instructions

First fork this repository, make your changes and submit them back to this repository as a Pull Request. If you are unfamiliar with this process, please read the [GitHub User Documentation][8].

#### Adding a Best Practice

To add a new best practice, you should first identify which category it should belong under. Then create your markdown file using the following file format: `YYYY-MM-DD-title-of-the-best-practice.md`. The `YYYY-MM-DD` ultimately does not matter, because we are using Jekyll's post mechanism, it expects it to be in the file name. Use the `template.md` as a start to the best practice and change the details where needed.

<!-- Links -->
[1]: https://www.nowsecure.com/resources/secure-mobile-development/primer/mobile-security/ "Mobile Security Primer"
[2]: https://www.nowsecure.com/resources/secure-mobile-development/ "Secure Mobile Development"
[3]: https://www.nowsecure.com/resources/downloads/secure-mobile-development/ "Secure Mobile Devlopment - Download a PDF"
[4]: LICENSE.md "License"
[5]: http://jekyllrb.com "Jekyll"
[6]: CONTRIBUTING.md "Contributing"
[7]: https://www.nowsecure.com/contact/ "Contact Us"
[8]: https://help.github.com/articles/creating-a-pull-request/ "Creating a Pull Request"
