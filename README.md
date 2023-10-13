# Prowler-Quick-Start-Guide
Notes on using Prowler for Cloud Assessments

## AWS 🙊

Request AWS Access Key and Secret Access Key and run

```c
aws configure     
AWS Access Key ID [None]: AKI--------SNIP--------
AWS Secret Access Key [None]: CPdP-----------SNIP----------
Default region name [None]: 
Default output format [None]:
```

It is as simple as running `prowler aws` which will use the Access Key and Secret Access Key

```c
prowler aws   
                         _
 _ __  _ __ _____      _| | ___ _ __                                                                                                                                                          
| '_ \| '__/ _ \ \ /\ / / |/ _ \ '__|                                                                                                                                                         
| |_) | | | (_) \ V  V /| |  __/ |                                                                                                                                                            
| .__/|_|  \___/ \_/\_/ |_|\___|_|v3.10.0                                                                                                                                                     
|_| the handy cloud security tool                                                                                                                                                             
                                                                                                                                                                                              
Date: 2023-10-13 06:24:54                                                                                                                                                                     


This report is being generated using credentials below:

AWS-CLI Profile: [default] AWS Filter Region: [all]
AWS Account: [70--------55] UserId: [AID---------------K4K]
Caller Identity ARN: [arn:aws:iam::705-------55:user/prowler]

Executing 291 checks, please wait...

-> Scan completed! |▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉| 291/291 [100%] in 2:50.3 

Overview Results:
╭────────────────────┬─────────────────────╮
│ 54.2% (477) Failed │ 45.34% (399) Passed │
╰────────────────────┴─────────────────────╯

Account 705540354455 Scan Results (severity columns are for fails only):
╭────────────┬───────────────────┬───────────┬────────────┬────────┬──────────┬───────╮
│ Provider   │ Service           │ Status    │   Critical │   High │   Medium │   Low │
├────────────┼───────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ accessanalyzer    │ FAIL (34) │          0 │      0 │        0 │    34 │
├────────────┼───────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ account           │ PASS (3)  │          0 │      0 │        0 │     0 │
├────────────┼───────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ acm               │ FAIL (1)  │          0 │      1 │        0 │     0 │
├────────────┼───────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ athena            │ FAIL (34) │          0 │     17 │       17 │     0 │
├────────────┼───────────────────┼───────────┼────────────┼────────┼──────────┼───────┤

```

## Compliane Framework Specific Testing

If it has been requested that the AWS Account is tested againast a specific compliance framework, e.g. CIS Benchmark, then this can also be done.

Some interesting reading ref AWS CIS 1.4.0 if interested 🥱

https://docs.aws.amazon.com/audit-manager/latest/userguide/CIS-1-4.html

https://www.reddit.com/r/aws/comments/nvyim3/what_is_different_in_the_new_aws_cis_14_benchmark/

```c
prowler aws --list-compliance
                         _
 _ __  _ __ _____      _| | ___ _ __                                                                                                                                                                                                        
| '_ \| '__/ _ \ \ /\ / / |/ _ \ '__|                                                                                                                                                                                                       
| |_) | | | (_) \ V  V /| |  __/ |                                                                                                                                                                                                          
| .__/|_|  \___/ \_/\_/ |_|\___|_|v3.10.0                                                                                                                                                                                                   
|_| the handy cloud security tool                                                                                                                                                                                                           
                                                                                                                                                                                                                                            
Date: 2023-10-13 08:15:17                                                                                                                                                                                                                   

- gxp_eu_annex_11_aws
- nist_800_171_revision_2_aws
- gdpr_aws
- ffiec_aws
- aws_well_architected_framework_security_pillar_aws
- mitre_attack_aws
- nist_800_53_revision_4_aws
- iso27001_2013_aws
- ens_rd2022_aws
- cis_1.5_aws
- rbi_cyber_security_framework_aws
- aws_foundational_security_best_practices_aws
- cisa_aws
- fedramp_moderate_revision_4_aws
- aws_audit_manager_control_tower_guardrails_aws
- fedramp_low_revision_4_aws
- pci_3.2.1_aws
- cis_1.4_aws
- cis_2.0_aws
- nist_csf_1.1_aws
- soc2_aws
- aws_well_architected_framework_reliability_pillar_aws
- gxp_21_cfr_part_11_aws
- nist_800_53_revision_5_aws
- hipaa_aws

There are 25 available Compliance Frameworks.
```

### List the requiremnets specified under the compliance framework

If needed, we can check the requiremnets of each framework with `prowler aws --list-compliance-requirements <FrameworkName>`

