# sqsmv

Move all messages from one SQS queue, to another.


## Installation

### Source

    go get github.com/cadams8238/sqsmv


## Configuration

The `AWS_SECRET_ACCESS_KEY` + `AWS_ACCESS_KEY_ID` -OR- `AWS_PROFILE`, and `AWS_REGION`
environment variables must be set.


## Usage

Supply source and destination URL endpoints.

    sqsmv -src https://region.queue.amazonaws.com/123/queue-a -dest https://region.queue.amazonaws.com/123/queue-b

To run jobs in parallel, use -clients parameter:

    sqsmv -src https://region.queue.amazonaws.com/123/queue-a -dest https://region.queue.amazonaws.com/123/queue-b -clients 8

To use AWS multifactor authentication, use the -mfa flag like so:
    sqsmv -src https://region.queue.amazonaws.com/123/queue-a -dest https://region.queue.amazonaws.com/123/queue-b -mfa

    Make sure you have the mfa_serial added to your AWS profile configuration before running. For more information, see the
    documentation here: https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-role.html#cli-configure-role-mfa

    NOTE: This MFA flag only supports MFA with a token provider (such as Google Authenticator, Duo, etc)

## Seeing is believing :)

Create some SQS messages to play with using the AWS CLI.

    for i in {0..24..1}; do
        aws sqs send-message \
            --queue-url https://ap-southeast-2.queue.amazonaws.com/123/wat-a
            --message-body "{\"id\": $i}"
    done


## License

The MIT License (MIT)

Copyright (c) 2016-2018 Scott Barr

See [LICENSE.md](LICENSE.md)
