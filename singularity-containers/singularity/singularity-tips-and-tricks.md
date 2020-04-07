# Singularity Tips and Tricks

The following are some handy quick tips for users just getting started with Singularity:

* Default images will automatically bind your $HOME and /tmp/ \(among a few other locations\). This will not automatically bind your data/ or scratch/ directories, so you may want to review the [Mounting and binding](accessing-oscar-filesystem.md) documentation.
* Your environment will include your $HOME which comes with anything user-specific installed in your .local directories. I point this out for any python users who have installed packages using pip --user. I was building a tensorflow singularity image which was having issues as there were previously existing custom numpy installs in my .local causing conflicts.
* Avoid making very large images. No need to build a 5g container most of the time. Keep it lean and only include the tools/packages you need to do your work. Bloat is bad!
* Keep your data out of your containers where possible. It is always faster to mount volumes in `/gpfs/data` or `/gpfs/scratch` rather than try and bundle the data into the container.

