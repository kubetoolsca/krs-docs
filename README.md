# Krs Official Documentation

## Running locally

Clone the repository and run the following command:

```bash
hugo server
```

## Running a container locally

You can run docsy-example inside a [Docker](https://docs.docker.com/)
container, the container runs with a volume bound to the `docsy-example`
folder. This approach doesn't require you to install any dependencies other
than [Docker Desktop](https://www.docker.com/products/docker-desktop) on
Windows and Mac, and [Docker Compose](https://docs.docker.com/compose/install/)
on Linux.

1. Build the docker image

   ```bash
   docker-compose build
   ```

1. Run the built image

   ```bash
   docker-compose up
   ```

   > NOTE: You can run both commands at once with `docker-compose up --build`.

1. Verify that the service is working.

   Open your web browser and type `http://localhost:1313` in your navigation bar,
   This opens a local instance of the docsy-example homepage. You can now make
   changes to the docsy example and those changes will immediately show up in your
   browser after you save.

### Cleanup

To stop Docker Compose, on your terminal window, press **Ctrl + C**.

To remove the produced images run:

```bash
docker-compose rm
```
For more information see the [Docker Compose documentation][].

## Using a local Docsy clone

Make sure your installed go version is `1.18` or higher.

Clone the latest version of the docsy theme into the parent folder of your project. The newly created repo should now reside in a sibling folder of your site's root folder.

```shell
cd root-of-your-site
git clone --branch v0.7.2 https://github.com/google/docsy.git ../docsy
```

Now run:

```shell
HUGO_MODULE_WORKSPACE=docsy.work hugo server --ignoreVendorPaths "**"
```

or, when using npm, prepend `local` to the script you want to invoke, e.g.:

```shell
npm run local serve
```

By using the `HUGO_MODULE_WORKSPACE` directive (either directly or via prefix `local` when using npm), the server now watches all files and directories inside the sibling directory `../docsy` , too. Any changes inside the local `docsy` theme clone are  now immediately picked up (hot reload), you can instantly see the effect of your local edits.

In the command above, we used the environment variable `HUGO_MODULE_WORKSPACE` to tell hugo about the local workspace file `docsy.work`. Alternatively, you can declare the workspace file inside your settings file `hugo.toml`:

```toml
[module]
  workspace = "docsy.work"
```

Your project's `hugo.toml` file already contains these lines, the directive for workspace assignment is commented out, however. Remove the two trailing comment characters '//' so that this line takes effect.



This error occurs if you are running an outdated version of Hugo. As of docsy theme version `v0.7.0`, hugo version `0.110.0` or higher is required.
See this [section](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/#install-hugo) of the user guide for instructions on how to install Hugo.

Or you may be confronted with the following error:

```console
$ hugo server


