# cfn-modules: AWS EBS volume

AWS EBS volume with [alerting](https://www.npmjs.com/package/@cfn-modules/alerting).

## Install

> Install [Node.js and npm](https://nodejs.org/) first!

```
npm i @cfn-modules/ebs-volume
```

## Usage

```
---
AWSTemplateFormatVersion: '2010-09-09'
Description: 'cfn-modules example'
Resources:
  Volume:
    Type: 'AWS::CloudFormation::Stack'
    Properties:
      Parameters:
        VpcModule: !GetAtt 'Vpc.Outputs.StackName' # required
        AlertingModule: !GetAtt 'Alerting.Outputs.StackName' # optional
        KmsKeyModule: !GetAtt 'Key.Outputs.StackName' # optional
        AZChar: 'A' # optional
        Size: '64' # optional
        Iops: '99' # optional (set to 99 to disable)
        BackupRetentionPeriod: '30' # optional
        BackupScheduleExpression: 'cron(0 5 ? * * *)' # optional
      TemplateURL: './node_modules/@cfn-modules/ebs-volume/module.yml'
```

## Examples

* [ec2-ebs](https://github.com/cfn-modules/docs/tree/master/examples/ec2-ebs)

## Related modules

* [ec2-instance-amazon-linux](https://github.com/cfn-modules/ec2-instance-amazon-linux)
* [ec2-instance-amazon-linux2](https://github.com/cfn-modules/ec2-instance-amazon-linux2)
* [efs-file-system](https://github.com/cfn-modules/efs-file-system)

## Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Default</th>
      <th>Required?</th>
      <th>Allowed values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VpcModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/vpc">vpc module</a></td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>AlertingModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/alerting">alerting module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>KmsKeyModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/kms-key">kms-key module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>AZChar</td>
      <td>Availability zone char</td>
      <td>A</td>
      <td>no</td>
      <td>[A, B, C]</td>
    </tr>
    <tr>
      <td>Size</td>
      <td>The size of the volume, in gibibytes (GiBs)</td>
      <td>64</td>
      <td>no></td>
      <td>[4-16384]</td>
    </tr>
    <tr>
      <td>Iops</td>
      <td>The number of I/O operations per second (IOPS) that the volume supports (set to 99 to disable)</td>
      <td>99</td>
      <td>no</td>
      <td>[99-32000]</td>
    </tr>
    <tr>
      <td>BackupRetentionPeriod</td>
      <td>The number of days to keep backups of the EBS volume (set to 0 to disable)</td>
      <td>30</td>
      <td>no</td>
      <td>[0-35]</td>
    </tr>
    <tr>
      <td>BackupScheduleExpression</td>
      <td>A CRON expression specifying when AWS Backup initiates a backup job</td>
      <td>cron(0 5 ? * * *)</td>
      <td>no</td>
      <td></td>
    </tr>
  </tbody>
</table>

## Limitations

* Highly available: EBS volumes only live in a single AZ by design
* Scalable: EBS volumes throughput is limited by design
* Operations friendly: Alerting is not enabled
