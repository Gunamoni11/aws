node ('main') {
 parameters{
    string (name: 'keyname', defaultValue: 'terra', description: ' ')
    string (name: 'SecurityGroup', defaultValue: 'sg-0244e3f85210cc582', description: ' ')
    string (name: 'Subnet', defaultValue: 'subnet-04bb8948', description: ' ')
            }
  stages{
               stage('cr lb'){
           sh "aws elbv2 create-listener --load-balancer-arn ${jsonitem['LoadBalancers'][0]['LoadBalancerArn']} --protocol HTTP --port 80 --default-actions Type=forward,TargetGroupArn=${jsonitem1['TargetGroups'][0]['TargetGroupArn']} --region us-east-2"
               }
           stage ('creating aclc'){
           sh "aws autoscaling create-launch-configuration --launch-configuration-name my-lc3-cli --image-id ami-0fb653ca2d3203ac1 --instance-type t2.micro --security-groups " + SecurityGroup + " --key-name " + keyname + " --user-data file://userdata.txt --iam-instance-profile demo_full_access --user-data file://userdata.txt --region us-east-2"
          }
           stage('creating asg'){
           sh "aws autoscaling create-auto-scaling-group --auto-scaling-group-name my-asg3-cli --launch-configuration-name my-lc3-cli --max-size 2 --min-size 1 --desired-capacity 1 --target-group-arns ${jsonitem1['TargetGroups'][0]['TargetGroupArn']} --availability-zones us-east-2c --region us-east-2"
        }
       }
  }
