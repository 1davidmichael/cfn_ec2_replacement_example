# CFN Example Volume Resize Without Replacement

This repo provides an example of using CloudFormation to add a volume to an EC2 instance that is able to be grown via CloudFormation without triggering a replacement.

The issue is that any devices changed within `BlockDeviceMappings` will cause a replacement when the volumes are grown, even with the volume is the root one.

<https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html#cfn-ec2-instance-blockdevicemappings>

The solution is instead to define a custom EC2 EBS volume and use [AWS::EC2::VolumeAttachment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-ebs-volumeattachment.html#aws-properties-ec2-ebs-volumeattachment--examples) to attach to the given instance. This will allow the volume to be grown within CloudFormation without a replacement. Note that in order to see the new size you will still need to grow the volume from the OS perspective. See here for details on how to do this: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html
