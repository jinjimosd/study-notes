
- So sanh cac instance type:
  + https://instances.vantage.sh/
- Tinh toan chi phi cho AWS:
  + https://calculator.aws/#/

- Instance purchasing options: 
  - Saving plan instacnes

- EC2 Service
  - Amazon EC2 instance storage: Temporary store: caching, file tạm
- Snapshot instanse tu dong luu vao s3 budgit.

- Su dung lamda, ... viet job tu dong xoa image, snapshot ma ko su dung

- De thi hoi ve IOPS, chon IOPS phu hop cua tung loai storage

- Doc qua ve IOPS
https://viettelidc.com.vn/tin-tuc/iops-la-gi-va-tai-sao-no-lai-quan-trong

- hoc thuoc bang cuu chuong:
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html

- Doc them ve: 
https://aws.amazon.com/blogs/database/understanding-burst-vs-baseline-performance-with-amazon-rds-and-gp2/

- Encrypt volume (at-rest): Doc them ve encrypt at-rest
- EBS-optimized (de thi hoi):
- Incremental : a => b. Co xoa dc snapshot a.
- Dung thu snapshot lifecycle manager.
- Moi EC2 nen dung 1 key pair rieng, single each one ec2.
- Network Interface

1. 
- Elastic IP: Ip public
- Enhanced networking: more bandwitth, (Fabric ELASTIC)
- HOI: 1 group co the add 1 instance da chay hay khong
- HOI: co the gan 1 instance vao nhieu group duoc khong
- EC2 lifecycle (hoc thuoc)
- EC2 user data
- Other config
- Connect to instance
- ssh, rdo, ... nen dung sesson management (SSO)
- EC2 co the dung role ket noi den s3 (SSO)
- Computing, networking, storage, security.

- Agenda: 
- EFS:
- Manager NFS
- Thuc hanh tao EFS, mount vao nhieu instance cung sua

- S3: simple storage service (dung cho static file)
- S3: global
- budget: regional
- limit account 100 budget:
- check xem so luong budget la soft limit hay hard limit
- Tinh chat: Data durability and HA with persistent storage
- S3 storage class
- 

https://aws.amazon.com/vi/what-is/service-oriented-architecture/
- S3 support lifecycle management ho tro chuyen doi giua cac s3 storage class
- IAM rule for s3 bucket force https https://repost.aws/knowledge-center/s3-bucket-policy-for-config-rule

6. 
- KMS co hai loai:
  - AWS managed key
  - Customer managed key

- Bai toan enterprise: 
  - Tao rieng mot account moi (khong phai IAM user) chi luu tru cac thong tin security (KMS, ...)
- Tao budget khong mat tien, luu du lieu vao moi mat tien
- Trong budget, upload 1 object moi mac dinh dung key cua budget, co the chon rieng cach encrypted.
- Moi object co the luu cac key khac nhau trong 1 budget
- Co the update key cua object, tuy nhien phai lam bang tay..
https://docs.aws.amazon.com/AmazonS3/latest/userguide/ServerSideEncryptionCustomerKeys.html (bai thi hoi)
- DNS provider co the force http tu dong chuyen thanh https
- Bucket policy
- access list (bucket, object)
- S3 access log (audit)

- Replication:
  - Cross Region Replication (CRR)
  - Same region Replication (SRR)
  - Must enable versioning in source and destination
  - After activating, only new object are replicated (old is not)

- Pre-Signed URLs
- Dung khi muon up thang file len s3, khong can di qua application url, khong ton bandwinth.

- Lifecycle Managerment
- Multipart upload & Byte-range fetches
- Neu upload multi path file xong bi mat mang, thi cac part aws se xu ly nhu the nao, xoa trong bao lau

- S3 transfer Acceleration (S3TA)
  - Bai toan global

- Data consistency:
  - Strong read-after-write-consistency

8. VPC
- https://cidr.xyz/ 
- 10.88.135.144/28
  - /28: prefix
  - 10.: 1 octet tuong duong 8 bit => 2^8 don vi.
  - Khong nen dat mot cai dai IP co range qua lon, chi nen dat range vua du de co the mo rong ra duoc. Neu dat het (0.0.0.0/0) thi choi mot minh, khong 1 router nao du kha nang de quan ly.
** Tu thiet ke 1 vpc
- VPC limit 5 cho 1 region. Day la soft limit, neu can hon thi request cho AWS.
- CIDR limit prefix tu 16 den 28
- Thuc te thi co the thiet ke CIDR trung voi CIDR default cua AWS. Tuy nhien nen thiet ke khac vi mai sau co the peer 2 CIDR voi nhau.
- Moi subnet tuong ung voi mot AZ
- Giua cac tang khong nen dung chung route table
- Private subnet khong the truy cap internet => Can tao NAT Gateway gan vao public subnet, gan 1 Elastic ip => sua route table cua private subnet gan vao Nat Gateway.
- NACL la stateless.
  - Rule number uu tien so be hon. Rule be allow rule lớn deny => allow.
  - NACL cho phep deny 1 ip, 1 dai ip.
- NAT:
  - NAT instance: disable Source/destination check
- Bang cuu chuong: so sanh NAT gateway va NAT instance.

9. VPC (TIEP)
- Cac yeu to anh huong den toc do duong truyen: 
  - Instance type, network interface (fabric)
  - ** Thử cấu hình HA cho một con NAT attact 2 con NAT vào cùng 1 route table
- Egress-only internet
  - ** xoa NAT gateway co ra internet duoc khong, xoa egress co ra internet duoc khong (slice 45)
- NAT Instance co the su dung de lam Bastion host => khong nen dung, nen dung session management. (hoặc https://www.cyberark.com/)
- VPC Peering:
- Private Link
- VPC Endpoint

- AWS VPN 
- Ram la gi
- Performance incresing Network: o Global Accelerator
- Cname, root53
- Flow log: debug request den app.