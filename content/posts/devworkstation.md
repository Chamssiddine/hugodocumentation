---
title: "Developers Workstation"
date: 2023-01-19T14:53:23+01:00
draft: false
cover: 
    video: /add.mov
    alt: 'this is a video'
    caption: 'caption'

---


We will be explaining how to create VMs for our Developers
## Creating VMs
To create new VMs, you'll need to navigate to the **Workstation Module**
```
$ cd infrastructure/modules/workstation
```
Apply the Terraform file using the following command:

```ruby
$ terrafrom apply

```
This will create the necessary infrastructure on your cloud provider (e.g. Google Cloud Platform) and provision new VMs for your developers.
## Adding new developer

To add a new developer to the project, you'll need to modify the main.tf file in the Terraform module for workstations. Here's how you can do it:

1. Navigate to the ./infrastructure/workstation directory.

2. Open the main.tf file and add a new line to the locals block. Here's an example of what it should look like:

```terraform
locals {
  // to add new workstation just add a new list with it's name, machine_type, your prefered os and zone
  workstations = {
  "workstation1" = { machine_type = "e2-medium", zone = "europe-west9-a", tag = ["ping", "ssh","metrics"], image = "debian-cloud/debian-11", bucket_name = "uniquename" },  
  "workstation2" = { machine_type = "e2-micro", zone = "europe-west9-a", tag = ["ping", "ssh","metrics"], image = "debian-cloud/debian-11", bucket_name = "uniquename" },
 "workstation3" = { machine_type = "e2-micro", zone = "europe-west9-a", tag = ["ping", "ssh"], image = "debian-cloud/debian-11", bucket_name = "uniquename" }
  }
}

```
Make sure to replace the values with the appropriate ones for your new developer.

![Creating another workstation](https://user-images.githubusercontent.com/62959061/229340280-1b1614f1-7140-4274-b8df-a177f1aecf0c.mov)

![Creating another workstation](/g.gif)

3. Save the main.tf file.

4. Apply the changes using the following command:

* After modfiying you need to apply the changes using:

```ruby
$ terrafrom apply
```

This will provision a new VM for the new developer with the specified settings.

## Conclusion

That's it! You should now have a new VM for the new developer ready to use. If you have any questions or run into any issues, feel free to reach out to me for assistance. I'm always happy to help!
