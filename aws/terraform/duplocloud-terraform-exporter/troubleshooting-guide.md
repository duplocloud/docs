# Troubleshooting Guide

While executing the Utility, If you encounter an issue, we suggest referring the following guide to help you troubleshoot.

<details>

<summary>no valid credential sources for S3 Backend found.</summary>

`duplo_token` has expired. Access DuploCloud Portal> User > Profile > Temporary API Token and export

```
export duplo_token="xxx-xxxxx-xxxxxxxx"
```



</details>

<details>

<summary>NoSuchBucket: The specified bucket does not exist status code: 404</summary>

If you encounter this error while executing `make run`

Set `DISABLETFSTATERESOURCECREATION` key as false in DuploCloud.

Please [contact the DuploCloud team](https://duplocloud.com/company/contact-us/) for assistance.

</details>

