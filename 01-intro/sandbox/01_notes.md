1. in AWS, create an EC2 instance.
    1. [Log in to AWS console](https://aws.amazon.com/console)
    2. Go to the Instances dashboard and (assuming you don't already have an instance) launch an instance.
    3. Make selections for your instance
        * Enter a name
        * Choose the OS distro (Ubuntu 22.04 LTS is fine)
        * Select CPU architecture (choose 64-bit x64; Arm chips aren't as well supported)
        * Select instance type (note the number of CPUs, GiBs of memory, and price (although you'll only be charged while your instance is running, so shut it down when not in use); Consider 8 GiB a minimum for MLops)
        * Select or create an ssh key pair
            * create a key pair
            * Enter a name, select RSA as the type and `.pem` as the private key format
            * Move this file into your ~/.ssh directory
        * Default network settings are fine for now
        * Increase the storage to 30+ GiB (general purpose SSDs are fine)
        * Default **Advanced Details** are fine.
        * Launch your instance.
    4. Go the the instance summary for your new (running) instance and get the public IP address.
    5. SSH into your instance

        ```bash
        ssh -i ~/.ssh/your_aws_key.pem ubuntu@34.567.890.12
        ```

        * Note: if you get an error like `Permissions 0664 for '~/.ssh/your_aws_key.pem' are too open.`, that means you need to `chmod` that key so that only your user account has read-write powers. Do this via `chmod 600 ~/.ssh/your_aws_key.pem`. After `chmod`ing, you should be able to ssh right in.
    6. Set up a connection config in ~/.ssh/config

        ```bash
        Host a_connection_alias_name
            HostName 34.567.890.12
            User ubuntu
            IdentityFile ~/.ssh/your_aws_key.pem
        ```

        * Now you'll be able to ssh in via `ssh a_connection_alias_name` (pick a better alias than that, though).
        * Note: Your instance's public IP address; will change when you shut it down and restart it.

    7. install miniconda.