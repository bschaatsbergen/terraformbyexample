# Terraform by Example

Repository for [Terraform by Example](https://terraformbyexample.com)

### Overview

Terraform by Example is a introduction to Terraform using example configuration files to manage resources in Google Cloud, Amazon Web Services, etc.

### Building

To build the site you'll need Go and Hugo installed. Run:

```console
$ hugo server -D
```

To see the site locally:

open `http://127.0.0.1:1313/` in your browser.

### Publishing

To publish a new version of the site we simply push a tag to the remote repository.

```console
$ git push origin <tag_name>
```

The [release](.github/workflows/release.yaml) workflow will publish the new version of the site to S3 and invalidate the CloudFront distribution.

### Inspiration

This project is inspired by [Go by Example](https://github.com/mmcgrana/gobyexample).

### FAQ

#### The examples are not working; what do I do?

Feel free to [open an issue](https://github.com/bschaatsbergen/terraformbyexample/issues) and we'll happily help you out.