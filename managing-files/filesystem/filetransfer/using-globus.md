# Using Globus

Globus Online provides a transfer service for moving data between institutions such as Brown and XSEDE facilities. You can also use Globus to transfer files between these institutions and your local machine. Files can be transferred using the Globus web interface or the command line interface.

### Using Globus

To use Globus, first create a personal Globus ID account. You can then use either the web or command line interface to move files.

The instructions below demonstrate using the [web interface ](https://app.globus.org/file-manager)to perform a transfer:

After logging in to Globus you will see the [transfer](https://app.globus.org/file-manager) page. To set up the transfer user the select the "to" and "from" end point to transfer files. You will need to use your Oscar username and password to connect to the Oscar endpoint. Use either of the following endpoints:

```text
brownccv#Brown-CCV-oscar-1
brownccv#Brown-CCV-oscar-2
```

If you want to use Globus Online to move data to/from you own machine, you can install Globus Connect Personal. Installing Globus Connect Personal allows you to create an endpoint on your computer that you can use to transfer data to and from your computer. For installation details see: [https://www.globus.org/globus-connect-personal](https://www.globus.org/globus-connect-personal)

You can then select the files you want to transfer.

You start the transfer using the button in blue shown below. You should see "Transfer request submitted successfully" and an id for the transfer.

If you have started a transfer between two remote machines you don't have to keep your computer connect to Globus. When the transfer is compete you will receive and email. **Note if you are using Globus Connect Personal for a transfer to/from your machine, Globus personal will need to stay running on your machine for the transfer to complete.**

## Tips for Transferring Data between Globus and Google Drive

For Google Drive, there are "rates limits" on how much data and how many files a user can transfer in any 24 hours period. The following two tips can help to alleviate the restrictions from the rates limits:

* transfer a subfolder as a job. A user can submit 2-3 jobs at a time.
* compress the folder or subfolders with a lot of small files, e.g., using tar, before transfer

