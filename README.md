# Simple Low Latency Streaming Platform

## Features
* Sub-second average end-to-end continent-wide latency, under 2 seconds worlwide
* Royalty free solution - based on freeware [Nimble Streamer](https://wmspanel.com/nimble)
* SRT ingest - broadcast with any SRT capable broadcaster, including freeware OBS and Larix Broadcaster
* SLDP egress - plays in any [MSE capable browser](https://caniuse.com/?search=mse)

## Setup

### Deploying the architecture
1. Sign in to the [AWS Management Console](https://aws.amazon.com/console)
2. Switch to the [AWS region](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-available-regions) that is closest to your broadcast location
3. Click the button below to launch the CloudFormation template. Alternatively you can [download](template.yaml) the template and adjust it to your needs.

[![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?stackName=simple-low-latency-streaming-platform&templateURL=https://lostshadow.s3.amazonaws.com/simple-low-latency-streaming-platform/template.yaml)

4. Choose the instance type for your server; make your choice depending on how much you will need to stream (use figures [here](https://cloudonaut.io/ec2-network-performance-cheat-sheet/) as reference); you will be able to change the instance size later, or just discard the stack and create a new one with a different setup
5. Leave all other settings to default
6. Hit the `Create Stack` button. 
7. Wait for the `Status` to become `CREATE_COMPLETE`. Note that this may take **1-2 minutes** or more.
8. Under `Outputs`, notice the keys named `IngressEndpoint` and `EgressEndpoint`; write these down for using later


### Testing your setup
1. Point your SRT encoder to the `srt://...` address output by CloudFormation above as `IngressEndpoint`
2. Open the SLDP test player [here](http://player.wmspanel.com/#player=sldp) and set it up with the URI output by CloudFormation above as `EgressEndpoint`


### Integration

For browser playback, you'll have to set up and integrate the free SLDP player [here](https://softvelum.com/player/web)

To integrate with mobile apps you can make use of the commercial SDK [here](https://softvelum.com/mobile/buy)

## Notes
* Setup only uses a single stream, namely `stream1`; you will have to alter the template if you need to broadcast more streams simultaneously or if you want to name them differently
* The CloudFormation template creates a VPC with the internal IP range `10.129.0.0/16`; be sure to change this if it overlaps with other VPCs