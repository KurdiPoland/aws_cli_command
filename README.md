# Usefull comamnd of aws_cli_command
#AWS  
 aws configure --profile iam-manage
 aws configure list
 aws configure list-profiles
 aws sts get-caller-identity --profile <profile>
 aws s3 ls



#wylistowanie vpc
aws ec2 describe-vpcs

#wylistowanie vpc ale tylko nazwa
aws ec2 describe-vpcs --query 'Vpcs[*].VpcId' 

#wylistowanie Ec2 tylko nawy oraz statusy
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[Tags[?Key==`Name`].Value | [0], State.Name]' --output table


##wylistowanie Ec2 tylko tych z tagkey='Name'
aws ec2 describe-instances --filters "Name=tag-key,Values=Name" --query "Reservations[*].Instances[*].[InstanceId, State.Name, Tags[?Key=='Name'].Value | [0]]" --output table

#wylistowanie Ec2
aws ec2 describe-instances

#wyświetlanie Ec2 z wykorzystaniem filtra
 aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"

#wyswietlwnie Ec2 z wykorzystaniem id
aws ec2 describe-instances --instance-id <id-ec2-instance>

#wryfikacja security group 
aws ec2 describe-security-groups --group-ids <id-security-group>


#weryfikacja security group rule na podstawie podanego SG id
aws ec2 describe-security-group-rules --filter Name=group-id,Values=<id-security-group>
Jeżeli poszczególne wyświetlnose security groups rule zawierają 
"IsEgress": false -> to znaczy że to są rule inbound
"IsEgress": true -> to znaczy że są outbound

====================
#SG
====================

aws ec2 describe-instances --instance-ids <instance_id> --query "Reservations[*].Instances[*].SecurityGroups[*]" --output table

aws ec2 describe-instance-attribute \
    --instance-id i<ec2_id> \
    --attribute groupSet

aws ec2 describe-security-groups \
  --group-ids <id_sg>

====================
#S3
====================

#Usuniecie backetu po nazwie
aws s3api delete-bucket --bucket <nazwa-bucketu>

#Lista objektów w backecie
aws s3api list-objects --bucket your-bucket-name

#lista objektórw w backend przez s3://
aws s3 ls s3://<backet0name>/<objects>

#Weryfiakcja wersjonowanych obejektów w S3
aws s3api list-object-versions --bucket terraform-state-storage-0310241354

#pobranie pliku z s3 bucket o określonej wersji
aws s3api get-object --bucket terraform-state-storage-0310241354 --key <path_to_file>/<file> --version-id <VersionID> .<local_path>/<file>

#weryfikacja działąjacych instacji rds
aws rds describe-db-instances

#weryfikacja instancji rds
aws rds describe-db-instances --query "DBInstances[*].{DBInstanceIdentifier:DBInstanceIdentifier,Engine:Engine,DBInstanceStatus:DBInstanceStatus}" --output table

#wylistowanie DB po konkretnych tagach


====================================================================================================
#wylistowanie iam role
aws iam list-roles

#wylistowanie iam_role , tylko nazwy
aws iam list-roles --query "Roles[*].RoleName" --output text
