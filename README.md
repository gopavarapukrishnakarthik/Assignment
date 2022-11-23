# Assignment
submit as a assignment
# upload all the files to the repository
# open terminal and run 
aws ecr create-repository --repository-name Apprepository --region us-west-1
# connect with docker and aws
# Build the docker image
docker build -t krishna/web/app .
docker tag web-app :latest [Apprepository URI]:v1
#docker push [Apprepository URI]:v1
docker push our AWS ID .dkr.ecr.us-east-1.amazonaws.com/app:v1

# launch a cluster
aws cloudformation deploy --stack-name nodejs --template-file cluster.yml --region us-west-1 --capabilities CAPABILITY_IAM

# launch a service
aws cloudformation deploy \
  --stack-name nodejs-service \
  --template-file service.yml \
  --region us-west-1 \
  --parameter-overrides StackName=nodejs \
                        ServiceName=App service \
                        ListenerArn=arn:aws:elasticloadbalancing:us-west-1:209640446841:listener/app/empir-Publi-8P1LMMEYPQD3/259190f1dd5cf73d/cf0803942aa32eb2 \
                        ImageUrl=209640446841.dkr.ecr.us-east-1.amazonaws.com/app:v1 \
                        Path=* \
                        Priority=1
                        
# go to output and You can fetch a URL from the service API using your browser or curl.      


# Add GITHUB for continuous intergation
Go to github repository and actions tab.
place the prepared aws.yml file and exicute to get start for Continuous integration.