```c
prowler aws --list-compliance-requirements cis_1.4_aws                                                            
                         _
 _ __  _ __ _____      _| | ___ _ __                                                                                                                                                                                                        
| '_ \| '__/ _ \ \ /\ / / |/ _ \ '__|                                                                                                                                                                                                       
| |_) | | | (_) \ V  V /| |  __/ |                                                                                                                                                                                                          
| .__/|_|  \___/ \_/\_/ |_|\___|_|v3.10.0                                                                                                                                                                                                   
|_| the handy cloud security tool                                                                                                                                                                                                           
                                                                                                                                                                                                                                            
Date: 2023-10-13 08:24:48                                                                                                                                                                                                                   

Listing CIS 1.4 AWS Compliance Requirements:

Requirement Id: 1.1
        - Description: Maintain current contact details
        - Checks:
                account_maintain_current_contact_details
                                                                                                                                                                                                                                            
Requirement Id: 1.10
        - Description: Ensure multi-factor authentication (MFA) is enabled for all IAM users that have a console password
        - Checks:
                iam_user_mfa_enabled_console_access
                                                                                                                                                                                                                                            
Requirement Id: 1.11
        - Description: Do not setup access keys during initial user setup for all IAM users that have a console password
        - Checks:
                iam_user_no_setup_initial_access_key
                                                                                                                                                                                                                                            
Requirement Id: 1.12
        - Description: Ensure credentials unused for 45 days or greater are disabled
        - Checks:
                iam_user_accesskey_unused
                iam_user_console_access_unused
```

## Run CIS Benchmarks

Simple as running prowler and specifiying to the framework you want to test against

```c
prowler aws --compliance cis_1.4_aws
                         _
 _ __  _ __ _____      _| | ___ _ __                                                                                                                                                          
| '_ \| '__/ _ \ \ /\ / / |/ _ \ '__|                                                                                                                                                         
| |_) | | | (_) \ V  V /| |  __/ |                                                                                                                                                            
| .__/|_|  \___/ \_/\_/ |_|\___|_|v3.10.0                                                                                                                                                     
|_| the handy cloud security tool                                                                                                                                                             
                                                                                                                                                                                              
Date: 2023-10-13 06:24:54                                                                                                                                                                     


This report is being generated using credentials below:

AWS-CLI Profile: [default] AWS Filter Region: [all]
AWS Account: [70--------55] UserId: [AID---------------K4K]
Caller Identity ARN: [arn:aws:iam::705-------55:user/prowler]

Executing 65 checks, please wait...

-> Scan completed! |▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉| 65/65 [100%] in 1:10.3 

Overview Results:
╭─────────────────────┬────────────────────╮
│ 69.39% (170) Failed │ 29.39% (72) Passed │
╰─────────────────────┴────────────────────╯

Account 705540354455 Scan Results (severity columns are for fails only):
╭────────────┬────────────────┬───────────┬────────────┬────────┬──────────┬───────╮
│ Provider   │ Service        │ Status    │   Critical │   High │   Medium │   Low │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ accessanalyzer │ FAIL (17) │          0 │      0 │        0 │    17 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ account        │ PASS (3)  │          0 │      0 │        0 │     0 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ cloudtrail     │ FAIL (19) │          0 │     17 │        0 │     2 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ cloudwatch     │ FAIL (15) │          0 │      0 │       15 │     0 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ config         │ FAIL (17) │          0 │      0 │       17 │     0 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ ec2            │ FAIL (68) │          0 │     17 │       51 │     0 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ iam            │ FAIL (10) │          3 │      1 │        4 │     2 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ s3             │ FAIL (7)  │          0 │      1 │        6 │     0 │
├────────────┼────────────────┼───────────┼────────────┼────────┼──────────┼───────┤
│ aws        │ vpc            │ FAIL (17) │          0 │      0 │       17 │     0 │
╰────────────┴────────────────┴───────────┴────────────┴────────┴──────────┴───────╯
* You only see here those services that contains resources.

Detailed results are in:
 - HTML: /opt/prowler/output/prowler-output-7----------5-20231013082938.html
 - JSON-OCSF: /opt/prowler/output/prowler-output-7----------5-20231013082938.ocsf.json
 - CSV: /opt/prowler/output/prowler-output-7----------5-20231013082938.csv
 - JSON: /opt/prowler/output/prowler-output-7----------5-20231013082938.json

Compliance Status of CIS-1.4 Framework:
╭───────────────────┬──────────────────╮
│ 70.25% (170) FAIL │ 29.75% (72) PASS │
╰───────────────────┴──────────────────╯

Framework CIS-1.4 Results:
╭────────────┬───────────────────────────────────┬───────────┬───────────╮
│ Provider   │ Section                           │ Level 1   │ Level 2   │
├────────────┼───────────────────────────────────┼───────────┼───────────┤
│ AWS        │ 1. Identity and Access Management │ FAIL(26)  │ FAIL(1)   │
├────────────┼───────────────────────────────────┼───────────┼───────────┤
│ AWS        │ 2.1. Simple Storage Service (S3)  │ FAIL(4)   │ FAIL(3)   │
├────────────┼───────────────────────────────────┼───────────┼───────────┤
│ AWS        │ 3. Logging                        │ FAIL(17)  │ FAIL(36)  │
├────────────┼───────────────────────────────────┼───────────┼───────────┤
│ AWS        │ 4. Monitoring                     │ FAIL(10)  │ FAIL(5)   │
├────────────┼───────────────────────────────────┼───────────┼───────────┤
│ AWS        │ 5. Networking                     │ FAIL(51)  │ FAIL(17)  │
╰────────────┴───────────────────────────────────┴───────────┴───────────╯
* Only sections containing results appear.
```

                                              
