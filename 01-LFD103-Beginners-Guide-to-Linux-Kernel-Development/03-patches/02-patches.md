## About Patches
> - Linux kernel development is done using git, which was started by Linus Torvalds
    and is currently maintained by Junio C. Hamano.

> - To learn more about git, you can read [A short History of Git](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git) and the [Git Book](https://git-scm.com/book/en/v2) for
    details on how to use git.

> - The first three chapters of the Git Book provide the basics on how to get commit
    history, working with remotes, creating branches, tags, and rebasing to tagged
    versions.

> - These are essential survival skills, necessary for any developer.

> - Developers send changes they want to see in the kernel to the kernel mailing lists
    through email.

> - These changes are called `patches`.

> - Patches are small incremental changes made to the kernel.

> - Each patch contains a change to the kernel that implements one independent
    modification that stands on its own.

> - A patch cannot break the kernel build.

> - Requiring each patch to do one thing makes it easier to isolate regressions;
    reverting a problem patch becomes easier as well.

> - Complex changes to the kernel are thus split into smaller chunks.

> - As an example, if you were to find an existing compile warning while making a
    code change, you would fix it independently in a separate patch instead of
    combining it with your code change.

> - Maintainers have their personal preferences on how granular the patch splitting
    should be for their subsystems.

> - This is true for coding styles as well.

> - Maintainers are good about giving feedback on their preferences during the patch
    review.

<br />
<br />


## What is in a Patch?
> - You can take a look at a real commit on the next page.

> - In the screenshot we highlighted individual components, and we will walk through
    these individual components as well. We used:

```bash
git format-patch -1 --pretty=fuller 3a38e874d70b
```

> - To generate the patch you will see on the next patch and get the complete
    information about this patch.

<br />

![Patch Commit Example](./image-patch-commit.png)

<br />

```plaintext
Patch Components
    Commit ID
        - The auto-generated SHA 1 hash is generated from a cryptographic hash function
          that has all the important information about the patch, such as the commit
          date, the committer's name and email address, the log message, and more.
        - Changing any of the information associated with the Commit ID results in
          changing it.
        - This makes it a tamperproof fast way to compare two commits using the IDs, and
          git pull requests become fast and efficient.

    Commit Header
        "major subsystem: minor area: short description of what is being changed"
        "usbip: usbip_host: cleanup() do_rebind() return path"

        - As you can see in the image provided above, the patch changes the "usbip_host"
          driver, which is a sub-driver of the "usbip" driver.
        - This driver falls under the drivers/usb subsystem.
        - The author of the patch writes this information in a standard format with ":"
          separating the major and minor subsystem fields.
        - You will also see "/" as a separator, which would look like
          "usbip/usbip_host: cleanup do_rebind() return path" instead of
          "usbip: usbip_host: cleanup do_rebind() return path".
        - Using "/" or ":" is determined by the maintainer's preference. If in doubt,
          refer to a few patches for the subsystem for information on individual preferences.

    Commit Log
        - It provides a detailed description of the change and why the change is made.
        - Alternate design choices if any are considered.
        - Detailed about the testing done.
        - The example we provided shows a small change and the commit log is simple and to
          the point.
        - Commit logs can be long for patches that fix panics, as they include panic stack
          traces.
        - We encourage you to take a look at a few commit logs in the kernel source
          repository to get a better understanding of the kind of information that is relevant
          to include in them.

    Author
        - This componennt provides the author's name and email information.
        - This information can be specified when you run "git commit" or it can be configured
          in your ".gitconfig" file, which is a very convenient way to generate commits.

    Author Date
        - Auto-generated commit time and date.
        - This value comes from the system time of your computer when you create the change.
```
