# Condo/Priority Jobs

{% hint style="info" %}
**Note:** we do not provide users condo access by default if their group/PI has a condo on the system. You will have to explicitly request a condo access and we will ask for approval from the PI.
{% endhint %}

To use your condo account to submit jobs, include the following line in your batch script:

```text
#SBATCH --account=<condo-name>
```

You can also provide this option on the command line while submitting the job using `sbatch`:

```text
$ sbatch --account=<condo-name> <batch-script>
```

Similarly, you can change the account while asking for interactive access too:

```text
interact -a <condo-name> ... <other_options>
```

Condo account names are typically `<groupname>-condo`, and you can view a full list with the `condos` command on Oscar.

To see the running and pending jobs in a condo:

`condo <condo-name>`

## Premium Account \(priority\) jobs

If you have a premium account, that should be your default QOS for submitting jobs. You can check if you have a premium account with the command `groups`. If you have a priority account you will see `priority` in your the output form `groups`.

You can check the qos for a running job by running the command `myq`. The `QOS` column should show `"pri-<username>"`

If you are interested in seeing all your accounts and associations, you can use the following command:

```text
sacctmgr -p list assoc where user=<username>
```

