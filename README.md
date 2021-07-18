<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/sns-secure-cli/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# sns-secure CLI tool and library

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

The sns-secure tool can be used to harden your sns topic security posture. The tool is useful if you have a lot of topics to update. It supports:

* list topics and their encryption status
* enabling encryption
* disabling encryption

It is used as part of the Security Controls blueprint:

* [Security Controls](https://github.com/boltopspro-docs/security-controls): Continuously applies the security-group remedation as well as other remeidations. IE: S3 Buckets, SNS topics, etc.


## Usage

    sns-secure encrypt TOPIC_ARN # default AWS managed SNS KMS key
    sns-secure encrypt TOPIC_ARN --kms-key xxx # CMK key
    sns-secure unencrypt TOPIC_ARN
    sns-secure show TOPIC_ARN
    sns-secure list

## Examples with Output

    $ sns-secure list
    +----------------------------------------------------------------------------+------------+
    |                                   Topic                                    | Encrypted? |
    +----------------------------------------------------------------------------+------------+
    | arn:aws:sns:us-west-2:112233445566:hello-topic                             | false      |
    | arn:aws:sns:us-west-2:112233445566:security-controls-SnsTopic-EN5U8KM3PGWV | true       |
    +----------------------------------------------------------------------------+------------+
    $ sns-secure encrypt arn:aws:sns:us-west-2:112233445566:security-controls-SnsTopic-EN5U8KM3PGWV
    The SNS topic is now encrypted with key: alias/aws/sns
    $

## Batch Commands

There are some supported batch commands:

    s3-secure batch encrypt FILE.txt
    s3-secure batch encrypt FILE.txt --kms-key xxx # the --kms-key option MUST come at the end
    s3-secure batch unencrypt FILE.txt

The format of FILE.txt is a list of SNS topic ARNs separated by newlines.  Example:

topics.txt:

    arn:aws:sns:us-west-2:112233445566:hello-topic
    arn:aws:sns:us-west-2:112233445566:security-controls-SnsTopic-EN5U8KM3PGWV

## Installation

Install with:

    git clone git@github.com:boltopspro/sns-secure-cli
    bundle
    rake install
