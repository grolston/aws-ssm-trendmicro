# SSM Trend Micro Deep Security

Leveraging AWS SSM agent, Trend Micro can be installed on supported instances tagged correctly. The template supports running the association hourly and if the agent is already installed it will not attempt to clobber that installation.

## Prerequisites

The following details the prerequisites

| Requirement | Description | Support Link |
| ------------ | ----------- | ----------- |
| Instance Profile with SSM permissions | The ec2 has to have an instance profile attached to it that allows it to talk to SSM | [SSM Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/getting-started-create-iam-instance-profile.html)  |
| Support Operating Systems | Currently Windows instances with PS 4.0 and AWS Linux, AWS Linux 2, CENTOS/RHEL 7| NA |

## SSM Association & Targeting

The following tagging schema is leverage for SSM to run the Trend Micro installation:

| Tag Key | Tag Value | Target Description |
| ------- | --------- | --------- |
| trendmicro | linux | targets linux as script needs `sh` |
| trendmicro | windows | target windows as script needs `powershell` |

> **Note:** Tagging is important. If you tag a linux machine as windows, SSM will still try to run the AWS-RunsPowerShellScript causing an error.

The following state associations are created:

1. Linux-TrendMicro -> Runs `AWS-RunShellScript` association
2. Windows-TrendMicro -> Runs `AWS-RunPowerShellScript` association

## Template Parameters

The following parameters are leveraged in the template:

| Parameter | Service | Description |
| --------- | ------- | ----------- |
| Activation URL | The Activation URL for Trend Micro central server |
| Manager URL | The Manager URL for Trend Micro central server |
| Policy ID | Trend Micro Deep Security |Trend Micro Policy ID |
